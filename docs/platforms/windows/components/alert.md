# Windows — ContentDialog (Alert / Dialog)

Source: WinUI 3 ContentDialog control

## Appearance

- Background: SolidBackgroundFillColorQuarternary (`#FFFFFF` / `#2C2C2C`)
- Corner radius: 8px (layerCornerRadius)
- Border: 1px SurfaceStrokeColorDefault
- Shadow: Shadow 28
- Overlay: SmokeFillColorDefault (black @ 30% light, black @ 40% dark)

## Metrics

| Property | Value |
|----------|-------|
| Max width | 548px |
| Min width | 320px |
| Padding (content area) | 24px |
| Title padding | 24px left/right, 18px top |
| Button area padding | 24px horizontal, 20px bottom, 8px top |
| Button gap | 8px |
| Corner radius | 8px |

## Structure

```
┌───────────────────────────────────┐
│ Title                             │  ← 20px Subtitle, SemiBold
│                                   │
│ Content area                      │  ← 14px Body, Regular
│ (text, custom content, inputs)    │
│                                   │
├───────────────────────────────────┤
│ [Close]  [Secondary]  [Primary]  │  ← Button row
└───────────────────────────────────┘
```

## Title

| Property | Value |
|----------|-------|
| Font | 20px Subtitle, SemiBold (600) |
| Color | TextFillColorPrimary |
| Max lines | 2 (truncated with ellipsis) |
| Bottom margin | 12px (to content) |

## Content

| Property | Value |
|----------|-------|
| Font | 14px Body, Regular (400) |
| Color | TextFillColorSecondary |
| Scrollable | Yes, if content exceeds max height |
| Max height | Adapts to window height minus title and button areas |

## Buttons

ContentDialog supports up to 3 buttons: Primary, Secondary, and Close.

| Property | Primary | Secondary | Close |
|----------|---------|-----------|-------|
| Style | AccentButtonStyle (filled accent) | DefaultButtonStyle (standard) | DefaultButtonStyle (standard) |
| Min width | 130px each | 130px each | 130px each |
| Height | 32px | 32px | 32px |
| Corner radius | 4px | 4px | 4px |
| Position | Right-most | Center | Left-most |

Buttons are laid out right-to-left: Primary on the right, then Secondary, then Close on the left. They are equally distributed across the full width.

When `DefaultButton` is set to `Primary`, the primary button receives AccentButtonStyle.

### Full-Width Buttons (Single Button)

When only one button is present, it spans the full width of the dialog.

### Stacked Layout

If the combined button width exceeds available space, buttons stack vertically with Primary on top.

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Dialog open (scale + fade) | 300ms | Decelerate |
| Dialog close (scale + fade) | 200ms | Accelerate |
| Smoke overlay fade in | 300ms | Decelerate |
| Smoke overlay fade out | 200ms | Accelerate |

Open animation: starts at ~95% scale with 0 opacity, animates to 100% scale and full opacity.
Close animation: reverse, fading to 0 opacity with slight scale down.

## Position

- Always centered in the window, both horizontally and vertically.
- Cannot be moved or dragged.
- Uses `XamlRoot` as the placement anchor (renders within the app's XAML island).

## Behavior

| Behavior | Default |
|----------|---------|
| Light dismiss | No (modal, blocks interaction) |
| Escape key | Invokes CloseButton action |
| Enter key | Invokes DefaultButton action |
| Background interaction | Blocked (smoke overlay intercepts) |
| Multiple dialogs | Only one can be shown at a time |
