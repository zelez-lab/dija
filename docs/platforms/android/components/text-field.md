# Android — Text Field (Material Design 3)

Source: m3.material.io/components/text-fields/specs

## Variants

| Variant | Background | Border | Usage |
|---------|-----------|--------|-------|
| Filled | surfaceContainerHighest | bottom line 1dp | Default preference, forms |
| Outlined | transparent | outline 1dp all sides | When filled conflicts with background |

## Metrics

| Property | Filled | Outlined |
|----------|--------|----------|
| Height | 56dp | 56dp |
| Corner radius (top) | 4dp | 4dp |
| Corner radius (bottom) | 0dp | 4dp |
| Horizontal padding | 16dp | 16dp |
| Top padding (to label) | 8dp | — |
| Bottom padding (to input) | 8dp | — |
| Active indicator (bottom line) | 2dp (focused) / 1dp (rest) | — |
| Outline width | — | 2dp (focused) / 1dp (rest) |
| Input font | Body Large (Roboto Regular, 16sp) |
| Label font (resting) | Body Large (Roboto Regular, 16sp) |
| Label font (floating) | Body Small (Roboto Regular, 12sp) |
| Supporting text font | Body Small (Roboto Regular, 12sp) |
| Supporting text top padding | 4dp |

## Colors

### Filled Text Field

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container | Enabled | `#E6E0E9` (surfContainerHighest) | `#36343B` |
| Active indicator | Enabled | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Active indicator | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Label | Resting | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Label | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Input text | — | `#1D1B20` (onSurface) | `#E6E0E9` |
| Placeholder | — | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Leading icon | — | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Trailing icon | — | `#49454F` (onSurfaceVariant) | `#CAC4D0` |

### Outlined Text Field

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container | Enabled | transparent | transparent |
| Outline | Enabled | `#79747E` (outline) | `#938F99` |
| Outline | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Label | Resting | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Label | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Input text | — | `#1D1B20` (onSurface) | `#E6E0E9` |

### Error State

| Element | Light | Dark |
|---------|-------|------|
| Active indicator / outline | `#B3261E` (error) | `#F2B8B5` |
| Label | `#B3261E` (error) | `#F2B8B5` |
| Supporting text | `#B3261E` (error) | `#F2B8B5` |
| Trailing icon | `#B3261E` (error) | `#F2B8B5` |

## States

| State | Visual effect |
|-------|--------------|
| Enabled | Default styling |
| Hovered | State layer 8% on container, indicator 1dp |
| Focused | Label floats, indicator 2dp, primary color |
| Error | Error color on indicator/label/supporting text |
| Disabled | Container onSurface @ 4%, content onSurface @ 38% |

## Label Animation

The label text animates between resting and floating positions:
- **Resting**: centered vertically in the field, Body Large (16sp)
- **Floating**: moved to top edge, Body Small (12sp)
- **Duration**: Medium 1 (250ms)
- **Easing**: Standard decelerate

For outlined variant, the floating label sits on the outline border with a
gap cut in the border behind it.

## Supporting and Counter Text

- Supporting text appears below the field, 4dp gap
- Character counter right-aligned below the field
- Both use Body Small (12sp)
- Error state turns supporting text to error color
