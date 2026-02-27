# Android — Button (Material Design 3)

Source: m3.material.io/components/buttons/specs

## Variants

| Variant | Container | Border | Elevation | Usage |
|---------|-----------|--------|-----------|-------|
| Filled | primary | none | Level 0 (0dp) | Highest emphasis, final actions (Save, Confirm) |
| Filled tonal | secondaryContainer | none | Level 0 (0dp) | Medium-high emphasis (Next, Open) |
| Elevated | surfaceContainerLow | none | Level 1 (1dp) | Medium emphasis on patterned backgrounds |
| Outlined | transparent | outline 1dp | Level 0 (0dp) | Medium emphasis (Back, Cancel) |
| Text | transparent | none | Level 0 (0dp) | Lowest emphasis (Learn more, Skip) |

## Metrics

| Property | Value |
|----------|-------|
| Height | 40dp |
| Min width | 48dp |
| Corner radius | 20dp (full pill) |
| Horizontal padding | 24dp |
| Horizontal padding (with icon) | 16dp (start), 24dp (end) |
| Icon size | 18dp |
| Icon-label gap | 8dp |
| Label font | Label Large (Roboto Medium 500, 14sp) |

## Colors

### Filled Button

| Element | Light | Dark |
|---------|-------|------|
| Container | `#6750A4` (primary) | `#D0BCFF` (primary) |
| Label | `#FFFFFF` (onPrimary) | `#381E72` (onPrimary) |

### Filled Tonal Button

| Element | Light | Dark |
|---------|-------|------|
| Container | `#E8DEF8` (secondaryContainer) | `#4A4458` (secondaryContainer) |
| Label | `#1D192B` (onSecondaryContainer) | `#E8DEF8` (onSecondaryContainer) |

### Elevated Button

| Element | Light | Dark |
|---------|-------|------|
| Container | `#F7F2FA` (surfaceContainerLow) | `#1D1B20` (surfaceContainerLow) |
| Label | `#6750A4` (primary) | `#D0BCFF` (primary) |
| Shadow | Level 1 (1dp) | Level 1 (1dp) |

### Outlined Button

| Element | Light | Dark |
|---------|-------|------|
| Container | transparent | transparent |
| Border | `#79747E` (outline) | `#938F99` (outline) |
| Label | `#6750A4` (primary) | `#D0BCFF` (primary) |

### Text Button

| Element | Light | Dark |
|---------|-------|------|
| Container | transparent | transparent |
| Label | `#6750A4` (primary) | `#D0BCFF` (primary) |

## States

State layer uses the label/content color at varying opacity:

| State | Container effect | Label effect |
|-------|-----------------|-------------|
| Enabled | Default | Default |
| Hovered | + state layer 8% | Default |
| Focused | + state layer 10% | Default |
| Pressed | + state layer 10% + ripple | Default |
| Disabled | onSurface @ 12% | onSurface @ 38% |

### Elevated button states

| State | Elevation |
|-------|-----------|
| Enabled | Level 1 (1dp) |
| Hovered | Level 2 (3dp) |
| Focused | Level 1 (1dp) |
| Pressed | Level 1 (1dp) |
| Disabled | Level 0 (0dp) |

## Icon Buttons

Separate from common buttons. Four variants: standard, filled, filled tonal, outlined.

| Property | Value |
|----------|-------|
| Container size | 40dp x 40dp |
| Icon size | 24dp |
| Corner radius | 20dp (full) |
| Touch target | 48dp x 48dp |
