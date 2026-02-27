# Slider

A control that allows the user to select a value from a continuous or discrete range by dragging a thumb along a track.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UISlider | Documented |
| macOS | NSSlider | Documented |
| Android | Slider (Material Design 3) | Documented |
| Windows | Slider | Documented |
| Linux | GtkScale | Documented |

## iOS

Source: UISlider, SwiftUI Slider

### Track

| Property | Value |
|----------|-------|
| Height | 4pt (visual), 44pt (hit area) |
| Corner radius | 2pt (fully rounded) |
| Minimum track color | tintColor (systemBlue by default) |
| Maximum track color | systemFill (`#787880` @ 0.20 light / @ 0.36 dark) |
| Total width | Fills available horizontal space |

### Thumb

| Property | Value |
|----------|-------|
| Size | 28pt diameter |
| Color | white (`#FFFFFF`) |
| Shadow 1 | offset(0, 0.5) blur 4, black @ 0.12 |
| Shadow 2 | offset(0, 0.5) blur 1, black @ 0.04 |
| Corner radius | 14pt (fully circular) |
| Hit area | 44 x 44pt (padded beyond visual) |

### Custom Min/Max Images

| Property | Value |
|----------|-------|
| Position | Left of min track / right of max track |
| Size | 20pt (typically) |
| Color | secondaryLabel |
| Spacing from track | 8pt |

### States

| State | Track | Thumb | Notes |
|-------|-------|-------|-------|
| Normal | Standard colors | White circle, shadows | |
| Dragging | Standard colors | White circle, shadows, tracks finger | No visual change on thumb during drag |
| Disabled | Alpha 0.3 | Alpha 0.3 | Entire slider dimmed |

### Animation

| Property | Value |
|----------|-------|
| Value change (programmatic) | 0.15s ease-in-out (when `animated: true`) |
| Thumb snap (to stepped values) | 0.1s ease-out |
| Track fill | Follows thumb position in real-time (no animation lag) |

### Stepped Slider

When using discrete steps (SwiftUI `Slider(value:in:step:)`):

| Property | Value |
|----------|-------|
| Tick marks | Not visible by default (no built-in tick UI) |
| Snap behavior | Thumb snaps to nearest step on release |
| Haptic feedback | Light impact at each step boundary |

### Continuous vs. Discrete

| Mode | Behavior |
|------|----------|
| Continuous | Value updates in real-time as thumb moves |
| Discrete (with step) | Value snaps to nearest step on release |

### Metrics (Summary)

```
     +-- min image (optional)
     |
     v        min track (tintColor)    max track (gray)
    [<]  ==================O==================  [>]
                              ^                        ^
                           thumb (28pt)          max image (optional)
         <------------ track (4pt height) ------------>
```

### Accessibility

| Property | Value |
|----------|-------|
| Role | Slider (adjustable) |
| VoiceOver | "[Label], [value]%, adjustable" |
| Increment/decrement | ~10% of range per swipe up/down |
| Custom step | Respects step value if set |

## macOS

Reference: NSSlider, NSSliderCell, Apple HIG (macOS 14+).

### Overview

`NSSlider` provides a continuous or discrete value selection control. The same class renders as horizontal, vertical, or circular depending on frame proportions. macOS sliders have a clean, minimal look with a round knob on a track.

### Variants

| Variant             | Condition                        | Usage                      |
|--------------------|----------------------------------|----------------------------|
| Horizontal (linear) | Width > Height                  | Most common                |
| Vertical (linear)   | Height > Width                  | Volume, levels             |
| Circular            | Set via `sliderType = .circular` | Jog wheels, fine adjustment |

### Slider Types

| Type              | Description                                            |
|-------------------|--------------------------------------------------------|
| `.linear`         | Standard horizontal or vertical track with knob        |
| `.circular`       | Rotary dial control                                    |

### Metrics

#### Track

| Control Size | Track Height (pt) | Track Corner Radius (pt) |
|-------------|-------------------|--------------------------|
| Mini        | 2                 | 1 (capsule)              |
| Small       | 2.5               | 1.25 (capsule)           |
| Regular     | 4                 | 2 (capsule)              |
| Large       | 5                 | 2.5 (capsule)            |

#### Knob (Thumb)

The knob is a circular handle that the user drags along the track.

| Control Size | Knob Diameter (pt) | Knob Border (pt) |
|-------------|-------------------|-------------------|
| Mini        | 12                | 0.5               |
| Small       | 14                | 0.5               |
| Regular     | 18                | 0.5               |
| Large       | 22                | 0.5               |

#### Tick Marks (Discrete Sliders)

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

#### Circular Slider

| Control Size | Diameter (pt) | Indicator Width (pt) |
|-------------|---------------|---------------------|
| Mini        | 24            | 2                   |
| Small       | 30            | 2                   |
| Regular     | 40            | 3                   |
| Large       | 50            | 3                   |

### Colors

#### Track

| Element            | Light Mode                    | Dark Mode                      |
|--------------------|-------------------------------|--------------------------------|
| Track (unfilled)   | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.10)`       |
| Track (filled)     | controlAccentColor (`#007AFF`)| controlAccentColor (`#0A84FF`) |
| Track disabled     | `rgba(0,0,0,0.04)`           | `rgba(255,255,255,0.04)`       |
| Filled disabled    | controlAccentColor at 40%     | controlAccentColor at 40%      |

The "filled" portion extends from the minimum value to the current knob position.

#### Knob

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `#FFFFFF`               | `#FFFFFF`               |
| Hover        | `#FFFFFF`               | `#FFFFFF`               |
| Pressed      | `#F0F0F0`               | `#E8E8E8`               |
| Disabled     | `#F5F5F5`               | `#D0D0D0`               |

#### Knob Border

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `rgba(0,0,0,0.15)`     | `rgba(0,0,0,0.30)`     |
| Hover        | `rgba(0,0,0,0.20)`     | `rgba(0,0,0,0.35)`     |
| Pressed      | `rgba(0,0,0,0.25)`     | `rgba(0,0,0,0.40)`     |
| Disabled     | `rgba(0,0,0,0.08)`     | `rgba(0,0,0,0.15)`     |

#### Knob Shadow

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

#### Tick Marks

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `rgba(0,0,0,0.20)`     | `rgba(255,255,255,0.20)`|
| Disabled     | `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.08)`|

### States

| State        | Visual Changes                                          |
|--------------|--------------------------------------------------------|
| Normal       | Default track + knob                                    |
| Hover        | Knob border darkens slightly                            |
| Pressed      | Knob slightly darker, reduced shadow                    |
| Dragging     | Knob follows mouse, continuous value update             |
| Disabled     | 40% opacity on filled track, dimmed knob                |
| Focused      | Focus ring around entire slider                         |

### Animation

| Transition              | Duration (ms) | Curve          |
|------------------------|---------------|----------------|
| Knob snap to tick       | 150           | Spring (snappy)|
| Track fill change       | 0             | Immediate      |
| Hover border darken     | 80            | Ease Out       |
| Press feedback          | 30            | Ease Out       |
| Focus ring appear       | 150           | Ease Out       |

### Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from knob bounds (or track bounds)
Radius:   knob radius + 3 pt
```

Some implementations show the focus ring around the knob only; others around the entire track. AppKit default is around the knob.

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Left Arrow      | Decrease value by one step                 |
| Right Arrow     | Increase value by one step                 |
| Up Arrow        | Increase value (vertical) / decrease (circular) |
| Down Arrow      | Decrease value (vertical) / increase (circular) |
| Option+Arrow    | Larger step (10% of range)                 |
| Home            | Set to minimum value                       |
| End             | Set to maximum value                       |

### Value Display

Sliders do not natively display their current value. If a value label is needed, it should be a separate `NSTextField` positioned near the slider.

### Dija Skin Mapping

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

## Android

Source: m3.material.io/components/sliders/specs

### Variants

| Variant | Description |
|---------|------------|
| Continuous | Smooth value selection across range |
| Discrete | Snaps to predefined steps (tick marks) |
| Range | Two thumbs for min/max selection |
| Centered | Anchored at center, slides left or right |

### Metrics

| Property | Value |
|----------|-------|
| Track height (active) | 4dp |
| Track height (inactive) | 4dp |
| Track corner radius | 2dp (rounded ends) |
| Thumb diameter | 20dp |
| Thumb shape | Circle |
| Handle (outer touch area) | 44dp |
| Touch target | 48dp x 48dp |
| Tick mark size | 4dp x 4dp |
| Tick mark shape | Circle |
| Track gap (between thumb and track) | 6dp |
| Stop indicator size | 4dp x 4dp |
| Value label height | 28dp |
| Value label corner radius | 14dp (full pill) |
| Value label padding | 8dp horizontal |
| Value label font | Label Medium (Roboto Medium 500, 12sp) |

### Colors

#### Track

| Element | Light | Dark |
|---------|-------|------|
| Active track | `#6750A4` (primary) | `#D0BCFF` |
| Inactive track | `#E7E0EC` (surfaceContainerHighest) | `#36343B` |
| Active tick marks | `#FFFFFF` (onPrimary) | `#381E72` |
| Inactive tick marks | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Stop indicator | `#6750A4` (primary) | `#D0BCFF` |

#### Thumb

| Element | Light | Dark |
|---------|-------|------|
| Thumb | `#6750A4` (primary) | `#D0BCFF` |
| State layer (hovered) | primary @ 8% | primary @ 8% |
| State layer (focused) | primary @ 10% | primary @ 10% |
| State layer (pressed) | primary @ 10% | primary @ 10% |

#### Value Label

| Element | Light | Dark |
|---------|-------|------|
| Container | `#6750A4` (primary) | `#D0BCFF` |
| Text | `#FFFFFF` (onPrimary) | `#381E72` |

#### Disabled

| Element | Value |
|---------|-------|
| Active track | onSurface @ 38% |
| Inactive track | onSurface @ 12% |
| Thumb | onSurface @ 38%, with surface @ 100% inner circle |

### States

| State | Effect |
|-------|--------|
| Enabled | Default styling |
| Hovered | 40dp state layer halo around thumb |
| Focused | 40dp state layer halo around thumb |
| Pressed | 40dp state layer halo, value label appears (discrete) |
| Dragged | State layer 16% |
| Disabled | Reduced opacity track and thumb |

### Discrete Slider

- Tick marks shown on track at each step
- Value label popup appears above thumb on press/drag
- Thumb snaps to nearest tick mark on release

### Animation

- Value label enter: Short 3 (150ms), Standard decelerate
- Value label exit: Short 2 (100ms), Standard accelerate
- Snap to tick: Short 4 (200ms), Standard easing
- State layer: Short 2 (100ms)

## Windows

Source: WinUI 3 Slider control

### Track

| Property | Value |
|----------|-------|
| Track height | 4px (rest), 6px (hover/interaction) |
| Corner radius | 2px (fully rounded at 4px height) |
| Filled (min side) | AccentFillColorDefault (SystemAccentColor) |
| Unfilled (max side) | ControlStrongFillColorDefault (`#72000000` / `#9AFFFFFF`) |
| Total hit area height | 32px (invisible padding above/below track) |

### Thumb (Knob)

| Property | Value |
|----------|-------|
| Outer diameter | 20px |
| Inner dot diameter | 8px (rest), 10px (hover), 14px (pressed) |
| Outer fill | White (light) / `#FFFFFF` | Dark: `#FFFFFF` |
| Inner fill | AccentFillColorDefault |
| Shadow | Shadow 2 (key: 0px 1px 1px rgba(0,0,0,0.08), ambient: 0px 0px 2px rgba(0,0,0,0.06)) |
| Border | 1px ControlStrokeColorSecondary |

The thumb uses a **two-layer design**: a white outer circle with a subtle shadow, and an accent-colored inner dot that grows/shrinks based on interaction state.

### States

| State | Track height | Filled color | Unfilled color | Thumb inner dot |
|-------|-------------|-------------|----------------|----------------|
| Rest | 4px | AccentFillColorDefault | ControlStrongFillColorDefault | 8px, AccentColor |
| Hover | 6px | AccentFillColorSecondary | ControlStrongFillColorDefault | 10px, AccentColor |
| Pressed | 6px | AccentFillColorTertiary | ControlStrongFillColorDefault | 14px, AccentColor |
| Disabled | 4px | AccentFillColorDisabled | ControlStrongFillColorDisabled | 8px, disabled gray |

### Tick Marks

Optional tick marks along the track.

| Property | Value |
|----------|-------|
| Tick width | 1px |
| Tick height | 4px |
| Tick color | ControlStrongFillColorDefault |
| Position | Centered below (horizontal) or beside (vertical) the track |
| TickFrequency | Configurable (integer step) |
| TickPlacement | None, TopLeft, BottomRight, Outside |

### Range Labels

| Property | Value |
|----------|-------|
| Min/Max value labels | Optional, 12px Caption |
| Header label | Optional, 14px Regular, positioned above |
| Current value tooltip | Appears on press, shows numeric value |

### Layout

```
Header label (optional)
--------------*--------------  <- track with thumb
Tick marks (optional)
```

| Property | Value |
|----------|-------|
| Horizontal slider height | 32px (including hit area) |
| Vertical slider width | 32px |
| Min length | 100px |

### Step Snap

When `StepFrequency` or `SnapsTo` is set, the thumb snaps to discrete positions along the track. The snap animation uses:

| Transition | Duration | Easing |
|-----------|----------|--------|
| Snap to nearest step | 100ms | Control fast |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Track height grow (rest -> hover) | 100ms | Control fast |
| Track height shrink (hover -> rest) | 150ms | Decelerate |
| Thumb dot grow (rest -> hover) | 100ms | Control fast |
| Thumb dot grow (hover -> pressed) | 50ms | Linear |
| Thumb dot shrink (pressed -> rest) | 200ms | Decelerate |
| Value tooltip appear | 100ms | Decelerate |
| Value tooltip disappear | 50ms | Accelerate |

## Linux

### Appearance

A horizontal (or vertical) slider with a thin track and a circular thumb.

### Track

| Property | Light | Dark |
|----------|-------|------|
| Height | 4px | 4px |
| Corner radius | 2px (fully rounded) | 2px |
| Filled (left of thumb) | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Unfilled (right of thumb) | `rgba(0,0,0, 0.15)` | `rgba(255,255,255, 0.15)` |
| Fill level indicator | `--accent-bg-color` @ 0.5 | `--accent-bg-color` @ 0.5 |

### Thumb (Slider Handle)

| Property | Light | Dark |
|----------|-------|------|
| Diameter | 20px | 20px |
| Color | `#FFFFFF` | `#FFFFFF` |
| Border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Shadow | (0, 1) blur 2, black @ 0.10 | (0, 1) blur 2, black @ 0.10 |
| Corner radius | 10px (fully round) | 10px |
| Hit area | 34px diameter (invisible) | 34px |

### States

| State | Thumb | Track |
|-------|-------|-------|
| Rest | white, 20px | normal |
| Hover | white, slight border darken | normal |
| Active (dragging) | accent_bg_color, 20px | normal |
| Disabled | white, opacity 0.5 | opacity 0.5 |

#### Hover

| Property | Value |
|----------|-------|
| Thumb border | `rgba(0,0,0, 0.25)` (slightly stronger) |

#### Active (Dragging)

| Property | Value |
|----------|-------|
| Thumb color | `--accent-bg-color` (fills with accent) |
| Thumb border | none (accent fill covers) |

### Metrics

| Property | Value |
|----------|-------|
| Track height | 4px |
| Track corner radius | 2px |
| Thumb diameter | 20px |
| Hit area (thumb) | 34px |
| Min width (horizontal) | 100px |
| Total widget height | 34px (includes hit area) |
| Horizontal padding | 12px |

### Marks and Ticks

GtkScale supports marks (tick marks along the track):

| Property | Value |
|----------|-------|
| Mark height | 6px |
| Mark width | 1px |
| Mark color | `rgba(0,0,0, 0.20)` / `rgba(255,255,255, 0.20)` |
| Mark label font | `.caption` (13px) |
| Mark label color | dim-label color (secondary) |

### Value Display

| Property | Value |
|----------|-------|
| Value position | Above or below (configurable) |
| Value font | `.caption` (13px) |
| Draw value | Optional (default: off) |
| Value format | Configurable via signal |

### Orientation

| Orientation | Track Axis | Filled Direction |
|-------------|-----------|-----------------|
| Horizontal | Left to right | Left of thumb = filled |
| Vertical | Bottom to top | Below thumb = filled |
| Inverted | Reverses direction | Filled direction reverses |

### Focus

| Property | Value |
|----------|-------|
| Focus ring | 2px accent outline around thumb |
| Focus ring offset | 2px |
| Focus radius | thumb radius + 2px = 12px |

### Keyboard Support

| Key | Action |
|-----|--------|
| Left / Down | Decrease by step |
| Right / Up | Increase by step |
| Page Up / Page Down | Increase / decrease by page step |
| Home / End | Jump to min / max |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Thumb color change | 200ms | ease-in-out |
| Value change (keyboard) | immediate | -- |
| Value change (scroll) | immediate | -- |

### OSD Variant

When used with `.osd` style class (e.g., media player volume):

| Property | Value |
|----------|-------|
| Track height | 3px (thinner) |
| Trough visible | no |
| Background | transparent |
| Thumb | same, with OSD shadow |

### CSS Node Structure

```
scale[.horizontal/.vertical]
 +-- trough
 |    +-- slider (thumb)
 |    +-- highlight (filled portion)
 |    +-- fill (fill level, optional)
 +-- marks.top
 |    +-- mark
 |         +-- indicator
 |         +-- label
 +-- marks.bottom
      +-- mark
           +-- indicator
           +-- label
```
