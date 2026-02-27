# Android — Badge (Material Design 3)

Source: m3.material.io/components/badges/specs

## Variants

| Variant | Size | Content |
|---------|------|---------|
| Small (dot) | 6dp x 6dp | No content, presence indicator |
| Large (number) | 16dp height, variable width | 1-3 digit count |

## Small Badge (Dot)

| Property | Value |
|----------|-------|
| Width | 6dp |
| Height | 6dp |
| Corner radius | 3dp (full circle) |
| Color | error (`#B3261E` light / `#F2B8B5` dark) |

## Large Badge (Number)

| Property | Value |
|----------|-------|
| Min width | 16dp |
| Height | 16dp |
| Corner radius | 8dp (full pill) |
| Horizontal padding | 4dp |
| Label font | Label Small (Roboto Medium 500, 11sp) |
| Max digits | 3 (displays "999+" for larger values) |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#B3261E` (error) | `#F2B8B5` |
| Label | `#FFFFFF` (onError) | `#601410` |

## Positioning

Badges are positioned relative to their anchor element (typically an icon):

| Anchor | Small badge offset | Large badge offset |
|--------|-------------------|-------------------|
| Icon (24dp) | top: -2dp, right: -4dp | top: -4dp, right: -6dp |
| Navigation icon | top: 2dp, right: 4dp (from icon center) | top: 0dp, right: 0dp |

Badge should not clip outside the component container bounds. If it would,
adjust position inward.

## States

Badges themselves have no interactive states (not tappable). They reflect
the state of their parent component:

| Parent state | Badge effect |
|-------------|-------------|
| Enabled | Visible |
| Disabled | Hidden or reduced opacity |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Enter (scale up) | Short 3 (150ms) | Emphasized decelerate |
| Exit (scale down) | Short 2 (100ms) | Standard accelerate |
| Count change | Short 2 (100ms) | Cross-fade |

Enter animation scales from 0 to 1.0 at the badge center point.

## Layout

### On Icon Button

```
+---[Badge 6dp]---+
|  +-----------+  |
|  | Icon 24dp |  |
|  +-----------+  |
+------------------+
```

### On Navigation Bar Icon

```
    [16dp Badge: 3]
  +-----------+
  | Icon 24dp |
  +-----------+
     Label
```

## Comparison with iOS Badge

| Property | iOS Badge | M3 Badge |
|----------|----------|----------|
| Small size | 6dp dot | 6dp dot |
| Large size | 18dp height | 16dp height |
| Color | systemRed (`#FF3B30`) | error (`#B3261E`) |
| Font | SF Pro Bold, 13sp | Roboto Medium, 11sp |
| Shape | Circle/pill | Circle/pill |
| Max display | Unlimited | 999+ |
