# Windows — ToolTip / TeachingTip

Source: WinUI 3 ToolTip, TeachingTip controls

## ToolTip

A lightweight popup that shows explanatory text when the user hovers over or focuses a control.

### Metrics

| Property | Value |
|----------|-------|
| Max width | 320px |
| Padding | 8px horizontal, 6px vertical |
| Corner radius | 4px (controlCornerRadius) |
| Background | SolidBackgroundFillColorSecondary (`#EEEEEE` / `#1C1C1C`) |
| Border | 1px ControlStrokeColorDefault |
| Shadow | Shadow 2 |
| Font | 12px Caption, Regular (400) |
| Text color | TextFillColorPrimary |
| Max lines | Unlimited (wraps at max width) |

### Timing

| Event | Delay |
|-------|-------|
| Show delay (initial hover) | 400ms |
| Show delay (subsequent, BetweenShowDelay) | 100ms |
| Auto-dismiss | 5000ms (configurable) |

### Placement

| Mode | Description |
|------|------------|
| Top | Above the target (default) |
| Bottom | Below the target |
| Left | Left of target |
| Right | Right of target |
| Mouse | Near mouse cursor |
| Auto | System chooses based on space |

Offset from target: 4px gap.

### States

ToolTip is non-interactive. It disappears when:
- Mouse leaves the target control
- Auto-dismiss timer expires
- Target control loses focus
- User scrolls the page

## TeachingTip

A rich, contextual popup for user education, first-run tips, and feature discovery. Can include title, message, action buttons, an image/illustration, and a close button.

### Container Metrics

| Property | Value |
|----------|-------|
| Max width | 336px |
| Min width | 320px |
| Padding | 16px |
| Corner radius | 8px (layerCornerRadius) |
| Background | SolidBackgroundFillColorSecondary |
| Border | 1px SurfaceStrokeColorDefault |
| Shadow | Shadow 16 |

### Structure

```
┌─────────────────────────────────┐
│ [🖼️ Hero image (optional)]     │  ← Full width, above content
├─────────────────────────────────┤
│ [Icon]  Title                [X]│  ← 14px SemiBold + close button
│                                 │
│ Message body text               │  ← 14px Regular, TextFillColorSecondary
│                                 │
│                    [Action] [X] │  ← Optional action button + close
└──────────▲──────────────────────┘
           │ Tail (triangle pointer)
```

### Title

| Property | Value |
|----------|-------|
| Font | 14px Body Strong, SemiBold (600) |
| Color | TextFillColorPrimary |
| Icon size | 16x16px (optional, left of title) |

### Subtitle / Message

| Property | Value |
|----------|-------|
| Font | 14px Body, Regular (400) |
| Color | TextFillColorSecondary |
| Top margin | 4px (below title) |

### Close Button

| Property | Value |
|----------|-------|
| Icon | `&#xE711;` (X glyph), 8x8px visible, 32x32px hit area |
| Position | Top-right corner |
| Style | Subtle (transparent rest, hover fill) |

### Action Button

| Property | Value |
|----------|-------|
| Style | AccentButtonStyle or DefaultButtonStyle |
| Height | 32px |
| Position | Bottom-right of content area |
| Max: 2 buttons | Action + Close (text variant) |

### Tail (Pointer Arrow)

| Property | Value |
|----------|-------|
| Width | 16px |
| Height | 8px |
| Shape | Isoceles triangle |
| Fill | Same as TeachingTip background |
| Border | 1px, same as container border |
| Shadow | None (cannot shadow non-rectangular surfaces) |
| Margin from edges | 12px minimum from container corners |
| Position | Centers on target element when possible |

### Placement Modes (Targeted)

| Mode | Description |
|------|------------|
| Top | Above target, tail points down |
| Bottom | Below target, tail points up |
| Left | Left of target, tail points right |
| Right | Right of target, tail points left |
| Center | Overlapping target center |
| TopRight, TopLeft | Offset variants |
| BottomRight, BottomLeft | Offset variants |
| LeftTop, LeftBottom | Offset variants |
| RightTop, RightBottom | Offset variants |
| Auto | System chooses based on space |

### Non-Targeted (Global) TeachingTip

When no target is specified, the TeachingTip appears at the bottom of the window without a tail.

| Property | Value |
|----------|-------|
| Position | Bottom-center of window |
| Margin from bottom | 16px |
| Tail | Hidden |
| Width | Up to 336px, centered |

### Hero Image

| Property | Value |
|----------|-------|
| Position | Top of TeachingTip (above title) |
| Width | Full width (minus border) |
| Max height | 200px |
| Corner radius | Inherits top corners from container (8px top-left, 8px top-right, 0 bottom) |

## Behavior

| Behavior | ToolTip | TeachingTip |
|----------|---------|-------------|
| Trigger | Hover / focus | Programmatic (IsOpen) |
| Light dismiss | N/A (auto-dismiss) | Yes (click outside closes) |
| Escape key | N/A | Closes |
| Interactive content | No | Yes (buttons, links) |
| Persist on hover | No | Yes (stays while interacting) |
| Preferred placement | Top | Auto |
| Multiple visible | No (one at a time) | No (one at a time) |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| ToolTip fade in | 100ms | Decelerate |
| ToolTip fade out | 50ms | Accelerate |
| TeachingTip open (scale + fade) | 300ms | Decelerate |
| TeachingTip close (fade) | 200ms | Accelerate |
| TeachingTip tail appear | Matches container | — |
