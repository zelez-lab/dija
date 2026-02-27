# Maintainer Guide

This document covers build-time processes and workflows that only Dija maintainers need to know about.
Users building apps with Dija don't need any of this — `cargo build` just works.

## Pre-compiled Artifacts Policy

Several build artifacts are **checked into the repo** so that users never need external tools:

| Artifact | Source | Tool | Location |
|----------|--------|------|----------|
| SPIR-V bytecode (`.spv`) | `.glsl` shaders | `glslangValidator` | `crates/dija-render/src/vulkan/spv/` |
| Baked glyph atlas | Inter TTF files | `build.rs` (self-contained) | Generated in `$OUT_DIR` at build time |
| Icon path data | Phosphor SVG files | `build.rs` (self-contained) | Generated in `$OUT_DIR` at build time |

**Rule:** if a build step requires an external tool, pre-compile the output and commit it.
Users should only need `rustc` and `cargo`.

## Vulkan Shaders (GLSL → SPIR-V)

GLSL shader sources live alongside their compiled SPIR-V in `crates/dija-render/src/vulkan/spv/`.
The Vulkan backend embeds `.spv` files via `include_bytes!` — no runtime compilation.

### Editing shaders

1. Edit the `.glsl` source
2. Run `just shaders` to recompile all `.spv` files
3. Commit both the `.glsl` and `.spv` together

### Tool installation

`just shaders` requires `glslangValidator` from the [Khronos glslang](https://github.com/KhronosGroup/glslang) project:

```bash
# macOS
brew install glslang

# Ubuntu/Debian
apt install glslang-tools

# Arch
pacman -S glslang
```

### Why not compile at build time?

Using `glslangValidator` in `build.rs` would require every user building with `feature = "vulkan"` to install it.
Pre-compiled `.spv` checked into the repo avoids that. An alternative would be using [naga](https://github.com/gfx-rs/wgpu/tree/trunk/naga) as a build dependency (pure Rust GLSL/WGSL → SPIR-V), but that adds a crate dependency to the build graph.

## Font Atlas Baking

`crates/dija-render/build.rs` contains a **self-contained TTF parser and glyph rasterizer** (no external dependencies).
When `feature = "default-font"` is enabled, it:

1. Parses Inter TTF files (Regular 400, Medium 500, Bold 700) from `crates/dija-render/data/fonts/`
2. Rasterizes glyphs at 6 sizes (12, 14, 16, 18, 20, 24 px) for Latin characters (U+0020–00FF)
3. Shelf-packs them into a 1024×1024 atlas with sRGB coverage encoding
4. Emits `$OUT_DIR/baked_fonts.rs` with the atlas pixels, glyph metrics, and font data constants

This runs automatically during `cargo build` — no maintainer action needed unless you're changing the baked font set or rasterizer logic.

### Key parameters

- `ATLAS_SIZE`: 1024×1024 (increase if you add more weights/sizes)
- `SIZES`: `[12.0, 14.0, 16.0, 18.0, 20.0, 24.0]`
- `WEIGHTS`: Inter Regular, Medium, Bold
- Coverage encoding: sRGB gamma correction (`R8_UNORM` atlas format)

## Icons (dija-icons)

`crates/dija-icons/` is a curated icon catalog (Phosphor Icons fork, 1512 icons × 6 weights). Its `build.rs` is fully self-contained — no external dependencies.

### Build pipeline

1. **SVG → PathCommand**: `build.rs` parses SVG files from `crates/dija-icons/svg/{weight}/` and converts path data into static `PathCommand` arrays
2. **Pre-tessellation** (optional, `feature = "pre_tessellated"`): bakes triangle meshes at compile time so rendering is O(n) scale instead of O(n log n) tessellation per frame
3. **Codegen**: emits `$OUT_DIR/catalog/{weight}.rs` with one `pub const ICON_NAME: IconData` per icon

### Dead code elimination (DCE)

Icons are designed for aggressive DCE — only icons your app actually references end up in the binary:

- **Static names** (`icon { name: "play" }`) → compiles to `&::dija::icons::regular::PLAY`. Unreferenced icons are eliminated by the linker. This is the default and recommended path.
- **Dynamic names** (`icon { name: variable }`) → requires `feature = "lookup"`, which generates a runtime lookup table referencing *all* enabled icons. This defeats DCE — use only when icon names come from data at runtime.

### Verifying DCE

```bash
just verify-icon-dce
```

Builds two binaries (one with a single icon reference, one baseline) and compares sizes. Delta should be ~8 KB for one icon. If significantly larger, DCE is broken.

### Adding new icons

Drop `.svg` files into `crates/dija-icons/svg/{weight}/` and rebuild. The `build.rs` picks them up automatically. Icon names are derived from filenames (kebab-case → SCREAMING_SNAKE_CASE).

### Features

| Feature | Default | Effect |
|---------|---------|--------|
| `regular` | Yes | Enable regular weight icons |
| `thin`, `light`, `bold`, `fill`, `duotone` | No | Enable other weights |
| `pre_tessellated` | Yes | Bake triangle meshes at compile time |
| `lookup` | No | Runtime name → icon resolution (defeats DCE) |
