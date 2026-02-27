# Windows — ProgressBar and ProgressRing

Source: WinUI 3 ProgressBar, ProgressRing controls

## ProgressBar (Linear)

### Track Metrics

| Property | Value |
|----------|-------|
| Height | 3px (default), 1px (indeterminate track portion) |
| Corner radius | 1.5px (fully rounded) |
| Track color (unfilled) | ControlStrongFillColorDefault (`#72000000` / `#9AFFFFFF`) |
| Fill color | AccentFillColorDefault (SystemAccentColor) |
| Width | Fills available horizontal space |

### Determinate Mode

A solid fill bar that advances from left to right based on `Value` (0-100).

| Property | Value |
|----------|-------|
| Fill height | 3px |
| Fill corner radius | 1.5px |
| Fill color | AccentFillColorDefault |

### Indeterminate Mode

An animated looping pattern where a short accent bar slides back and forth across the track.

| Property | Value |
|----------|-------|
| Track height | 1px |
| Moving bar height | 3px |
| Moving bar width | ~33% of total width |
| Animation duration | 2000ms per cycle |
| Animation curve | Ease (cubic-bezier(0.8, 0, 0.2, 1)) |

The indeterminate animation: the accent bar starts from the left, accelerates to the right, decelerates, then reverses. It creates a smooth oscillating motion.

### Paused State

| Property | Value |
|----------|-------|
| Fill color | SystemFillColorCaution (`#9D5D00` / `#FCE100`) |
| Animation | Stopped (bar freezes in place) |

### Error State

| Property | Value |
|----------|-------|
| Fill color | SystemFillColorCritical (`#C42B1C` / `#FF99A4`) |
| Animation | Stopped |

## ProgressRing (Circular)

### Ring Metrics

| Property | Value |
|----------|-------|
| Default diameter | 32x32px |
| Min diameter | 20x20px (cannot go smaller) |
| Max diameter | Unlimited (scales with container) |
| Stroke width | 3px (scales proportionally) |
| Track color | ControlStrongFillColorDefault |
| Fill color | AccentFillColorDefault |

### Determinate Mode

A circular arc that sweeps clockwise from the top (12 o'clock position).

| Property | Value |
|----------|-------|
| Start angle | 270 degrees (top/12 o'clock) |
| Sweep direction | Clockwise |
| Background ring | Full circle, track color |
| Fill arc | Partial circle, accent color |

### Indeterminate Mode

A rotating partial arc that continuously spins.

| Property | Value |
|----------|-------|
| Arc length | ~90 degrees (varies during animation) |
| Rotation speed | ~3000ms per revolution |
| Arc expansion/contraction | The arc length grows and shrinks as it rotates |
| Animation curve | Ease-in-out for arc length, Linear for rotation |

The indeterminate ring animation combines:
1. Continuous clockwise rotation (linear, 3s cycle)
2. Arc length oscillation: sweeps between ~30 degrees and ~270 degrees (ease-in-out)

### Paused and Error States

Same color mapping as ProgressBar (caution yellow for paused, critical red for error).

## Sizing Behavior

| Container | ProgressBar | ProgressRing |
|-----------|-------------|-------------|
| No explicit size | Fills width, 3px height | 32x32px default |
| Explicit width/height | Stretches to fill | Uses smaller of w/h |
| Min constraint | No width minimum | 20x20px minimum |

## Custom Foreground

Both controls accept a `Foreground` property to override the accent color for the fill.

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| ProgressBar value change | 200ms | Ease |
| ProgressBar indeterminate cycle | 2000ms | Ease |
| ProgressRing value change | 200ms | Ease |
| ProgressRing indeterminate spin | 3000ms | Linear (rotation) |
| ProgressRing arc oscillation | 1500ms | Ease-in-out |
| State change (normal → paused/error) | 200ms | Control fast |
