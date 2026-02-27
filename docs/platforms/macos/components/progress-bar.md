# macOS Progress Bar (NSProgressIndicator -- Bar Style)

Reference: NSProgressIndicator, Apple HIG (macOS 14+).

## Overview

`NSProgressIndicator` with `.bar` style displays a horizontal progress bar. It supports both determinate (known progress) and indeterminate (unknown duration) modes. The bar style is the most common progress indicator in macOS.

## Styles

| Style            | Description                                              |
|------------------|----------------------------------------------------------|
| `.bar`           | Horizontal progress bar (this document)                  |
| `.spinning`      | Circular spinning indicator (see activity-indicator.md)   |

## Metrics

### Determinate Bar

| Control Size | Height (pt) | Corner Radius (pt) | Min Width (pt) |
|-------------|-------------|---------------------|----------------|
| Mini        | 4           | 2 (capsule)         | 32             |
| Small       | 6           | 3 (capsule)         | 48             |
| Regular     | 6           | 3 (capsule)         | 64             |
| Large       | 8           | 4 (capsule)         | 64             |

The bar width is typically the full width of its container. Height is fixed per control size.

### Indeterminate Bar

Same dimensions as determinate. The indeterminate bar shows an animated "barber pole" pattern -- diagonal stripes that scroll left to right continuously.

| Property                  | Value             |
|---------------------------|-------------------|
| Stripe width               | 12 pt            |
| Stripe angle               | ~30 degrees      |
| Animation speed            | ~40 pt/sec       |

## Colors

### Track (Background)

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.10)`       |
| Disabled     | `rgba(0,0,0,0.04)`           | `rgba(255,255,255,0.05)`       |

### Fill (Progress)

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | controlAccentColor (`#007AFF`)| controlAccentColor (`#0A84FF`) |
| Disabled     | controlAccentColor at 40%     | controlAccentColor at 40%      |

### Indeterminate Stripes

| Element              | Light Mode                         | Dark Mode                          |
|----------------------|------------------------------------|------------------------------------|
| Stripe 1 (lighter)   | controlAccentColor at 70% opacity | controlAccentColor at 70% opacity  |
| Stripe 2 (darker)    | controlAccentColor at 100%        | controlAccentColor at 100%         |

## Border

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `rgba(0,0,0,0.06)`     | `rgba(255,255,255,0.06)`|
| Disabled     | `rgba(0,0,0,0.03)`     | `rgba(255,255,255,0.03)`|

Border width: 0.5 pt.

## Progress Fill Corner Radius

The fill portion has the same corner radius as the track, minus the inset:

```
Fill corner radius = Track corner radius - 0.5 (border width)
```

When progress is very small (< 2x corner radius), the fill becomes a short capsule.

## Animation

### Determinate

| Transition               | Duration (ms) | Curve         |
|-------------------------|---------------|---------------|
| Value change (smooth)    | 250           | Ease In Out   |
| Value jump (large delta) | 150           | Ease Out      |
| Appear                   | 200           | Fade in       |
| Disappear                | 200           | Fade out      |

### Indeterminate

| Property                 | Value                          |
|--------------------------|--------------------------------|
| Stripe scroll speed       | ~40 pt/sec                    |
| Animation type            | Continuous linear scrolling   |
| Start animation           | Automatic when indeterminate  |
| Stop animation            | On `stopAnimation()` or hide  |

### State Transitions

| Transition                      | Duration (ms) | Curve          |
|---------------------------------|---------------|----------------|
| Determinate -> Indeterminate    | 200           | Crossfade      |
| Indeterminate -> Determinate    | 200           | Crossfade      |
| Enable -> Disable               | 200           | Ease In Out    |
| Show -> Hide                    | 200           | Fade           |

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.progressIndicator`                      |
| Value        | Current progress (0.0 to 1.0)             |
| Min value    | 0.0                                       |
| Max value    | 1.0 (or `maxValue`)                      |
| Description  | "Progress" or custom label                 |

## Common Patterns

### Linear Progress (file download, export)

```
[========================            ]  72%
```

Full width of container, optional percentage label to the right.

### Inline Progress (toolbar, status bar)

```
Loading... [===========             ]
```

Smaller width, paired with a text description.

### System Download Progress

For system-level downloads (App Store, Software Update), progress bars show:
- Determinate fill with smooth animation
- Gradient shimmer on the fill (subtle highlight sweep)
- Pause/resume support (striped pattern when paused)

## Dija Skin Mapping

```
comp! ProgressBar {
    attr value, f32, default: 0.0      // 0.0 to 1.0
    attr indeterminate, bool, default: false
    attr size, Size, default: Size::MD

    // macOS skin maps:
    // Size::XS  -> Mini   (4 pt height)
    // Size::SM  -> Small  (6 pt height)
    // Size::MD  -> Regular (6 pt height)
    // Size::LG  -> Large  (8 pt height)
    //
    // Track: rounded capsule, gray fill
    // Fill: accent color, animated value changes
    // Indeterminate: scrolling barber pole stripes
    // Border: 0.5 pt subtle outline
}
```
