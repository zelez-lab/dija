# macOS Activity Indicator (Spinning Indicator)

Reference: NSProgressIndicator (spinning style), Apple HIG (macOS 14+).

## Overview

The spinning activity indicator is a circular indicator used when the duration of an operation is unknown. It is `NSProgressIndicator` with `.spinning` style. This is the classic macOS "spinner" seen throughout the system.

## Variants

### Indeterminate Spinning (most common)

A circular ring of fading segments that rotates continuously. This is the standard "loading" indicator.

### Determinate Spinning (less common)

A circular ring that fills clockwise to show progress. Less commonly used; most apps prefer the bar-style for determinate progress.

## Metrics

### Size

| Control Size | Diameter (pt) | Line Width (pt) |
|-------------|---------------|-----------------|
| Mini        | 10            | 1.5             |
| Small       | 16            | 2               |
| Regular     | 32            | 2.5             |
| Large       | 48 (custom)   | 3               |

Note: The "standard" macOS spinner sizes are 16 and 32 pt. Mini (10) and Large (48) are less common.

### Segment Geometry

The spinner consists of 12 radial segments (lines or rounded capsules) arranged in a circle.

| Property                | Value           |
|-------------------------|-----------------|
| Number of segments       | 12              |
| Segment shape            | Rounded capsule |
| Rotation per frame       | 30 degrees (360/12) |
| Full rotation period     | ~1000 ms        |
| Frame interval           | ~83 ms per step |

### Segment Dimensions (Regular, 32 pt)

| Property                | Value           |
|-------------------------|-----------------|
| Segment length           | 8 pt            |
| Segment width            | 2.5 pt          |
| Segment corner radius    | 1.25 pt (capsule) |
| Inner radius (gap)       | 4 pt            |
| Outer radius             | 12 pt           |

## Colors

### Segment Colors

Each segment has a different opacity based on its position in the rotation, creating the "trailing" fade effect.

| Segment Position (from lead) | Opacity |
|------------------------------|---------|
| 0 (leading)                   | 1.00    |
| 1                             | 0.92    |
| 2                             | 0.83    |
| 3                             | 0.75    |
| 4                             | 0.67    |
| 5                             | 0.58    |
| 6                             | 0.50    |
| 7                             | 0.42    |
| 8                             | 0.33    |
| 9                             | 0.25    |
| 10                            | 0.17    |
| 11                            | 0.08    |

### Base Color

| Context              | Light Mode              | Dark Mode               |
|---------------------|-------------------------|-------------------------|
| On opaque background | `#4D4D4D` (dark gray)  | `#C8C8C8` (light gray)  |
| On vibrant surface   | labelColor (auto)       | labelColor (auto)        |
| Tinted / accent      | controlAccentColor      | controlAccentColor       |
| Disabled             | `rgba(0,0,0,0.15)`     | `rgba(255,255,255,0.15)` |

The base color is multiplied by the per-segment opacity values above.

## Animation

### Indeterminate Rotation

| Property                | Value                    |
|-------------------------|--------------------------|
| Rotation direction       | Clockwise               |
| Step interval            | 83 ms (12 fps)          |
| Step size                | 30 degrees              |
| Full revolution          | ~1000 ms                |
| Start behavior           | Automatic on display     |
| Stop behavior            | Fades out on hide        |

Note: The spinner does NOT use smooth continuous rotation. It uses discrete 30-degree steps, giving it the characteristic macOS spinner look.

### Determinate Fill (Circular)

When used as a determinate circular indicator:

| Property                | Value                    |
|-------------------------|--------------------------|
| Fill direction           | Clockwise from 12 o'clock |
| Track color              | `rgba(0,0,0,0.08)` light / `rgba(255,255,255,0.10)` dark |
| Fill color               | controlAccentColor        |
| Stroke width             | Line width from size table |
| Fill animation           | 250 ms ease-in-out per update |

### Show/Hide Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Show (fade in)       | 200           | Ease Out      |
| Hide (fade out)      | 200           | Ease In       |
| Start spinning       | Immediate     | N/A           |
| Stop spinning        | Last frame holds, then fades | 200 ms |

## States

| State           | Visual Changes                              |
|-----------------|---------------------------------------------|
| Spinning        | Continuous rotation animation               |
| Stopped         | Static (last position) or hidden             |
| Hidden          | Not visible, no animation running            |
| Disabled        | Dimmed, may or may not animate               |

## Usage Patterns

### Inline Loading

Small spinner next to text:

```
[*] Loading items...
```

- Spinner: 16 pt (small)
- Text: 13 pt body, labelColor
- Gap: 6 pt between spinner and text

### Full-Area Loading

Centered spinner for content areas:

```
+---------------------------+
|                           |
|           [*]             |
|       Loading...          |
|                           |
+---------------------------+
```

- Spinner: 32 pt (regular) or larger
- Label below: 13 pt, secondaryLabelColor
- Gap: 8 pt between spinner and label

### Button Loading State

Replace button content with spinner:

- Spinner size matches button's font size (13 pt regular)
- Spinner is white on accent-colored buttons
- Spinner is labelColor on standard buttons
- Button disabled during loading

### Toolbar Loading

Status bar or toolbar spinner:

- Spinner: 16 pt (small)
- Color: secondaryLabelColor
- No label

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.progressIndicator`                      |
| Trait        | Indeterminate                             |
| Description  | "Loading" or custom label                  |
| Value        | None (indeterminate) or 0.0-1.0 (determinate) |

## Dija Skin Mapping

```
comp! Spinner {
    attr size, Size, default: Size::MD
    attr color, Option<Color>, default: None  // None = auto from context
    attr spinning, bool, default: true

    // macOS skin maps:
    // Size::XS  -> 10 pt diameter (mini)
    // Size::SM  -> 16 pt diameter
    // Size::MD  -> 32 pt diameter
    // Size::LG  -> 48 pt diameter
    //
    // 12 segments at decreasing opacity
    // Step animation: 30 deg every 83 ms
    // Color: dark gray (light), light gray (dark) unless overridden
    // Show/hide: 200 ms fade
}
```
