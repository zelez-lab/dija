# iOS — Slider (UISlider)

Source: UISlider, SwiftUI Slider

## Track

| Property | Value |
|----------|-------|
| Height | 4pt (visual), 44pt (hit area) |
| Corner radius | 2pt (fully rounded) |
| Minimum track color | tintColor (systemBlue by default) |
| Maximum track color | systemFill (`#787880` @ 0.20 light / @ 0.36 dark) |
| Total width | Fills available horizontal space |

## Thumb

| Property | Value |
|----------|-------|
| Size | 28pt diameter |
| Color | white (`#FFFFFF`) |
| Shadow 1 | offset(0, 0.5) blur 4, black @ 0.12 |
| Shadow 2 | offset(0, 0.5) blur 1, black @ 0.04 |
| Corner radius | 14pt (fully circular) |
| Hit area | 44 x 44pt (padded beyond visual) |

## Custom Min/Max Images

| Property | Value |
|----------|-------|
| Position | Left of min track / right of max track |
| Size | 20pt (typically) |
| Color | secondaryLabel |
| Spacing from track | 8pt |

## States

| State | Track | Thumb | Notes |
|-------|-------|-------|-------|
| Normal | Standard colors | White circle, shadows | |
| Dragging | Standard colors | White circle, shadows, tracks finger | No visual change on thumb during drag |
| Disabled | Alpha 0.3 | Alpha 0.3 | Entire slider dimmed |

## Animation

| Property | Value |
|----------|-------|
| Value change (programmatic) | 0.15s ease-in-out (when `animated: true`) |
| Thumb snap (to stepped values) | 0.1s ease-out |
| Track fill | Follows thumb position in real-time (no animation lag) |

## Stepped Slider

When using discrete steps (SwiftUI `Slider(value:in:step:)`):

| Property | Value |
|----------|-------|
| Tick marks | Not visible by default (no built-in tick UI) |
| Snap behavior | Thumb snaps to nearest step on release |
| Haptic feedback | Light impact at each step boundary |

## Continuous vs. Discrete

| Mode | Behavior |
|------|----------|
| Continuous | Value updates in real-time as thumb moves |
| Discrete (with step) | Value snaps to nearest step on release |

## Metrics (Summary)

```
     ┌── min image (optional)
     │
     ▼        min track (tintColor)    max track (gray)
    [◀]  ━━━━━━━━━━━━━━━━━━━━○━━━━━━━━━━━━━━━━━━  [▶]
                              ↑                        ↑
                           thumb (28pt)          max image (optional)
         ◄──────────── track (4pt height) ──────────►
```

## Accessibility

| Property | Value |
|----------|-------|
| Role | Slider (adjustable) |
| VoiceOver | "[Label], [value]%, adjustable" |
| Increment/decrement | ~10% of range per swipe up/down |
| Custom step | Respects step value if set |
