# Windows — Slider

Source: WinUI 3 Slider control

## Track

| Property | Value |
|----------|-------|
| Track height | 4px (rest), 6px (hover/interaction) |
| Corner radius | 2px (fully rounded at 4px height) |
| Filled (min side) | AccentFillColorDefault (SystemAccentColor) |
| Unfilled (max side) | ControlStrongFillColorDefault (`#72000000` / `#9AFFFFFF`) |
| Total hit area height | 32px (invisible padding above/below track) |

## Thumb (Knob)

| Property | Value |
|----------|-------|
| Outer diameter | 20px |
| Inner dot diameter | 8px (rest), 10px (hover), 14px (pressed) |
| Outer fill | White (light) / `#FFFFFF` | Dark: `#FFFFFF` |
| Inner fill | AccentFillColorDefault |
| Shadow | Shadow 2 (key: 0px 1px 1px rgba(0,0,0,0.08), ambient: 0px 0px 2px rgba(0,0,0,0.06)) |
| Border | 1px ControlStrokeColorSecondary |

The thumb uses a **two-layer design**: a white outer circle with a subtle shadow, and an accent-colored inner dot that grows/shrinks based on interaction state.

## States

| State | Track height | Filled color | Unfilled color | Thumb inner dot |
|-------|-------------|-------------|----------------|----------------|
| Rest | 4px | AccentFillColorDefault | ControlStrongFillColorDefault | 8px, AccentColor |
| Hover | 6px | AccentFillColorSecondary | ControlStrongFillColorDefault | 10px, AccentColor |
| Pressed | 6px | AccentFillColorTertiary | ControlStrongFillColorDefault | 14px, AccentColor |
| Disabled | 4px | AccentFillColorDisabled | ControlStrongFillColorDisabled | 8px, disabled gray |

## Tick Marks

Optional tick marks along the track.

| Property | Value |
|----------|-------|
| Tick width | 1px |
| Tick height | 4px |
| Tick color | ControlStrongFillColorDefault |
| Position | Centered below (horizontal) or beside (vertical) the track |
| TickFrequency | Configurable (integer step) |
| TickPlacement | None, TopLeft, BottomRight, Outside |

## Range Labels

| Property | Value |
|----------|-------|
| Min/Max value labels | Optional, 12px Caption |
| Header label | Optional, 14px Regular, positioned above |
| Current value tooltip | Appears on press, shows numeric value |

## Layout

```
Header label (optional)
─────────────●────────────  ← track with thumb
Tick marks (optional)
```

| Property | Value |
|----------|-------|
| Horizontal slider height | 32px (including hit area) |
| Vertical slider width | 32px |
| Min length | 100px |

## Step Snap

When `StepFrequency` or `SnapsTo` is set, the thumb snaps to discrete positions along the track. The snap animation uses:

| Transition | Duration | Easing |
|-----------|----------|--------|
| Snap to nearest step | 100ms | Control fast |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Track height grow (rest → hover) | 100ms | Control fast |
| Track height shrink (hover → rest) | 150ms | Decelerate |
| Thumb dot grow (rest → hover) | 100ms | Control fast |
| Thumb dot grow (hover → pressed) | 50ms | Linear |
| Thumb dot shrink (pressed → rest) | 200ms | Decelerate |
| Value tooltip appear | 100ms | Decelerate |
| Value tooltip disappear | 50ms | Accelerate |
