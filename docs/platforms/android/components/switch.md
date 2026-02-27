# Android — Switch (Material Design 3)

Source: m3.material.io/components/switch/specs

## Track

| Property | Value |
|----------|-------|
| Width | 52dp |
| Height | 32dp |
| Corner radius | 16dp (full pill) |

### Track Colors

| State | Light | Dark |
|-------|-------|------|
| Off | `#E7E0EC` (surfaceContainerHighest) | `#36343B` |
| Off (border) | `#79747E` (outline) | `#938F99` |
| On | `#6750A4` (primary) | `#D0BCFF` |
| Disabled off | `#E7E0EC` @ 12% | `#E6E0E9` @ 12% |
| Disabled on | `#1D1B20` @ 12% | `#E6E0E9` @ 12% |

Off track has a 2dp border (outline color). On track has no border.

## Thumb

| Property | Off | On | Pressed |
|----------|-----|-----|---------|
| Diameter | 16dp | 24dp | 28dp |
| Shape | Circle | Circle | Circle |

### Thumb Colors

| State | Light | Dark |
|-------|-------|------|
| Off | `#79747E` (outline) | `#938F99` |
| On | `#FFFFFF` (onPrimary) | `#381E72` (onPrimary) |
| Disabled off | `#1D1B20` @ 38% | `#E6E0E9` @ 38% |
| Disabled on | `#FFFFFF` | `#322F35` |

## Thumb Icon

M3 switch supports an optional icon inside the thumb:

| State | Icon | Size |
|-------|------|------|
| Off (with icon) | Close (X) | 16dp |
| On (with icon) | Check | 16dp |

When icons are shown, the off-state thumb is 24dp (not 16dp) to accommodate the icon.

Icon colors:
- Off icon: `#E7E0EC` (surfaceContainerHighest)
- On icon: `#6750A4` (onPrimaryContainer)

## States

| State | Effect |
|-------|--------|
| Hovered | State layer 8% on thumb |
| Focused | State layer 10% on thumb |
| Pressed | Thumb grows to 28dp, state layer 10% |
| Disabled | Track and thumb at reduced opacity |

State layer is rendered as a 40dp circle centered on the thumb.

## Animation

- Thumb slide: Medium 1 (250ms), Standard easing
- Thumb size change: Short 4 (200ms), Standard easing
- Color transition: Short 4 (200ms)

## Metrics Summary

```
[  Track 52x32dp, radius 16dp                    ]
[  +---------+                    +---------+     ]
[  | thumb   |      OFF           | thumb   | ON  ]
[  | 16dp    |                    | 24dp    |     ]
[  +---------+                    +---------+     ]
```

Touch target: 48dp minimum height.
