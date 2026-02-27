# Linux (GNOME/Adwaita) — Surfaces

Source: GNOME Human Interface Guidelines, libadwaita 1.x

Adwaita's signature look: **flat, opaque, card-based** layouts with clear hierarchy.
No blur effects. No translucency in standard components.

## Design Philosophy

Unlike iOS (layered translucency) or macOS (vibrancy/blur), GNOME/Adwaita achieves
visual hierarchy through:

1. **Color differentiation** — distinct background colors per surface level
2. **Subtle borders** — 1px borders at ~15% opacity
3. **Minimal shadows** — small, tight shadows to suggest elevation
4. **Card grouping** — related content collected in rounded-corner cards

## Surface Levels

### Light Theme

| Level | Surface | Background | Notes |
|-------|---------|------------|-------|
| 0 | Window base | `#FAFAFA` | Lowest layer |
| 1 | Header bar | `#EBEBEB` | Slightly darker than window |
| 1 | Sidebar | `#EBEBEB` | Same level as header bar |
| 2 | View (content area) | `#FFFFFF` | Brighter than window |
| 2 | Cards | `#FFFFFF` + 1px border + shadow | Sits on top of window |
| 3 | Popovers | `#FFFFFF` + shadow | Floats above content |
| 4 | Dialogs | `#FAFAFA` + large shadow | Modal overlay |
| 5 | OSD elements | dark bg, ~`rgba(0,0,0,0.80)` | On-screen display |

### Dark Theme

| Level | Surface | Background |
|-------|---------|------------|
| 0 | Window base | `#242424` |
| 1 | Header bar | `#303030` |
| 1 | Sidebar | `#303030` |
| 2 | View (content area) | `#1E1E1E` |
| 2 | Cards | `#383838` + 1px border + shadow |
| 3 | Popovers | `#383838` + shadow |
| 4 | Dialogs | `#383838` + large shadow |
| 5 | OSD elements | `rgba(0,0,0,0.80)` |

## Header Bar

The header bar is Adwaita's defining surface — a colored band at the top with CSD
(client-side decorations) integrating window controls.

| Property | Light | Dark |
|----------|-------|------|
| Background | `#EBEBEB` | `#303030` |
| Backdrop (unfocused) | `#FAFAFA` | `#242424` |
| Bottom border | `rgba(0,0,0,0.15)` | `rgba(255,255,255,0.15)` |
| Min height | 47px | 47px |
| Padding | 6px | 6px |
| Corner radius (top) | 12px (CSD window corners) | 12px |

The header bar fades to the window background color when the window loses focus
(backdrop state), creating a subtle visual indicator of the active window.

## Sidebar

| Property | Light | Dark |
|----------|-------|------|
| Background | `#EBEBEB` | `#303030` |
| Backdrop | `#F2F2F2` | `#2A2A2A` |
| Separator (right edge) | `rgba(0,0,0,0.15)` | `rgba(255,255,255,0.15)` |
| Width (default) | 25% of window | 25% of window |
| Width (min) | 180px | 180px |
| Width (max) | 280px | 280px |

The sidebar uses the same background color as the header bar, creating a visual
connection between the two.

## Cards

Cards are the primary content grouping mechanism in Adwaita.

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FFFFFF` | `#383838` |
| Border | `rgba(0,0,0,0.12)` 1px | `rgba(255,255,255,0.10)` 1px |
| Corner radius | 12px | 12px |
| Shadow | (0, 1) blur 3, black @ 0.06 | (0, 1) blur 3, black @ 0.06 |
| Content padding | 12px | 12px |

### Card Variants

| Style Class | Behavior |
|-------------|----------|
| `.card` | Default card with border, shadow, background |
| `.card.activatable` | Adds hover/press states (for clickable cards) |
| `.boxed-list` | Cards containing rows (no padding, rows fill edge-to-edge) |

Boxed lists are the GNOME equivalent of iOS grouped table cells: a card filled with
rows separated by 1px dividers.

## Popovers

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FFFFFF` | `#383838` |
| Border | `rgba(0,0,0,0.15)` 1px | `rgba(255,255,255,0.15)` 1px |
| Corner radius | 12px | 12px |
| Shadow | (0, 4) blur 12, black @ 0.15 | (0, 4) blur 12, black @ 0.15 |
| Arrow size | 12px | 12px |
| Padding | 6px | 6px |

## Dialogs

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FAFAFA` | `#383838` |
| Corner radius | 12px | 12px |
| Shadow | (0, 12) blur 36, black @ 0.25 | (0, 12) blur 36, black @ 0.25 |
| Max width | 480px | 480px |
| Content margin | 24px | 24px |
| Scrim (behind dialog) | black @ 0.32 | black @ 0.32 |

## View Background

The main content area uses a distinct view background:

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FFFFFF` | `#1E1E1E` |
| Used by | GtkTextView, GtkListView, GtkColumnView, GtkTreeView | — |

The view background is slightly brighter (light) or darker (dark) than the window
background, providing subtle contrast.

## Backdrop (Unfocused Window) Behavior

When a window loses focus, Adwaita reduces visual contrast:

- Header bar fades to `--headerbar-backdrop-color` (matches window bg)
- Sidebar fades to `--sidebar-backdrop-color`
- Window shadow reduces
- Overall saturation is subtly reduced

This is a purely CSS-driven effect — no translucency or blur involved.

## Comparison to iOS and macOS

| Property | GNOME/Adwaita | iOS | macOS |
|----------|--------------|-----|-------|
| Blur effects | None | Everywhere | Everywhere |
| Translucency | None | Materials | Vibrancy |
| Corner shape | Circular arcs | Superellipse | Superellipse |
| Card borders | Visible, 1px | Subtle or none | Subtle |
| Surface hierarchy | Color-based | Blur-based | Blur-based |
| Elevation model | Flat + minimal shadow | Material layers | Vibrancy layers |
| Backdrop state | Color fade | Not applicable | Desaturation |
