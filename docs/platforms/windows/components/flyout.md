# Windows — Flyout / MenuFlyout

Source: WinUI 3 Flyout, MenuFlyout, MenuBar controls

## Flyout (Generic Popup)

A light-dismiss popup anchored to a control, containing arbitrary content.

### Metrics

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Padding | 16px |
| Border | 1px SurfaceStrokeColorFlyout |
| Shadow | Shadow 8 |
| Max width | 456px |
| Min width | 96px |

### Placement

| Mode | Description |
|------|------------|
| Top | Above the target, centered |
| Bottom | Below the target, centered |
| Left | Left of target, vertically centered |
| Right | Right of target, vertically centered |
| Full | Centered in window |
| Auto | System chooses best placement |

Default placement: `Top`. Flyout repositions automatically to stay within window bounds.

### Arrow gap

8px between the flyout surface and the anchor element.

## MenuFlyout (Context Menu)

A popup containing a list of selectable menu items, typically shown on right-click or via a menu button.

### Container Metrics

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Padding | 4px vertical, 0px horizontal |
| Border | 1px SurfaceStrokeColorFlyout |
| Shadow | Shadow 8 |
| Min width | 128px |
| Max width | 456px |
| Max height | 480px (scrollable) |

### MenuFlyoutItem

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px left, 12px right |
| Corner radius | 4px (with 2px horizontal margin) |
| Font | 14px, Regular |
| Icon size | 16x16px |
| Icon-to-text gap | 12px |
| Keyboard accelerator text | 12px, TextFillColorSecondary, right-aligned |
| Checkmark width | 16px (when applicable) |

### MenuFlyoutItem States

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |
| Disabled | Transparent | TextFillColorDisabled |

### MenuFlyoutSeparator

| Property | Value |
|----------|-------|
| Height | 1px |
| Color | DividerStrokeColorDefault |
| Margin | 4px vertical, 0px horizontal |

### MenuFlyoutSubItem (Submenu)

| Property | Value |
|----------|-------|
| Chevron icon | `&#xE76C;` (right arrow), 12x12px, right-aligned |
| Submenu offset | Overlaps parent by 4px horizontally |
| Submenu open delay | 200ms (hover) |
| Submenu close delay | 150ms (mouse exit) |

### Menu Structure

```
┌───────────────────────────────┐
│ [✓] Menu item with checkmark  │
│ [🔘] Radio menu item          │
│     Menu item (no icon)       │
│ ───────────────────────────── │
│ [📋] Paste             Ctrl+V │
│ [📂] Open submenu        ▶   │
│ ───────────────────────────── │
│     Disabled item             │
└───────────────────────────────┘
```

## MenuBar

A horizontal bar of top-level menus (File, Edit, View, etc.).

### Bar Metrics

| Property | Value |
|----------|-------|
| Height | 32px |
| Background | Transparent |
| Item padding | 12px horizontal |
| Item font | 14px, Regular |

### MenuBarItem States

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Open (menu visible) | SubtleFillColorTertiary | TextFillColorPrimary |

## ToggleMenuFlyoutItem

Same as MenuFlyoutItem with a checkmark indicator:

| Property | Value |
|----------|-------|
| Checkmark icon | `&#xE73E;`, 16x16px, AccentColor |
| Checkmark position | Left, replacing the icon area |
| Unchecked | No checkmark, icon area empty |

## RadioMenuFlyoutItem

Same as ToggleMenuFlyoutItem but with a radio bullet:

| Property | Value |
|----------|-------|
| Bullet | 8px filled circle, AccentColor |
| Bullet position | Left, centered in 16px icon area |

## Behavior

| Behavior | Flyout | MenuFlyout |
|----------|--------|-----------|
| Light dismiss | Yes (click outside closes) | Yes |
| Escape key | Closes | Closes current level |
| Arrow keys | N/A | Navigate items |
| Enter | N/A | Activate item |
| Right arrow | N/A | Open submenu |
| Left arrow | N/A | Close submenu |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Flyout open (scale + fade) | 200ms | Decelerate |
| Flyout close (fade) | 150ms | Accelerate |
| Menu item hover fill | 100ms | Control fast |
| Submenu open | 200ms | Decelerate |
| Submenu close | 150ms | Accelerate |
