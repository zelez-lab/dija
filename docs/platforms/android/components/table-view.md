# Android — List Items (Material Design 3)

Source: m3.material.io/components/lists/specs

M3 equivalent of iOS table view cells. Called "Lists" in M3 vocabulary.

## Variants

| Variant | Height | Content |
|---------|--------|---------|
| One-line | 56dp | Headline only |
| Two-line | 72dp | Headline + supporting text |
| Three-line | 88dp | Headline + 2 lines supporting text |

## Metrics

| Property | Value |
|----------|-------|
| Min height (one-line) | 56dp |
| Min height (two-line) | 72dp |
| Min height (three-line) | 88dp |
| Horizontal padding (leading edge) | 16dp |
| Horizontal padding (trailing edge) | 24dp |
| Vertical padding | 8dp (top and bottom, two/three-line) |
| Leading element gap | 16dp |
| Trailing element gap | 16dp |
| Headline-supporting gap | 0dp (adjacent lines) |
| Headline font | Body Large (Roboto Regular, 16sp) |
| Supporting text font | Body Medium (Roboto Regular, 14sp) |
| Overline font | Label Small (Roboto Medium, 11sp) |
| Trailing supporting font | Label Small (Roboto Medium, 11sp) |

## Leading Element Sizes

| Element type | Size |
|-------------|------|
| Icon | 24dp x 24dp |
| Avatar (monogram) | 40dp x 40dp |
| Avatar (image) | 40dp x 40dp |
| Thumbnail | 56dp x 56dp |
| Video thumbnail | 114dp x 64dp |
| Checkbox / Radio | 18dp x 18dp |

Avatar corner radius: 20dp (full circle).
Thumbnail corner radius: 0dp (square).

## Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#FEF7FF` (surface) | `#141218` |
| Headline | `#1D1B20` (onSurface) | `#E6E0E9` |
| Supporting text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Leading icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Trailing icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Trailing text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Overline | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Divider | `#CAC4D0` (outlineVariant) | `#49454F` |

## States

| State | Effect |
|-------|--------|
| Enabled | Default |
| Hovered | State layer onSurface @ 8% |
| Focused | State layer onSurface @ 10% |
| Pressed | State layer onSurface @ 10% + ripple |
| Disabled | Headline onSurface @ 38%, no state layer |
| Selected | No built-in selected state (use checkbox/radio) |
| Dragged | State layer onSurface @ 16%, elevation Level 4 (8dp) |

## Layout Anatomy

```
+------------------------------------------------------------------+
| [Leading]  Headline text                        [Trailing]  16dp |
| 16dp gap   Supporting text                       element         |
+------------------------------------------------------------------+
```

### One-line

```
+------------------------------------------------------------------+
| [Icon 24dp]  16dp  Headline                    [Switch]    24dp  |
+------------------------------------------------------------------+
                        56dp height
```

### Two-line

```
+------------------------------------------------------------------+
|  8dp top padding                                                 |
| [Avatar 40dp] 16dp  Headline                   [Icon 24dp] 24dp |
|                      Supporting text                             |
|  8dp bottom padding                                              |
+------------------------------------------------------------------+
                        72dp height
```

### Three-line

```
+------------------------------------------------------------------+
|  8dp top padding (content top-aligned)                           |
| [Thumb 56dp]  16dp  Headline                   [Checkbox]  24dp |
|                      Supporting line 1                           |
|                      Supporting line 2                           |
|  8dp bottom padding                                              |
+------------------------------------------------------------------+
                        88dp height
```

## Dividers

- Optional 1dp divider between list items
- Full-bleed or inset (indented past leading element)
- Color: outlineVariant
- Inset padding: 16dp + leading element width + 16dp gap
