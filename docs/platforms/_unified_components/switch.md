# Switch

A binary toggle control that allows the user to switch between an on and off state, typically rendered as a pill-shaped track with a sliding circular thumb.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UISwitch | Documented |
| macOS | NSSwitch | Documented |
| Android | Switch (Material Design 3) | Documented |
| Windows | ToggleSwitch | Documented |
| Linux | GtkSwitch | Documented |

## iOS

Source: UISwitch, SwiftUI Toggle

### Overall Size

| Property | Value |
|----------|-------|
| Width | 51pt |
| Height | 31pt |
| Corner radius | 15.5pt (fully rounded pill) |

### Track

| Property | Off (Light) | Off (Dark) | On |
|----------|-------------|------------|-----|
| Background | `#E9E9EB` (systemGray4-like) | `#39393D` | systemGreen (`#34C759` / `#30D158`) |
| Border | 0.5pt `#E0E0E0` (light) | none | none |
| Interior padding | 2pt (space between track edge and thumb) | -- | -- |

The track uses `systemFill` as the base off-state color in some contexts, but the visible result is close to the values above.

### Thumb

| Property | Value |
|----------|-------|
| Size (normal) | 27pt diameter |
| Size (pressed) | 27pt height x 31pt width (stretches horizontally) |
| Color | white (`#FFFFFF`) |
| Shadow | offset(0, 3) blur 8 spread 0, black @ 0.15 |
| Secondary shadow | offset(0, 3) blur 1 spread 0, black @ 0.06 |
| Corner radius | 13.5pt (fully rounded) |

### Animation

| Property | Value |
|----------|-------|
| Toggle duration | ~0.25s |
| Curve | Spring (damping 0.75, response 0.3) |
| Thumb expansion (press) | Grows to 31pt width in ~0.15s |
| Thumb expansion (release) | Shrinks back in ~0.2s |
| Track color transition | Cross-fade over ~0.15s |

#### Animation Sequence (Off -> On)

1. User touches: thumb expands width to 31pt (0.15s spring)
2. User releases (or drags past midpoint): thumb slides to right edge (0.25s spring)
3. Track cross-fades from gray to green (0.15s, starts slightly before thumb reaches end)
4. Thumb shrinks back to 27pt circle (0.2s spring)

### States

| State | Track | Thumb | Notes |
|-------|-------|-------|-------|
| Off | Gray background | Left position | |
| On | Green (or tintColor) background | Right position | |
| Pressed (off) | Gray background | Expanded, left | |
| Pressed (on) | Green background | Expanded, right | |
| Disabled (off) | Gray @ 0.5 opacity | Left, @ 0.5 opacity | Entire switch at reduced opacity |
| Disabled (on) | Green @ 0.5 opacity | Right, @ 0.5 opacity | |

### Custom Colors

| Property | Configurable |
|----------|-------------|
| `onTintColor` | Track color when on (default: systemGreen) |
| `thumbTintColor` | Thumb color (default: white) |
| `backgroundColor` (track off) | Track color when off (default: system gray) |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Switch |
| Minimum hit target | 51 x 31pt (already meets 44pt minimum on width, padded vertically) |
| VoiceOver | "Switch button, [label], [on/off]" |
| Haptic feedback | Light impact on toggle |

### SwiftUI Toggle Styles

In SwiftUI, Toggle has additional styles beyond the standard switch:

| Style | Description |
|-------|-------------|
| `.switch` | Standard UISwitch (default on iOS) |
| `.button` | Toggle as a tinted button |
| `.checkbox` | Checkbox (macOS only, not available on iOS) |

## macOS

Reference: NSSwitch (macOS 10.15+), Apple HIG (macOS 14+).

### Overview

`NSSwitch` was introduced in macOS 10.15 Catalina, bringing the iOS-style toggle switch to the Mac. It provides a binary on/off control that is visually distinct from checkboxes. It is NOT a subclass of NSButton -- it is its own control.

### Metrics

#### Track (Capsule)

| Control Size | Width (pt) | Height (pt) | Corner Radius (pt) |
|-------------|------------|-------------|---------------------|
| Mini        | 26         | 15          | 7.5 (capsule)       |
| Small       | 30         | 17          | 8.5 (capsule)       |
| Regular     | 38         | 22          | 11 (capsule)        |
| Large       | 46         | 26          | 13 (capsule)        |

#### Thumb (Knob)

The thumb is a circular knob that slides between off (left) and on (right) positions.

| Control Size | Diameter (pt) | Inset from Track (pt) |
|-------------|---------------|----------------------|
| Mini        | 13            | 1                    |
| Small       | 15            | 1                    |
| Regular     | 20            | 1                    |
| Large       | 24            | 1                    |

#### Thumb Shadow

```
Color:   rgba(0, 0, 0, 0.15)
Offset:  (0, 1) pt
Blur:    2 pt
```

### Colors

#### Track

| State            | Light Mode                         | Dark Mode                          |
|------------------|------------------------------------|------------------------------------|
| Off              | `rgba(0,0,0,0.09)`                | `rgba(255,255,255,0.10)`           |
| Off + Hover      | `rgba(0,0,0,0.12)`                | `rgba(255,255,255,0.14)`           |
| On               | controlAccentColor (`#007AFF`)     | controlAccentColor (`#0A84FF`)     |
| On + Hover       | controlAccentColor darkened 5%     | controlAccentColor lightened 5%    |
| On + Pressed     | controlAccentColor darkened 12%    | controlAccentColor lightened 10%   |
| Disabled Off     | `rgba(0,0,0,0.04)`                | `rgba(255,255,255,0.05)`           |
| Disabled On      | controlAccentColor at 40% opacity  | controlAccentColor at 40% opacity  |

#### Thumb (Knob)

| State            | Light Mode      | Dark Mode       |
|------------------|-----------------|-----------------|
| Normal           | `#FFFFFF`       | `#FFFFFF`       |
| Pressed          | `#F0F0F0`       | `#E8E8E8`       |
| Disabled         | `#F5F5F5`       | `#D0D0D0`       |

#### Border (Track)

| State            | Light Mode            | Dark Mode                 |
|------------------|-----------------------|---------------------------|
| Off              | `rgba(0,0,0,0.12)`   | `rgba(255,255,255,0.10)`  |
| On               | Transparent (filled)  | Transparent (filled)      |
| Disabled         | `rgba(0,0,0,0.06)`   | `rgba(255,255,255,0.05)`  |

Border width: 0.5 pt.

### States

| State        | Track                 | Thumb               | Notes                      |
|-------------|----------------------|---------------------|----------------------------|
| Off          | Gray fill            | Left position       |                            |
| On           | Accent color fill    | Right position      |                            |
| Off hover    | Slightly darker gray | Normal               |                            |
| On hover     | Slightly adjusted    | Normal               |                            |
| Pressed      | Same as current      | Slightly wider (squish) | Thumb expands ~2 pt wider  |
| Disabled     | Reduced opacity      | Dimmed               | No interaction             |
| Focused      | Focus ring           | Normal               | Keyboard navigation        |

#### Thumb Press Effect

When the thumb is pressed, it visually stretches in the direction of travel:
- Regular size: thumb width grows from 20 pt to ~24 pt
- The stretch is an ellipse, not a wider circle
- This gives a tactile "grabbable" feeling

### Animation

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

### Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from track bounds
Radius:   track corner radius + 3 pt (capsule + 3)
```

### Keyboard Interaction

| Key          | Action                                    |
|-------------|-------------------------------------------|
| Space        | Toggle on/off                             |
| Tab          | Move focus to next control                |
| Shift+Tab    | Move focus to previous control            |

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.switch`                                 |
| Value        | 0 (off) or 1 (on)                        |
| Label        | Associated label text                      |
| Traits       | `.togglable`                              |

### Dija Skin Mapping

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

## Android

Source: m3.material.io/components/switch/specs

### Track

| Property | Value |
|----------|-------|
| Width | 52dp |
| Height | 32dp |
| Corner radius | 16dp (full pill) |

#### Track Colors

| State | Light | Dark |
|-------|-------|------|
| Off | `#E7E0EC` (surfaceContainerHighest) | `#36343B` |
| Off (border) | `#79747E` (outline) | `#938F99` |
| On | `#6750A4` (primary) | `#D0BCFF` |
| Disabled off | `#E7E0EC` @ 12% | `#E6E0E9` @ 12% |
| Disabled on | `#1D1B20` @ 12% | `#E6E0E9` @ 12% |

Off track has a 2dp border (outline color). On track has no border.

### Thumb

| Property | Off | On | Pressed |
|----------|-----|-----|---------|
| Diameter | 16dp | 24dp | 28dp |
| Shape | Circle | Circle | Circle |

#### Thumb Colors

| State | Light | Dark |
|-------|-------|------|
| Off | `#79747E` (outline) | `#938F99` |
| On | `#FFFFFF` (onPrimary) | `#381E72` (onPrimary) |
| Disabled off | `#1D1B20` @ 38% | `#E6E0E9` @ 38% |
| Disabled on | `#FFFFFF` | `#322F35` |

### Thumb Icon

M3 switch supports an optional icon inside the thumb:

| State | Icon | Size |
|-------|------|------|
| Off (with icon) | Close (X) | 16dp |
| On (with icon) | Check | 16dp |

When icons are shown, the off-state thumb is 24dp (not 16dp) to accommodate the icon.

Icon colors:
- Off icon: `#E7E0EC` (surfaceContainerHighest)
- On icon: `#6750A4` (onPrimaryContainer)

### States

| State | Effect |
|-------|--------|
| Hovered | State layer 8% on thumb |
| Focused | State layer 10% on thumb |
| Pressed | Thumb grows to 28dp, state layer 10% |
| Disabled | Track and thumb at reduced opacity |

State layer is rendered as a 40dp circle centered on the thumb.

### Animation

- Thumb slide: Medium 1 (250ms), Standard easing
- Thumb size change: Short 4 (200ms), Standard easing
- Color transition: Short 4 (200ms)

### Metrics Summary

```
[  Track 52x32dp, radius 16dp                    ]
[  +---------+                    +---------+     ]
[  | thumb   |      OFF           | thumb   | ON  ]
[  | 16dp    |                    | 24dp    |     ]
[  +---------+                    +---------+     ]
```

Touch target: 48dp minimum height.

## Windows

Source: WinUI 3 ToggleSwitch control

### Track

| Property | Off (rest) | On (rest) |
|----------|-----------|-----------|
| Width | 40px | 40px |
| Height | 20px | 20px |
| Corner radius | 10px (fully rounded pill) |
| Fill (off) | ControlAltFillColorSecondary (`#06000000` / `#19FFFFFF`) | AccentFillColorDefault (SystemAccentColor) |
| Border (off) | ControlStrongStrokeColorDefault (`#72000000` / `#9AFFFFFF`) 1px | ControlStrokeColorOnAccentDefault 1px |
| Fill (on) | -- | AccentFillColorDefault |

### Knob (Thumb)

| Property | Off | On |
|----------|-----|-----|
| Diameter | 12px | 14px (grows on toggle) |
| Color | TextFillColorSecondary (`#9E000000` / `#C5FFFFFF`) | TextOnAccentFillColorPrimary (white/black) |
| Shape | Circle, centered vertically |
| Horizontal position | Left inset ~4px | Right inset ~4px |

The knob grows from 12px to 14px when the switch is in the "on" position.

### States

#### Off States

| State | Track fill | Track border | Knob |
|-------|-----------|-------------|------|
| Rest | ControlAltFillColorSecondary | ControlStrongStrokeColorDefault (1px) | 12px, TextFillColorSecondary |
| Hover | ControlAltFillColorTertiary | ControlStrongStrokeColorDefault (1px) | 14px, TextFillColorPrimary |
| Pressed | ControlAltFillColorQuarternary | ControlStrongStrokeColorDisabled (1px) | 17px wide (oval stretch), TextFillColorSecondary |
| Disabled | ControlAltFillColorDisabled | ControlStrongStrokeColorDisabled (1px) | 12px, TextFillColorDisabled |

#### On States

| State | Track fill | Track border | Knob |
|-------|-----------|-------------|------|
| Rest | AccentFillColorDefault | ControlStrokeColorOnAccentDefault (1px) | 14px, white |
| Hover | AccentFillColorSecondary | ControlStrokeColorOnAccentDefault (1px) | 14px, white |
| Pressed | AccentFillColorTertiary | ControlStrokeColorOnAccentTertiary (1px) | 17px wide (oval stretch), white |
| Disabled | AccentFillColorDisabled | transparent | 12px, TextOnAccentFillColorDisabled |

### Labels

| Property | Value |
|----------|-------|
| On label | "On" (localizable) |
| Off label | "Off" (localizable) |
| Font | 14px, Regular |
| Position | Right of track |
| Gap (track to label) | 8px |
| Header (optional) | Above the control, 14px Regular, 4px gap |

### Full Control Layout

```
Header label (optional)
+--------------------------+
| [===*]  On/Off label     |
+--------------------------+
```

Total control area:
- Min width: 154px (ThemeResource `ToggleSwitchThemeMinWidth`)
- Height: 32px (touch target)

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Knob slide (off -> on) | 200ms | Decelerate |
| Knob slide (on -> off) | 200ms | Decelerate |
| Track fill color change | 100ms | Control fast |
| Knob size change (rest -> hover) | 100ms | Control fast |
| Knob stretch (pressed) | 100ms | Control fast |
| Knob unstretch (release) | 150ms | Decelerate |

## Linux

### Appearance

Adwaita's switch is a compact pill-shaped toggle with a circular thumb.

### Track

| Property | Light | Dark |
|----------|-------|------|
| Width | 42px | 42px |
| Height | 26px | 26px |
| Corner radius | 13px (fully rounded) | 13px |
| Off background | `rgba(0,0,0, 0.15)` | `rgba(255,255,255, 0.15)` |
| On background | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Border (off) | 2px `rgba(0,0,0, 0.15)` | 2px `rgba(255,255,255, 0.15)` |
| Border (on) | none (accent fill covers) | none |

### Thumb (Slider)

| Property | Value |
|----------|-------|
| Diameter | 20px |
| Color | `#FFFFFF` |
| Shadow | (0, 1) blur 2, black @ 0.10 |
| Corner radius | 10px (fully round) |
| Horizontal margin | 3px from track edge |

### States

| State | Track | Thumb |
|-------|-------|-------|
| Off (rest) | `rgba(0,0,0, 0.15)` | Left position |
| Off (hover) | `rgba(0,0,0, 0.22)` | Left position |
| Off (active) | `rgba(0,0,0, 0.30)` | Left position |
| On (rest) | accent_bg_color | Right position |
| On (hover) | accent_bg_color, lightened ~8% | Right position |
| On (active) | accent_bg_color, darkened ~8% | Right position |
| Disabled (off) | `rgba(0,0,0, 0.08)` | Left, opacity 0.5 |
| Disabled (on) | accent @ 0.5 | Right, opacity 0.5 |

### Focus

| Property | Value |
|----------|-------|
| Focus ring | 2px `--accent-color`, 2px offset |
| Focus ring radius | track radius + 2px = 15px |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Thumb slide | 250ms | ease-in-out |
| Track color change | 250ms | ease-in-out |
| Hover color change | 200ms | ease-in-out |

### Keyboard Support

| Key | Action |
|-----|--------|
| Space | Toggle switch |
| Enter | Toggle switch |
| Tab | Move focus |

### Metrics Summary

```
Track:  42 x 26px, radius 13px
Thumb:  20 x 20px, radius 10px
Margin: 3px inset from track edge

Off:    [O          ]  thumb at x=3
On:     [          O]  thumb at x=19 (42 - 20 - 3)
```

### CSS Node Structure

```
switch
 +-- image (optional, for slider icon)
```

### Dija Skin Mapping

```
skin! {
    SwitchSkin {
        field track
        field thumb

        platform linux {
            light {
                track: {
                    width: 42, height: 26,
                    border_radius: 13,
                    background: rgba(0,0,0,0.15),
                    border: 2 rgba(0,0,0,0.15),
                }
                thumb: {
                    width: 20, height: 20,
                    border_radius: 10,
                    background: #FFFFFF,
                    shadow: 0 1 2 0 rgba(0,0,0,0.10),
                }
            }
        }
    }
}
```
