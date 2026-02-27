# macOS Slider (NSSlider)

Reference: NSSlider, NSSliderCell, Apple HIG (macOS 14+).

## Overview

`NSSlider` provides a continuous or discrete value selection control. The same class renders as horizontal, vertical, or circular depending on frame proportions. macOS sliders have a clean, minimal look with a round knob on a track.

## Variants

| Variant             | Condition                        | Usage                      |
|--------------------|----------------------------------|----------------------------|
| Horizontal (linear) | Width > Height                  | Most common                |
| Vertical (linear)   | Height > Width                  | Volume, levels             |
| Circular            | Set via `sliderType = .circular` | Jog wheels, fine adjustment |

## Slider Types

| Type              | Description                                            |
|-------------------|--------------------------------------------------------|
| `.linear`         | Standard horizontal or vertical track with knob        |
| `.circular`       | Rotary dial control                                    |

## Metrics

### Track

| Control Size | Track Height (pt) | Track Corner Radius (pt) |
|-------------|-------------------|--------------------------|
| Mini        | 2                 | 1 (capsule)              |
| Small       | 2.5               | 1.25 (capsule)           |
| Regular     | 4                 | 2 (capsule)              |
| Large       | 5                 | 2.5 (capsule)            |

### Knob (Thumb)

The knob is a circular handle that the user drags along the track.

| Control Size | Knob Diameter (pt) | Knob Border (pt) |
|-------------|-------------------|-------------------|
| Mini        | 12                | 0.5               |
| Small       | 14                | 0.5               |
| Regular     | 18                | 0.5               |
| Large       | 22                | 0.5               |

### Tick Marks (Discrete Sliders)

When `numberOfTickMarks > 0`:

| Control Size | Tick Width (pt) | Tick Height (pt) | Tick Spacing from Track (pt) |
|-------------|-----------------|------------------|------------------------------|
| Mini        | 1               | 4                | 2                            |
| Small       | 1               | 5                | 2                            |
| Regular     | 1               | 7                | 3                            |
| Large       | 1               | 9                | 3                            |

Tick marks can appear above, below, or both sides of the track (`tickMarkPosition`):
- `.above` / `.leading` -- ticks above (horizontal) or left (vertical)
- `.below` / `.trailing` -- ticks below (horizontal) or right (vertical)

### Circular Slider

| Control Size | Diameter (pt) | Indicator Width (pt) |
|-------------|---------------|---------------------|
| Mini        | 24            | 2                   |
| Small       | 30            | 2                   |
| Regular     | 40            | 3                   |
| Large       | 50            | 3                   |

## Colors

### Track

| Element            | Light Mode                    | Dark Mode                      |
|--------------------|-------------------------------|--------------------------------|
| Track (unfilled)   | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.10)`       |
| Track (filled)     | controlAccentColor (`#007AFF`)| controlAccentColor (`#0A84FF`) |
| Track disabled     | `rgba(0,0,0,0.04)`           | `rgba(255,255,255,0.04)`       |
| Filled disabled    | controlAccentColor at 40%     | controlAccentColor at 40%      |

The "filled" portion extends from the minimum value to the current knob position.

### Knob

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `#FFFFFF`               | `#FFFFFF`               |
| Hover        | `#FFFFFF`               | `#FFFFFF`               |
| Pressed      | `#F0F0F0`               | `#E8E8E8`               |
| Disabled     | `#F5F5F5`               | `#D0D0D0`               |

### Knob Border

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `rgba(0,0,0,0.15)`     | `rgba(0,0,0,0.30)`     |
| Hover        | `rgba(0,0,0,0.20)`     | `rgba(0,0,0,0.35)`     |
| Pressed      | `rgba(0,0,0,0.25)`     | `rgba(0,0,0,0.40)`     |
| Disabled     | `rgba(0,0,0,0.08)`     | `rgba(0,0,0,0.15)`     |

### Knob Shadow

```
Color:   rgba(0, 0, 0, 0.12)
Offset:  (0, 0.5) pt
Blur:    2 pt
```

Pressed state shadow:

```
Color:   rgba(0, 0, 0, 0.08)
Offset:  (0, 0.5) pt
Blur:    1 pt
```

### Tick Marks

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `rgba(0,0,0,0.20)`     | `rgba(255,255,255,0.20)`|
| Disabled     | `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.08)`|

## States

| State        | Visual Changes                                          |
|--------------|--------------------------------------------------------|
| Normal       | Default track + knob                                    |
| Hover        | Knob border darkens slightly                            |
| Pressed      | Knob slightly darker, reduced shadow                    |
| Dragging     | Knob follows mouse, continuous value update             |
| Disabled     | 40% opacity on filled track, dimmed knob                |
| Focused      | Focus ring around entire slider                         |

## Animation

| Transition              | Duration (ms) | Curve          |
|------------------------|---------------|----------------|
| Knob snap to tick       | 150           | Spring (snappy)|
| Track fill change       | 0             | Immediate      |
| Hover border darken     | 80            | Ease Out       |
| Press feedback          | 30            | Ease Out       |
| Focus ring appear       | 150           | Ease Out       |

## Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from knob bounds (or track bounds)
Radius:   knob radius + 3 pt
```

Some implementations show the focus ring around the knob only; others around the entire track. AppKit default is around the knob.

## Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Left Arrow      | Decrease value by one step                 |
| Right Arrow     | Increase value by one step                 |
| Up Arrow        | Increase value (vertical) / decrease (circular) |
| Down Arrow      | Decrease value (vertical) / increase (circular) |
| Option+Arrow    | Larger step (10% of range)                 |
| Home            | Set to minimum value                       |
| End             | Set to maximum value                       |

## Value Display

Sliders do not natively display their current value. If a value label is needed, it should be a separate `NSTextField` positioned near the slider.

## Dija Skin Mapping

```
comp! Slider {
    attr min, f32, default: 0.0
    attr max, f32, default: 1.0
    attr value, f32, default: 0.5
    attr step, f32, default: 0.0  // 0 = continuous
    attr disabled, bool, default: false
    attr size, Size, default: Size::MD

    // macOS skin maps:
    // Track: thin capsule (4 pt height regular)
    // Filled portion: accent color from min to value
    // Knob: 18 pt white circle with shadow
    // Tick marks: thin lines below track when step > 0
}
```
