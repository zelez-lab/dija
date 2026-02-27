# Android — Progress Indicators (Material Design 3)

Source: m3.material.io/components/progress-indicators/specs

## Variants

| Variant | Type | Description |
|---------|------|------------|
| Linear determinate | Horizontal bar | Known progress (file upload, download) |
| Linear indeterminate | Horizontal bar | Unknown duration (loading) |
| Circular determinate | Ring | Known progress (timer, loading %) |
| Circular indeterminate | Ring | Unknown duration (spinner) |

## Linear Progress Indicator

### Metrics

| Property | Value |
|----------|-------|
| Track height | 4dp |
| Track corner radius | 2dp (rounded ends) |
| Active indicator corner radius | 2dp |
| Min width | 240dp (recommended) |
| Stop indicator diameter | 4dp |
| Gap between indicator and track | 4dp |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Active indicator | `#6750A4` (primary) | `#D0BCFF` |
| Track | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Stop indicator | `#6750A4` (primary) | `#D0BCFF` |

### Determinate

- Active indicator width = progress percentage of total track width
- Stop indicator (4dp dot) at the end of the active track
- Gap between active indicator end and inactive track start

### Indeterminate

- Two animated indicators slide across the track
- Animation cycle: Long 4 (600ms) per sweep
- Easing: Emphasized

## Circular Progress Indicator

### Metrics

| Property | Value |
|----------|-------|
| Diameter | 48dp (default) |
| Track thickness (stroke) | 4dp |
| Track corner radius | 2dp (rounded cap) |
| Active indicator gap | 4dp |
| Padding | 4dp |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Active indicator | `#6750A4` (primary) | `#D0BCFF` |
| Track | `#E8DEF8` (secondaryContainer) | `#4A4458` |

### Determinate

- Active arc length = progress percentage of full circle (360 degrees)
- Starts from 12 o'clock position
- Gap between active and inactive track arcs

### Indeterminate

- Active arc grows and shrinks while rotating
- Rotation: continuous 360-degree, ~1333ms per revolution
- Arc sweep: oscillates between ~10 and ~270 degrees
- Easing: Standard

## Disabled State

| Element | Value |
|---------|-------|
| Active indicator | onSurface @ 38% |
| Track | onSurface @ 12% |

## Animation Details

### Linear Indeterminate

```
Phase 1: First indicator enters from left, grows, exits right
Phase 2: Second indicator enters from left, overlaps, exits right
Cycle: ~2000ms total, repeating
```

### Circular Indeterminate

```
Rotation: continuous clockwise, 1333ms per revolution
Arc length: grows from ~10deg to ~270deg, then shrinks
Head and tail move at different speeds
```

## Comparison with iOS

| Property | iOS Activity Indicator | M3 Progress Indicator |
|----------|----------------------|----------------------|
| Circular style | Spinning dots | Animated arc |
| Linear style | UIProgressView (2dp) | 4dp track with gaps |
| Default size (circular) | 20dp | 48dp |
| Track visibility | No track | Track always visible |
| Color | systemGray | primary |
