# Dija — Roadmap

## v0.1

| Step | Name | Progress |
|------|------|----------|
| 000 | Project Setup, Verification & Robustness | 100% |
| 001 | CLI & Tooling | 20% |
| 002 | Engine | 100% |
| 003 | Viewport & Coordinate System | 100% |
| 004 | Rendering Engine | 100% |
| 005 | Layout Engine | 100% |
| 006 | Style System | 100% |
| 007 | Text Engine | 100% |
| 008 | Event System & Focus | 100% |
| 009 | Effect System & Transitions | 100% |
| 010 | DSL & Macros | 100% |
| 011 | Platform Abstraction | 100% |
| 012 | macOS Backend | 100% |
| 013 | Linux Backend | 100% |
| 014 | Windows Backend | 100% |
| 015 | iOS Backend | 100% |
| 016 | Android Backend | 0% |
| 017 | Zelez Backend | 0% |
| 018 | Input Components | 0% |
| 019 | Container & Navigation Components | 0% |
| 020 | Display & Feedback Components | 0% |
| 021 | Theme System v2 | 0% |
| 022 | Documentation & Examples | 0% |
| 023 | v0.1 Release | 0% |

### v0.2 — Scripting & Plugins

| Step | Name | Progress |
|------|------|----------|
| 024 | Plugin System Core | 0% |
| 025 | Dija VM (bytecode format, interpreter, `no_std`) | 0% |
| 026 | Dijax: Lexer, Parser, AST, Compiler | 0% |
| 027 | Dijax: Full Integration | 0% |
| 028 | dija-ts: TypeScript subset → Dija VM | 0% |

**Dijax** is an Elixir-like scripting language purpose-built for Dija. Pattern matching, pipe operator, immutable data, first-class `defview`/`defservice` for actor definitions. Crate: `dija-script` (`no_std` + `alloc`).

**dija-ts** compiles a subset of TypeScript to bytecode that runs in the same Dija VM as Dijax. No Node.js, no WASM — just familiar syntax compiled to the same actor runtime. `no_std` + `alloc`, runs everywhere Dija runs.

**Plugin system** enables apps to host scripting backends. `PluginHost` trait with multiple implementations: Dijax (built-in), TypeScript subset, WASM. Capability-based permissions. Message-passing communication via `Value` type.

### v0.3 — Web & Companion Crates

| Step | Name | Progress |
|------|------|----------|
| 029 | Web Backend (HTML + CSS) | 0% |
| 030 | dija-grid (Enterprise Data Grid) | 0% |
| 031 | dija-chart (Enterprise Charting) | 0% |
| 032 | dija-automotive (Automotive & Instrument Components) | 0% |
| — | Complex text shaping (Arabic, CJK, emoji) | 0% |
| — | Spring physics animations | 0% |
| — | Variable fonts, ligatures | 0% |

### v0.4 — Embedded

| Step | Name | Progress |
|------|------|----------|
| 033 | Embedded / MCU Target | 0% |
| 034 | Multi-Display | 0% |
| 035 | Hardware Input | 0% |

### v0.5+ — Companion Crates

| Step | Name | Progress |
|------|------|----------|
| 036 | dija-map (Map & GIS) | 0% |
| 037 | dija-editor (Code Editor) | 0% |
| 038 | dija-pdf (PDF Viewer) | 0% |
| 039 | dija-flow (Diagram & Flow Editor) | 0% |
| 040 | dija-schedule (Calendar, Timeline, Gantt) | 0% |
| 041 | dija-sheet (Spreadsheet Engine) | 0% |
| 042 | dija-3d (3D Viewer) | 0% |
| 043 | dija-media (Video & Audio Player) | 0% |

## Companion Crates

All `#![no_std]` + `alloc`, zero external dependencies:

- `dija-engine` — Actor runtime extracted from `dija-core`. Standalone use for CLI tools, build systems, data pipelines. Atoms, Pid, Mailbox (with coalesceable message support), Scheduler, Supervision, Registry, PubSub, Timer. Port I/O for transparent non-blocking I/O (Erlang-style).
- `dija-grid` — Enterprise data grid. Virtual scrolling, grouping, pivoting, cell editing, server-side model.
- `dija-chart` — Enterprise charting. Line, bar, scatter, pie, treemap, heatmap, interactive zoom/brush.
- `dija-automotive` — Automotive instrument components. Gauges, needles, dials, indicators. MCU-ready, depends only on `dija-core`.

## Demo App

**Divine** — GPU-rendered terminal emulator + vim-like modal editor + plugin system. One app, keyboard-first, fully extensible.

## Rendering Architecture

The render pipeline is **polymorphic by design**. Three rendering strategies share the same Node tree, Style system, and `ui!{}` DSL — only the output stage differs.

| Strategy | Targets | Pipeline |
|----------|---------|----------|
| **Self-rendering** | macOS, Windows, Linux, iOS, Android | Node → Layout → DrawList → app-owned GPU |
| **Delegated compositing** | zelez OS | Node → Layout → RenderTree → kernel composites all apps on GPU |
| **Markup generation** | Web | Node → HTML + CSS classes → browser renders |

## Input Architecture

Unified Pointer model for all platforms. Mouse and touch are both pointer input — modern laptops have touch screens, tablets have keyboards. Components handle `Pointer` events, not `Mouse` or `Touch` separately.

## Scripting Architecture

Two-layer scripting model:

| Layer | Purpose | Languages | Constraint |
|-------|---------|-----------|------------|
| **Framework scripting** | Build Dija apps, define components | Dijax | `no_std` + `alloc`, zero deps |
| **Plugin hosting** | End-user app extensibility | TypeScript subset, WASM | All compile to Dija VM bytecode, `no_std` |

`PluginHost` trait in `dija-core` (no_std) defines the interface. Language backends implement it. Apps expose their API via `PluginApi` builder. All cross-language communication uses the `Value` type.
