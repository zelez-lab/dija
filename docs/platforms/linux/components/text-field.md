# Linux (GNOME/Adwaita) — Text Field (GtkEntry / GtkEditable)

## Appearance

GtkEntry in Adwaita is a flat-bottomed input with a subtle border that highlights
on focus with the accent color.

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FFFFFF` (view_bg_color) | `#1E1E1E` (view_bg_color) |
| Text color | `#2E3436` | `#FFFFFF` |
| Placeholder color | `rgba(46,52,54, 0.50)` | `rgba(255,255,255, 0.50)` |
| Border (rest) | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Border (focused) | 2px `--accent-color` | 2px `--accent-color` |
| Border (error) | 2px `--error-color` (`#C01C28`) | 2px `--error-color` |
| Corner radius | 6px | 6px |
| Shadow | none | none |

## Metrics

| Property | Value |
|----------|-------|
| Min height | 34px |
| Horizontal padding | 12px |
| Vertical padding | 8px |
| Corner radius | 6px |
| Font | Adwaita Sans Regular, 15px |
| Caret width | 1px |
| Caret color | `--accent-color` |
| Selection bg | `--accent-bg-color` @ 0.30 |
| Selection text | foreground (unchanged) |

## States

| State | Border | Background | Notes |
|-------|--------|------------|-------|
| Rest | 1px, `rgba(0,0,0,0.15)` | view_bg_color | — |
| Hover | 1px, `rgba(0,0,0,0.25)` | view_bg_color | Slightly stronger border |
| Focused | 2px, accent_color | view_bg_color | Accent highlight |
| Error | 2px, error_color | view_bg_color | Red border |
| Disabled | 1px, `rgba(0,0,0,0.10)` | `rgba(0,0,0,0.04)` | Content opacity 0.5 |

## Entry Variants

### Default Entry (GtkEntry)

Single-line text input. Used standalone or inside other widgets.

### Password Entry (GtkPasswordEntry)

| Property | Value |
|----------|-------|
| Input masking | Bullet characters |
| Peek button | Eye icon suffix, 16x16px |
| Caps lock indicator | Warning icon suffix |

### Search Entry (GtkSearchEntry)

| Property | Value |
|----------|-------|
| Prefix icon | Search (magnifying glass), 16x16px |
| Clear button | X icon suffix, appears when text is present |
| Placeholder | "Search..." |

### Editable Row (AdwEntryRow)

Used inside boxed lists. Label floats above input on focus/content.

| Property | Value |
|----------|-------|
| Label position (empty, unfocused) | Inside field, placeholder-style |
| Label position (focused/has content) | Floated above, `.caption` size (13px) |
| Label color (floating) | `--accent-color` when focused |
| Row min-height | 50px (taller to accommodate floating label) |
| Horizontal padding | 12px |
| Border | none (contained within boxed list card) |

### Spin Row (AdwSpinRow)

Number input with increment/decrement buttons inside a boxed list row.

| Property | Value |
|----------|-------|
| +/- button size | 34x34px |
| +/- button style | flat, icon only |
| Input alignment | right |

## Focus Behavior

| Property | Value |
|----------|-------|
| Focus ring | 2px accent-colored border (replaces default 1px border) |
| Focus transition | 200ms ease-in-out |
| Tab order | natural (follows DOM order) |
| Auto-select on focus | All text selected on Tab-focus, caret placed on click |

## Keyboard Support

| Key | Action |
|-----|--------|
| Tab | Move to next focusable |
| Shift+Tab | Move to previous focusable |
| Ctrl+A | Select all |
| Ctrl+C / Ctrl+V | Copy / paste |
| Ctrl+Z / Ctrl+Shift+Z | Undo / redo |
| Escape | Clear search (search entry) |
| Enter | Activate default action / submit |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Border color change | 200ms | ease-in-out |
| Floating label rise | 200ms | ease-out-cubic |
| Placeholder fade | 150ms | ease-in-out |
