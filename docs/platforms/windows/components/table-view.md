# Windows — ListView / DataGrid

Source: WinUI 3 ListView, GridView, ItemsView

## ListView (Standard List)

### Item Metrics

| Property | Value |
|----------|-------|
| Item height (single-line) | 40px |
| Item height (two-line) | 60px |
| Item height (three-line) | 72px |
| Item padding (horizontal) | 12px |
| Item padding (vertical) | 8px |
| Item corner radius | 4px (controlCornerRadius) |
| Item margin (between items) | 2px vertical |
| Icon size (leading) | 16x16px or 20x20px |
| Icon-to-text gap | 12px |
| Font (primary text) | 14px, Regular |
| Font (secondary text) | 12px Caption, Regular |
| Secondary text color | TextFillColorSecondary |

### Item States

| State | Background | Text | Indicator |
|-------|-----------|------|-----------|
| Rest | Transparent | TextFillColorPrimary | None |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary | None |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary | None |
| Selected | SubtleFillColorSecondary | TextFillColorPrimary | 3px accent pill (left edge) |
| Selected + Hover | SubtleFillColorTertiary | TextFillColorPrimary | 3px accent pill |
| Disabled | Transparent | TextFillColorDisabled | None |

### Selection Indicator

When an item is selected, a **3px wide, 16px tall accent-colored pill** appears on the left edge of the item (vertically centered). This is the primary selection indicator.

| Property | Value |
|----------|-------|
| Width | 3px |
| Height | 16px |
| Corner radius | 1.5px (fully rounded) |
| Color | AccentFillColorDefault |
| Position | Left edge, vertically centered |

### Group Header

| Property | Value |
|----------|-------|
| Font | 14px, SemiBold |
| Padding | 8px vertical, 12px horizontal |
| Separator | 1px DividerStrokeColorDefault below header |

## GridView (Grid Layout)

Same as ListView but items are arranged in a wrapping grid.

| Property | Value |
|----------|-------|
| Item size | Configurable (typical: 100x100px, 200x200px) |
| Item corner radius | 4px |
| Item gap | 4px |
| Selection check | Rounded checkbox in top-right corner |

## DataGrid (Table with Columns)

WinUI 3 does not ship a built-in DataGrid. Community implementations follow these conventions:

### Column Header

| Property | Value |
|----------|-------|
| Height | 32px |
| Padding | 12px horizontal |
| Font | 12px Caption, Regular |
| Color | TextFillColorSecondary |
| Background | Transparent |
| Sort indicator | Chevron glyph, 8px |
| Separator | 1px DividerStrokeColorDefault between columns |
| Resize handle | 1px wide, full height, on hover shows resize cursor |

### Data Row

| Property | Value |
|----------|-------|
| Height | 40px (standard), 32px (compact) |
| Padding | 12px horizontal per cell |
| Font | 14px, Regular |
| Hover | SubtleFillColorSecondary (full row) |
| Selected | SubtleFillColorSecondary + left accent pill |
| Alternating rows | Optional, uses SubtleFillColorSecondary for even rows |
| Row separator | 1px DividerStrokeColorDefault |

### Scrollbar

| Property | Value |
|----------|-------|
| Width (collapsed) | 2px |
| Width (expanded, on hover) | 6px |
| Corner radius | Fully rounded |
| Thumb color | ControlStrongFillColorDefault |
| Track color | Transparent |
| Hover: thumb color | ControlStrongFillColorDefault (increased opacity) |

## Empty State

| Property | Value |
|----------|-------|
| Illustration | Optional, centered |
| Message | 14px Body, TextFillColorSecondary, centered |
| Action button | Optional, Accent style |

## Swipe Actions

WinUI 3 SwipeControl can be added to list items:

| Property | Value |
|----------|-------|
| Action background | Configurable (e.g., SystemFillColorCritical for delete) |
| Action icon | 20x20px, white |
| Action text | 12px, white |
| Swipe threshold | 64px to reveal, 128px to execute |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Item hover fill | 100ms | Control fast |
| Selection indicator appear | 150ms | Decelerate |
| Selection indicator disappear | 100ms | Accelerate |
| Reorder (drag) | 200ms | Decelerate |
| Add item (entrance) | 200ms | Decelerate |
| Remove item (exit) | 150ms | Accelerate |
| Scrollbar expand | 150ms | Decelerate |
| Scrollbar collapse | 300ms | Accelerate |
