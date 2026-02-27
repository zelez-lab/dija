# Android — Segmented Button (Material Design 3)

Source: m3.material.io/components/segmented-buttons/specs

M3 equivalent of iOS segmented control. Two density modes: single-select
and multi-select.

## Variants

| Variant | Behavior | Usage |
|---------|----------|-------|
| Single-select | Radio-like, one active at a time | View switcher, sort order |
| Multi-select | Checkbox-like, multiple active | Filter tags |

## Metrics

| Property | Value |
|----------|-------|
| Height | 40dp |
| Min segment width | 48dp |
| Corner radius (outer) | 20dp (full pill) |
| Corner radius (inner dividers) | 0dp |
| Border width | 1dp |
| Icon size | 18dp |
| Icon-label gap | 8dp |
| Horizontal padding | 12dp |
| Label font | Label Large (Roboto Medium 500, 14sp) |
| Touch target | 48dp min height |

Segments are equal width, dividing the total width evenly. The outer shape
is a continuous pill (20dp radius on first and last segment).

## Colors

### Selected Segment

| Element | Light | Dark |
|---------|-------|------|
| Container | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Label/icon | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |
| Check icon | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |

### Unselected Segment

| Element | Light | Dark |
|---------|-------|------|
| Container | transparent | transparent |
| Border | `#79747E` (outline) | `#938F99` |
| Label/icon | `#1D1B20` (onSurface) | `#E6E0E9` |

### Disabled

| Element | Value |
|---------|-------|
| Container | transparent |
| Border | onSurface @ 12% |
| Label/icon | onSurface @ 38% |

## States

| State | Effect |
|-------|--------|
| Hovered | State layer 8% (onSecondaryContainer if selected, onSurface if not) |
| Focused | State layer 10% |
| Pressed | State layer 10% + ripple |
| Disabled | Reduced opacity (container 12%, content 38%) |

## Selection Animation

When a segment is selected:
1. Check icon (18dp) fades in and slides from left (Short 4, 200ms)
2. Container fills with secondaryContainer color
3. If a label-only segment, check icon appears before the label, pushing it right

## Layout

```
+--[Segment A]--+--[Segment B]--+--[Segment C]--+
|  [x] Label A  |    Label B    |    Label C    |
+----------------+----------------+----------------+
     selected         unselected      unselected
```

Dividers between segments: 1dp, outline color. Dividers adjacent to
a selected segment are hidden (the selected container fills the space).
