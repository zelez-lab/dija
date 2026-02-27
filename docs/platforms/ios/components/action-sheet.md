# iOS — Action Sheet (UIAlertController, style: .actionSheet)

Source: UIAlertController (style: .actionSheet), SwiftUI confirmationDialog

## iPhone Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | Ultra-thick material | Ultra-thick material |
| Corner radius | 14pt | 14pt |
| Corner curve | `.continuous` (superellipse) | |
| Position | Bottom of screen, above safe area | |
| Width | Screen width - 16pt (8pt margin each side) | |
| Safe area bottom margin | 8pt above home indicator | |

## Layout

Action sheets on iPhone consist of two separate rounded cards:

```
┌─────────────────────────────┐
│       Header (optional)      │  ← Title + message
├─────────────────────────────┤
│         Action 1             │  ← 57pt per action
├─────────────────────────────┤
│         Action 2             │
├─────────────────────────────┤
│    Destructive Action        │  ← systemRed text
└─────────────────────────────┘
        8pt gap
┌─────────────────────────────┐
│          Cancel              │  ← separate card
└─────────────────────────────┘
```

## Dimensions

| Element | Value |
|---------|-------|
| Action button height | 57pt |
| Header padding (top/bottom) | 14pt |
| Header padding (horizontal) | 16pt |
| Separator | 0.33pt, separator color |
| Gap between action group and cancel | 8pt |
| Cancel button height | 57pt |
| Side margins | 8pt (each side) |

## Typography

| Element | Font | Size | Weight | Color | Alignment |
|---------|------|------|--------|-------|-----------|
| Title | SF Pro | 13pt | Semibold | secondaryLabel | Centered |
| Message | SF Pro | 13pt | Regular | secondaryLabel | Centered |
| Regular action | SF Pro | 20pt | Regular | tintColor (systemBlue) | Centered |
| Destructive action | SF Pro | 20pt | Regular | systemRed | Centered |
| Cancel | SF Pro | 20pt | Semibold | tintColor | Centered |

Note: The title and message in action sheets use a smaller 13pt size compared to alerts (17pt title).

## Button States

| State | Effect |
|-------|--------|
| Pressed | Background highlight (systemGray4 fill) |
| Disabled | Text alpha 0.3 |

## iPad Presentation

On iPad, action sheets appear as popovers, not bottom sheets.

| Property | Value |
|----------|-------|
| Style | Popover (arrow pointing to source) |
| Width | ~320pt (content-dependent) |
| Corner radius | 14pt |
| Arrow size | 13pt height |
| Shadow | offset(0, 10) blur 40, black @ 0.25 |
| Background | Ultra-thick material |
| No cancel button | Dismiss by tapping outside |
| No dimming | Background remains interactive |

## Dimming Backdrop (iPhone)

| Property | Value |
|----------|-------|
| Overlay | black @ 0.4 |
| Tap to dismiss | Tapping backdrop triggers cancel |
| Animation | Fade in/out with sheet |

## Animation

### Present (iPhone)

| Property | Value |
|----------|-------|
| Duration | 0.3s |
| Curve | Spring (damping ~0.85) |
| Direction | Slides up from bottom |
| Backdrop | Fades in simultaneously |
| Cancel card | Appears with main card (no stagger) |

### Dismiss (iPhone)

| Property | Value |
|----------|-------|
| Duration | 0.25s |
| Curve | ease-in |
| Direction | Slides down to bottom |
| Backdrop | Fades out simultaneously |

### Present (iPad Popover)

| Property | Value |
|----------|-------|
| Duration | 0.25s |
| Curve | ease-out |
| Scale | Start at 0.9, animate to 1.0 |
| Opacity | Fade in |

## Interactive Dismissal

| Property | Value |
|----------|-------|
| Gesture | Swipe down on action sheet |
| Threshold | ~50pt or 50% velocity |
| Snap back | Spring if released above threshold |
| Dismiss | Animates down if below threshold |

## Accessibility

| Property | Value |
|----------|-------|
| VoiceOver | "Action sheet, [title], [message]" |
| Focus | First action |
| Escape gesture | Triggers cancel |
| Actions | Each announced as button |
