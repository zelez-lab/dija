# Android — Navigation Bar (Material Design 3)

Source: m3.material.io/components/navigation-bar/specs

Bottom navigation bar for primary destinations (3-5 items).

## Metrics

| Property | Value |
|----------|-------|
| Height | 80dp |
| Elevation | Level 2 (3dp) |
| Surface | surfaceContainer |
| Icon size | 24dp |
| Active indicator width | 64dp |
| Active indicator height | 32dp |
| Active indicator corner radius | 16dp (full pill) |
| Label font (active) | Label Medium (Roboto Medium 500, 12sp) |
| Label font (inactive) | Label Medium (Roboto Medium 500, 12sp) |
| Icon-to-label gap | 4dp |
| Min item width | 48dp |
| Max item width | 80dp |
| Item padding (horizontal) | 0dp (items equally spaced) |
| Top padding (to icon) | 12dp |
| Bottom padding (to label) | 16dp |

## Active Indicator

The active indicator is a pill shape that appears behind the selected icon:

| Property | Value |
|----------|-------|
| Width | 64dp |
| Height | 32dp |
| Corner radius | 16dp |
| Color | secondaryContainer |

## Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#F3EDF7` (surfaceContainer) | `#211F26` |
| Active icon | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |
| Active indicator | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Active label | `#1D1B20` (onSurface) | `#E6E0E9` |
| Inactive icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Inactive label | `#49454F` (onSurfaceVariant) | `#CAC4D0` |

## States

| State | Effect |
|-------|--------|
| Hovered | State layer 8% on indicator area |
| Focused | State layer 10% on indicator area |
| Pressed | State layer 10% + ripple on indicator area |

State layer color: onSurface for inactive items, onSecondaryContainer for active.

## Animation

- Indicator scale: Short 3 (150ms), Emphasized decelerate
- Icon transition (filled/outlined): Short 2 (100ms)
- Label fade: Short 2 (100ms)
- Label Y translation: up 4dp on select, down on deselect

## Badge Position

Badges appear on the top-right of the icon:
- Small dot badge: offset (8dp, -4dp) from icon center-right
- Large number badge: offset (4dp, -4dp)
- Badge must not overlap other items

## Layout

```
+------------------------------------------------------------------+
|  12dp padding top                                                |
|  [Icon]   [==Indicator==]   [Icon]          [Icon]               |
|           [  Active Icon ]                                       |
|  4dp gap                                                         |
|  Label     Label (bold)      Label           Label               |
|  16dp padding bottom                                             |
+------------------------------------------------------------------+
                              80dp
```

3-5 destinations. Below 3, use different navigation. Above 5, use
navigation drawer or navigation rail.
