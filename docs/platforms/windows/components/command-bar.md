# Windows — CommandBar / CommandBarFlyout

Source: WinUI 3 CommandBar, CommandBarFlyout controls

## CommandBar (Toolbar)

A horizontal bar containing AppBarButton commands with icon + optional label.

### Bar Metrics

| Property | Value |
|----------|-------|
| Height (open, labels visible) | 60px |
| Height (compact, icons only) | 48px |
| Background | Transparent (inherits parent, typically Mica) |
| Padding | 8px horizontal |
| Corner radius | None (spans full width) |

### AppBarButton

| Property | Value |
|----------|-------|
| Width | 48px (compact), variable (open with label) |
| Height | 48px (compact), 60px (open) |
| Icon size | 20x20px |
| Label font | 10px Caption, Regular |
| Label position | Below icon (when labels visible) |
| Corner radius | 4px |
| Background (rest) | Transparent |
| Background (hover) | SubtleFillColorSecondary |
| Background (pressed) | SubtleFillColorTertiary |

### AppBarToggleButton

Same metrics as AppBarButton. When toggled on:

| State | Background |
|-------|-----------|
| Toggled rest | SubtleFillColorSecondary |
| Toggled hover | SubtleFillColorTertiary |
| Toggled pressed | SubtleFillColorSecondary |

### AppBarSeparator

| Property | Value |
|----------|-------|
| Width | 1px |
| Height | 20px (centered vertically) |
| Color | DividerStrokeColorDefault |
| Margin | 8px horizontal |

### Overflow (More) Button

| Property | Value |
|----------|-------|
| Icon | `&#xE10C;` (ellipsis / "...") |
| Size | 48x48px (same as AppBarButton) |
| Position | Right end of command bar |

### Overflow Menu

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Padding | 4px vertical |
| Shadow | Shadow 8 |
| Border | 1px SurfaceStrokeColorFlyout |
| Item height | 40px |
| Item icon size | 16x16px (note: smaller than primary area) |
| Item font | 14px, Regular |
| Item padding | 12px horizontal |
| Max height | 480px (scrollable) |

## CommandBarFlyout

A floating command bar that appears contextually (e.g., on text selection or right-click). Consists of a primary row of icon buttons and an optional secondary menu.

### Flyout Metrics

| Property | Value |
|----------|-------|
| Primary row height | 40px |
| Primary button width | 40px |
| Primary button icon size | 16x16px |
| Corner radius | 8px (layerCornerRadius) |
| Background | Acrylic (Background type) |
| Shadow | Shadow 8 |
| Border | 1px SurfaceStrokeColorFlyout |
| Padding | 4px |

### Primary vs Secondary

```
┌──────────────────────────────────┐
│ [B] [I] [U] [🔗] [...] │  ← Primary commands (icon-only, 40px)
├──────────────────────────────────┤
│ Cut                     Ctrl+X   │  ← Secondary commands (menu items)
│ Copy                    Ctrl+C   │
│ Paste                   Ctrl+V   │
│ ─────────────────────────────── │
│ Select All              Ctrl+A   │
└──────────────────────────────────┘
```

### Secondary Menu Item

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px horizontal |
| Font | 14px, Regular |
| Icon size | 16x16px |
| Keyboard accelerator | 12px, TextFillColorSecondary, right-aligned |
| Icon-to-text gap | 12px |
| Separator | 1px DividerStrokeColorDefault, 4px vertical padding |

## States (Both)

### AppBarButton / CommandBarFlyout Button States

| State | Background | Icon color |
|-------|-----------|-----------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |
| Disabled | Transparent | TextFillColorDisabled |

## Placement

| CommandBar | Position |
|-----------|----------|
| Top of page | Full width, below title bar |
| Bottom of page | Full width, above bottom edge |
| CommandBarFlyout | Anchored near selection or right-click point |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| CommandBarFlyout open | 200ms | Decelerate |
| CommandBarFlyout close | 150ms | Accelerate |
| Overflow menu expand | 200ms | Decelerate |
| Overflow menu collapse | 150ms | Accelerate |
| Button hover fill | 100ms | Control fast |
