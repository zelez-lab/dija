# macOS Switch (NSSwitch)

Reference: NSSwitch (macOS 10.15+), Apple HIG (macOS 14+).

## Overview

`NSSwitch` was introduced in macOS 10.15 Catalina, bringing the iOS-style toggle switch to the Mac. It provides a binary on/off control that is visually distinct from checkboxes. It is NOT a subclass of NSButton -- it is its own control.

## Metrics

### Track (Capsule)

| Control Size | Width (pt) | Height (pt) | Corner Radius (pt) |
|-------------|------------|-------------|---------------------|
| Mini        | 26         | 15          | 7.5 (capsule)       |
| Small       | 30         | 17          | 8.5 (capsule)       |
| Regular     | 38         | 22          | 11 (capsule)        |
| Large       | 46         | 26          | 13 (capsule)        |

### Thumb (Knob)

The thumb is a circular knob that slides between off (left) and on (right) positions.

| Control Size | Diameter (pt) | Inset from Track (pt) |
|-------------|---------------|----------------------|
| Mini        | 13            | 1                    |
| Small       | 15            | 1                    |
| Regular     | 20            | 1                    |
| Large       | 24            | 1                    |

### Thumb Shadow

```
Color:   rgba(0, 0, 0, 0.15)
Offset:  (0, 1) pt
Blur:    2 pt
```

## Colors

### Track

| State            | Light Mode                         | Dark Mode                          |
|------------------|------------------------------------|------------------------------------|
| Off              | `rgba(0,0,0,0.09)`                | `rgba(255,255,255,0.10)`           |
| Off + Hover      | `rgba(0,0,0,0.12)`                | `rgba(255,255,255,0.14)`           |
| On               | controlAccentColor (`#007AFF`)     | controlAccentColor (`#0A84FF`)     |
| On + Hover       | controlAccentColor darkened 5%     | controlAccentColor lightened 5%    |
| On + Pressed     | controlAccentColor darkened 12%    | controlAccentColor lightened 10%   |
| Disabled Off     | `rgba(0,0,0,0.04)`                | `rgba(255,255,255,0.05)`           |
| Disabled On      | controlAccentColor at 40% opacity  | controlAccentColor at 40% opacity  |

### Thumb (Knob)

| State            | Light Mode      | Dark Mode       |
|------------------|-----------------|-----------------|
| Normal           | `#FFFFFF`       | `#FFFFFF`       |
| Pressed          | `#F0F0F0`       | `#E8E8E8`       |
| Disabled         | `#F5F5F5`       | `#D0D0D0`       |

### Border (Track)

| State            | Light Mode            | Dark Mode                 |
|------------------|-----------------------|---------------------------|
| Off              | `rgba(0,0,0,0.12)`   | `rgba(255,255,255,0.10)`  |
| On               | Transparent (filled)  | Transparent (filled)      |
| Disabled         | `rgba(0,0,0,0.06)`   | `rgba(255,255,255,0.05)`  |

Border width: 0.5 pt.

## States

| State        | Track                 | Thumb               | Notes                      |
|-------------|----------------------|---------------------|----------------------------|
| Off          | Gray fill            | Left position       |                            |
| On           | Accent color fill    | Right position      |                            |
| Off hover    | Slightly darker gray | Normal               |                            |
| On hover     | Slightly adjusted    | Normal               |                            |
| Pressed      | Same as current      | Slightly wider (squish) | Thumb expands ~2 pt wider  |
| Disabled     | Reduced opacity      | Dimmed               | No interaction             |
| Focused      | Focus ring           | Normal               | Keyboard navigation        |

### Thumb Press Effect

When the thumb is pressed, it visually stretches in the direction of travel:
- Regular size: thumb width grows from 20 pt to ~24 pt
- The stretch is an ellipse, not a wider circle
- This gives a tactile "grabbable" feeling

## Animation

The switch uses a spring animation for the thumb transition:

| Transition            | Duration (ms) | Curve            |
|----------------------|---------------|------------------|
| Off -> On (thumb)     | 250           | Spring (snappy)  |
| On -> Off (thumb)     | 250           | Spring (snappy)  |
| Track color change    | 200           | Ease In Out      |
| Press expand          | 80            | Ease Out         |
| Release contract      | 150           | Spring (snappy)  |
| Hover highlight       | 100           | Ease Out         |
| Focus ring appear     | 150           | Ease Out         |

Spring parameters for thumb: `bounce: 0.15, duration: 0.4`

## Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from track bounds
Radius:   track corner radius + 3 pt (capsule + 3)
```

## Keyboard Interaction

| Key          | Action                                    |
|-------------|-------------------------------------------|
| Space        | Toggle on/off                             |
| Tab          | Move focus to next control                |
| Shift+Tab    | Move focus to previous control            |

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.switch`                                 |
| Value        | 0 (off) or 1 (on)                        |
| Label        | Associated label text                      |
| Traits       | `.togglable`                              |

## Dija Skin Mapping

```
comp! Switch {
    attr on, bool, default: false
    attr disabled, bool, default: false
    attr size, Size, default: Size::MD

    // macOS skin maps:
    // Size::XS  -> Mini   (26x15 track, 13 thumb)
    // Size::SM  -> Small  (30x17 track, 15 thumb)
    // Size::MD  -> Regular (38x22 track, 20 thumb)
    // Size::LG  -> Large  (46x26 track, 24 thumb)
    //
    // Track: rounded rect with capsule radius
    // Thumb: circle positioned left (off) or right (on)
    // On-color: controlAccentColor
    // Animation: spring with bounce 0.15
}
```
