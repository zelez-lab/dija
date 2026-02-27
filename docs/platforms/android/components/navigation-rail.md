# Android — Navigation Rail (Material Design 3)

Source: m3.material.io/components/navigation-rail/specs

Vertical side navigation for tablets and larger screens. Replaces bottom
navigation bar when screen width >= 600dp (medium window size class).

## Metrics

| Property | Value |
|----------|-------|
| Width | 80dp |
| Elevation | Level 0 (0dp) |
| Surface | surface |
| Icon size | 24dp |
| Active indicator width | 56dp |
| Active indicator height | 32dp |
| Active indicator corner radius | 16dp (full pill) |
| Label font | Label Medium (Roboto Medium 500, 12sp) |
| Icon-to-label gap | 4dp |
| Item spacing (between items) | 0dp (vertically centered in 56dp slot) |
| Item height | 56dp (icon + label slot) |
| Top padding | 44dp (or FAB placement) |
| Alignment | Center (default), top |

## FAB Placement

The rail can host a FAB at the top, above the navigation items:

| Property | Value |
|----------|-------|
| FAB position | Top of rail, centered horizontally |
| FAB to first item gap | 12dp |
| FAB variant | Small (40dp) or standard (56dp) |

## Active Indicator

| Property | Value |
|----------|-------|
| Width | 56dp |
| Height | 32dp |
| Corner radius | 16dp (full pill) |
| Color | secondaryContainer |

## Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#FEF7FF` (surface) | `#141218` |
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

State layer color: onSurface for inactive, onSecondaryContainer for active.

## Configuration

| Mode | Labels | Description |
|------|--------|------------|
| Labels visible | All items | Always show icon + label |
| Labels selected | Active only | Only selected item shows label |
| Labels hidden | None | Icon-only rail |

## Menu Anchor

Navigation rail can show a menu icon at the top (above FAB) to
toggle an expanded navigation drawer. This is used in responsive
layouts:

- Compact (< 600dp): bottom navigation bar
- Medium (600-839dp): navigation rail
- Expanded (>= 840dp): navigation drawer

## Layout

```
+--------+
|  Menu  |  (optional hamburger icon)
| 44dp   |
|  FAB   |  (optional)
| 12dp   |
| [Icon] |
| Label  |
|        |
| [Icon] |
| Label  |
|        |
| [Icon] |
| Label  |
|        |
| [Icon] |
| Label  |
+--------+
   80dp
```

## Badge Position

Same as navigation bar: badges on top-right of icon.
