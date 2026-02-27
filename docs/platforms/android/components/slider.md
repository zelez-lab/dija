# Android — Slider (Material Design 3)

Source: m3.material.io/components/sliders/specs

## Variants

| Variant | Description |
|---------|------------|
| Continuous | Smooth value selection across range |
| Discrete | Snaps to predefined steps (tick marks) |
| Range | Two thumbs for min/max selection |
| Centered | Anchored at center, slides left or right |

## Metrics

| Property | Value |
|----------|-------|
| Track height (active) | 4dp |
| Track height (inactive) | 4dp |
| Track corner radius | 2dp (rounded ends) |
| Thumb diameter | 20dp |
| Thumb shape | Circle |
| Handle (outer touch area) | 44dp |
| Touch target | 48dp x 48dp |
| Tick mark size | 4dp x 4dp |
| Tick mark shape | Circle |
| Track gap (between thumb and track) | 6dp |
| Stop indicator size | 4dp x 4dp |
| Value label height | 28dp |
| Value label corner radius | 14dp (full pill) |
| Value label padding | 8dp horizontal |
| Value label font | Label Medium (Roboto Medium 500, 12sp) |

## Colors

### Track

| Element | Light | Dark |
|---------|-------|------|
| Active track | `#6750A4` (primary) | `#D0BCFF` |
| Inactive track | `#E7E0EC` (surfaceContainerHighest) | `#36343B` |
| Active tick marks | `#FFFFFF` (onPrimary) | `#381E72` |
| Inactive tick marks | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Stop indicator | `#6750A4` (primary) | `#D0BCFF` |

### Thumb

| Element | Light | Dark |
|---------|-------|------|
| Thumb | `#6750A4` (primary) | `#D0BCFF` |
| State layer (hovered) | primary @ 8% | primary @ 8% |
| State layer (focused) | primary @ 10% | primary @ 10% |
| State layer (pressed) | primary @ 10% | primary @ 10% |

### Value Label

| Element | Light | Dark |
|---------|-------|------|
| Container | `#6750A4` (primary) | `#D0BCFF` |
| Text | `#FFFFFF` (onPrimary) | `#381E72` |

### Disabled

| Element | Value |
|---------|-------|
| Active track | onSurface @ 38% |
| Inactive track | onSurface @ 12% |
| Thumb | onSurface @ 38%, with surface @ 100% inner circle |

## States

| State | Effect |
|-------|--------|
| Enabled | Default styling |
| Hovered | 40dp state layer halo around thumb |
| Focused | 40dp state layer halo around thumb |
| Pressed | 40dp state layer halo, value label appears (discrete) |
| Dragged | State layer 16% |
| Disabled | Reduced opacity track and thumb |

## Discrete Slider

- Tick marks shown on track at each step
- Value label popup appears above thumb on press/drag
- Thumb snaps to nearest tick mark on release

## Animation

- Value label enter: Short 3 (150ms), Standard decelerate
- Value label exit: Short 2 (100ms), Standard accelerate
- Snap to tick: Short 4 (200ms), Standard easing
- State layer: Short 2 (100ms)
