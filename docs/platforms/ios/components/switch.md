# iOS — Switch (UISwitch / Toggle)

Source: UISwitch, SwiftUI Toggle

## Overall Size

| Property | Value |
|----------|-------|
| Width | 51pt |
| Height | 31pt |
| Corner radius | 15.5pt (fully rounded pill) |

## Track

| Property | Off (Light) | Off (Dark) | On |
|----------|-------------|------------|-----|
| Background | `#E9E9EB` (systemGray4-like) | `#39393D` | systemGreen (`#34C759` / `#30D158`) |
| Border | 0.5pt `#E0E0E0` (light) | none | none |
| Interior padding | 2pt (space between track edge and thumb) | — | — |

The track uses `systemFill` as the base off-state color in some contexts, but the visible result is close to the values above.

## Thumb

| Property | Value |
|----------|-------|
| Size (normal) | 27pt diameter |
| Size (pressed) | 27pt height x 31pt width (stretches horizontally) |
| Color | white (`#FFFFFF`) |
| Shadow | offset(0, 3) blur 8 spread 0, black @ 0.15 |
| Secondary shadow | offset(0, 3) blur 1 spread 0, black @ 0.06 |
| Corner radius | 13.5pt (fully rounded) |

## Animation

| Property | Value |
|----------|-------|
| Toggle duration | ~0.25s |
| Curve | Spring (damping 0.75, response 0.3) |
| Thumb expansion (press) | Grows to 31pt width in ~0.15s |
| Thumb expansion (release) | Shrinks back in ~0.2s |
| Track color transition | Cross-fade over ~0.15s |

### Animation Sequence (Off -> On)

1. User touches: thumb expands width to 31pt (0.15s spring)
2. User releases (or drags past midpoint): thumb slides to right edge (0.25s spring)
3. Track cross-fades from gray to green (0.15s, starts slightly before thumb reaches end)
4. Thumb shrinks back to 27pt circle (0.2s spring)

## States

| State | Track | Thumb | Notes |
|-------|-------|-------|-------|
| Off | Gray background | Left position | |
| On | Green (or tintColor) background | Right position | |
| Pressed (off) | Gray background | Expanded, left | |
| Pressed (on) | Green background | Expanded, right | |
| Disabled (off) | Gray @ 0.5 opacity | Left, @ 0.5 opacity | Entire switch at reduced opacity |
| Disabled (on) | Green @ 0.5 opacity | Right, @ 0.5 opacity | |

## Custom Colors

| Property | Configurable |
|----------|-------------|
| `onTintColor` | Track color when on (default: systemGreen) |
| `thumbTintColor` | Thumb color (default: white) |
| `backgroundColor` (track off) | Track color when off (default: system gray) |

## Accessibility

| Property | Value |
|----------|-------|
| Role | Switch |
| Minimum hit target | 51 x 31pt (already meets 44pt minimum on width, padded vertically) |
| VoiceOver | "Switch button, [label], [on/off]" |
| Haptic feedback | Light impact on toggle |

## SwiftUI Toggle Styles

In SwiftUI, Toggle has additional styles beyond the standard switch:

| Style | Description |
|-------|-------------|
| `.switch` | Standard UISwitch (default on iOS) |
| `.button` | Toggle as a tinted button |
| `.checkbox` | Checkbox (macOS only, not available on iOS) |
