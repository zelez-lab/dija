# Dija

A cross-platform UI framework written in Rust. GPU-accelerated rendering, Erlang-inspired process model, zero external dependencies.

Dija is the default GUI framework for zelez OS.

## Why Dija

**Every view is a process.** Dija's core is an atom engine inspired by Erlang/OTP. Each view is a lightweight process with its own state and mailbox. Views communicate through message passing — emit to parent, send to Pid, publish to topic. A crashed view gets isolated and restarted without taking down the app.

**One codebase, every platform.** The same view code runs on macOS, Linux, Windows, iOS, Android, and zelez OS. Post-v0.1, the web becomes a target too — same views, rendered as HTML + CSS instead of GPU draw calls.

**Polymorphic rendering.** Three rendering strategies share the same Node tree, Style system, and DSL. Only the output stage differs:

| Strategy | Targets | Pipeline |
|----------|---------|----------|
| Self-rendering | macOS, Windows, Linux, iOS, Android | Node → Layout → DrawList → GPU |
| Delegated compositing | zelez OS | Node → Layout → RenderTree → kernel compositor |
| Markup generation | Web | Node → HTML + CSS classes → browser |

**Process-level debugging.** Suspend a single view without freezing the app. Step through messages one at a time. Trace message flow across views. Set conditional breakpoints on messages. Replay message sequences to reproduce bugs deterministically.

**`no_std` from day one.** Core crates compile with `#![no_std]` + `alloc`. Zero external dependencies except `libm`. Dija runs on bare-metal — it has to, because zelez OS has no standard library.

## Example

```rust
use dija::prelude::*;

ui!(vbox { gap: 16, items: center, p: 24, bg: slate.900,
    text { color: white, font_size: xxl, bold, "{self.count}" }
    el {
        bg: blue.500, rounded: md, p: {x: 16, y: 8},
        hover: { bg: blue.600 },
        pressed: { bg: blue.700 },
        on_click: "increment",
        text { color: white, "Increment" }
    }
})
```

## Architecture

```
crates/
├── dija           Umbrella crate (single user dependency)
├── dija-engine    Actor runtime: atoms, Pid, mailbox, scheduler, supervision
├── dija-core      Layout, style, effects, events, platform backends
├── dija-render    Draw list, GPU backends (Metal, Vulkan), rasterizer, text, atlas
├── dija-macros    Proc macros: ui!
├── dija-icons     Icon catalog (Phosphor Icons, 1512 icons × 6 weights, DCE-friendly)
├── dija-ui        Built-in components + themes
└── dija-cli       CLI: dev server, hot reload, MCP bridge
```

## Platforms

| Platform | Rendering | Status |
|----------|-----------|--------|
| macOS | Metal + AppKit | v0.1 |
| Linux | Vulkan + Wayland/X11 | v0.1 |
| Windows | Vulkan + Win32 | v0.1 |
| iOS | Metal + UIKit | v0.1 |
| Android | Vulkan + NDK | v0.1 |
| zelez OS | Kernel compositor | v0.1 |
| Web | HTML + CSS | v0.2 |

## Components

25 components with per-platform native look and feel:

Alert, AppBar, Badge, Button, Chip, DataTable, DatePicker, FAB, ListView, ProgressBar, SearchBar, SegmentedControl, Select, Sheet, Sidebar, Slider, Spinner, Stepper, Switch, TabBar, TextArea, TextField, TimePicker, Toast, Tooltip

## CLI

```bash
dija dev [--path <dir>] [-p <pkg>]     # Build + run with hot reload
dija mcp [--path <dir>] [-p <pkg>]     # MCP bridge (JSON-RPC on stdin/stdout)
dija new <name> [--target <t>]         # Create a new project from template
dija build [--target <t>]              # Production build
dija generate view|component|theme     # Code generation
dija translate                         # Convert HTML to ui!{} syntax
dija bundle [--target <t>]             # Package for distribution
dija doctor                            # Check environment
dija fmt                               # Format ui!{} macro blocks
```

`dija dev` owns the window and engine. Your app builds as a cdylib — on file change, only the root view is killed and re-spawned from the new library. Window, GPU pipeline, and engine stay alive.

The MCP bridge connects Claude Code to a running app. Inspect the UI tree, click elements, hover, scroll, step through view messages — all from the terminal.

## Status

Active development. The engine, layout (flexbox + grid), style system (Tailwind-inspired DSL), effects and transitions, text engine, event system, rendering pipeline, and platform abstraction are complete. Platform backends for macOS, Linux, Windows, and iOS are implemented. Components and documentation are in progress toward v0.1.

Source code will be published with the v0.1 release.

See [ROADMAP.md](ROADMAP.md) for the full plan.

## License

GPL-3.0. See [LICENSE](LICENSE).

Contributions require signing the [Contributor License Agreement](CLA.md).
