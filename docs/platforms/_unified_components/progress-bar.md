# Progress Bar

A horizontal indicator that shows the completion status of a task or process. Supports both determinate mode (known progress) and indeterminate mode (unknown duration with animated pattern).

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIProgressView | Documented |
| macOS | NSProgressIndicator (bar style) | Documented |
| Android | LinearProgressIndicator (Material Design 3) | Documented |
| Windows | ProgressBar | Documented |
| Linux | GtkProgressBar | Documented |

## iOS

Source: UIProgressView, SwiftUI ProgressView

### Styles

| Style | Height | Usage |
|-------|--------|-------|
| Default | 4pt | General progress indication |
| Bar | 2.5pt | Toolbars, navigation bars (e.g., Safari loading) |

### Track

| Property | Default Style | Bar Style |
|----------|--------------|-----------|
| Height | 4pt | 2.5pt |
| Corner radius | 2pt (fully rounded) | 1.25pt (fully rounded) |
| Background (unfilled) | systemFill (`#787880` @ 0.20 / @ 0.36) | systemFill |
| Filled color | tintColor (systemBlue default) | tintColor |
| Width | Full width of container | Full width of container |

### Colors

| Property | Light | Dark |
|----------|-------|------|
| Progress tint (default) | systemBlue (`#007AFF`) | systemBlue (`#0A84FF`) |
| Track tint (unfilled) | systemFill (`#787880` @ 0.20) | systemFill (`#787880` @ 0.36) |

Both `progressTintColor` and `trackTintColor` are fully customizable.

### Progress Value

| Property | Value |
|----------|-------|
| Range | 0.0 to 1.0 (clamped) |
| Default | 0.0 |
| Animation (setProgress animated) | ~0.25s ease-in-out |

### Indeterminate Progress (SwiftUI)

SwiftUI's `ProgressView()` without a value shows an indeterminate indicator. On iOS, this renders as a spinning `UIActivityIndicatorView` (not a progress bar). For a linear indeterminate bar, custom implementation is needed.

### Custom Images

UIProgressView supports custom images for both the progress and track:

| Property | Description |
|----------|-------------|
| `progressImage` | UIImage for the filled portion (stretched) |
| `trackImage` | UIImage for the unfilled portion (stretched) |

Images are resizable and stretched to fill their respective regions.

### Metrics (Summary)

```
Default style:
|==========================================|  <- 4pt height
  filled (tintColor)    unfilled (gray)
  <-------- progress ------><---- track --->

Bar style:
|==========================================|  <- 2.5pt height
```

### Animation

| Transition | Duration | Curve |
|-----------|----------|-------|
| Progress update (animated) | 0.25s | ease-in-out |
| Progress update (not animated) | Instant | -- |
| Fill direction | Left to right (LTR), right to left (RTL) | -- |

### Observed Value (SwiftUI)

SwiftUI `ProgressView` supports automatic progress tracking:

```swift
ProgressView(value: downloaded, total: totalSize) {
    Text("Downloading...")
} currentValueLabel: {
    Text("\(Int(downloaded))MB / \(Int(totalSize))MB")
}
```

| Property | Value |
|----------|-------|
| Label font | SF Pro Regular, 17pt (body) |
| Current value label font | SF Pro Regular, 13pt (footnote) |
| Label color | label |
| Value label color | secondaryLabel |
| Spacing (label to bar) | 4pt |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Progress indicator |
| VoiceOver | "[Label], [percentage]% complete" |
| Updates | VoiceOver announces significant changes |

## macOS

Reference: NSProgressIndicator, Apple HIG (macOS 14+).

### Overview

`NSProgressIndicator` with `.bar` style displays a horizontal progress bar. It supports both determinate (known progress) and indeterminate (unknown duration) modes. The bar style is the most common progress indicator in macOS.

### Styles

| Style            | Description                                              |
|------------------|----------------------------------------------------------|
| `.bar`           | Horizontal progress bar (this document)                  |
| `.spinning`      | Circular spinning indicator (see activity-indicator.md)   |

### Metrics

#### Determinate Bar

| Control Size | Height (pt) | Corner Radius (pt) | Min Width (pt) |
|-------------|-------------|---------------------|----------------|
| Mini        | 4           | 2 (capsule)         | 32             |
| Small       | 6           | 3 (capsule)         | 48             |
| Regular     | 6           | 3 (capsule)         | 64             |
| Large       | 8           | 4 (capsule)         | 64             |

The bar width is typically the full width of its container. Height is fixed per control size.

#### Indeterminate Bar

Same dimensions as determinate. The indeterminate bar shows an animated "barber pole" pattern -- diagonal stripes that scroll left to right continuously.

| Property                  | Value             |
|---------------------------|-------------------|
| Stripe width               | 12 pt            |
| Stripe angle               | ~30 degrees      |
| Animation speed            | ~40 pt/sec       |

### Colors

#### Track (Background)

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.10)`       |
| Disabled     | `rgba(0,0,0,0.04)`           | `rgba(255,255,255,0.05)`       |

#### Fill (Progress)

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | controlAccentColor (`#007AFF`)| controlAccentColor (`#0A84FF`) |
| Disabled     | controlAccentColor at 40%     | controlAccentColor at 40%      |

#### Indeterminate Stripes

| Element              | Light Mode                         | Dark Mode                          |
|----------------------|------------------------------------|------------------------------------|
| Stripe 1 (lighter)   | controlAccentColor at 70% opacity | controlAccentColor at 70% opacity  |
| Stripe 2 (darker)    | controlAccentColor at 100%        | controlAccentColor at 100%         |

### Border

| State        | Light Mode              | Dark Mode               |
|-------------|-------------------------|-------------------------|
| Normal       | `rgba(0,0,0,0.06)`     | `rgba(255,255,255,0.06)`|
| Disabled     | `rgba(0,0,0,0.03)`     | `rgba(255,255,255,0.03)`|

Border width: 0.5 pt.

### Progress Fill Corner Radius

The fill portion has the same corner radius as the track, minus the inset:

```
Fill corner radius = Track corner radius - 0.5 (border width)
```

When progress is very small (< 2x corner radius), the fill becomes a short capsule.

### Animation

#### Determinate

| Transition               | Duration (ms) | Curve         |
|-------------------------|---------------|---------------|
| Value change (smooth)    | 250           | Ease In Out   |
| Value jump (large delta) | 150           | Ease Out      |
| Appear                   | 200           | Fade in       |
| Disappear                | 200           | Fade out      |

#### Indeterminate

| Property                 | Value                          |
|--------------------------|--------------------------------|
| Stripe scroll speed       | ~40 pt/sec                    |
| Animation type            | Continuous linear scrolling   |
| Start animation           | Automatic when indeterminate  |
| Stop animation            | On `stopAnimation()` or hide  |

#### State Transitions

| Transition                      | Duration (ms) | Curve          |
|---------------------------------|---------------|----------------|
| Determinate -> Indeterminate    | 200           | Crossfade      |
| Indeterminate -> Determinate    | 200           | Crossfade      |
| Enable -> Disable               | 200           | Ease In Out    |
| Show -> Hide                    | 200           | Fade           |

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.progressIndicator`                      |
| Value        | Current progress (0.0 to 1.0)             |
| Min value    | 0.0                                       |
| Max value    | 1.0 (or `maxValue`)                      |
| Description  | "Progress" or custom label                 |

### Common Patterns

#### Linear Progress (file download, export)

```
[========================            ]  72%
```

Full width of container, optional percentage label to the right.

#### Inline Progress (toolbar, status bar)

```
Loading... [===========             ]
```

Smaller width, paired with a text description.

#### System Download Progress

For system-level downloads (App Store, Software Update), progress bars show:
- Determinate fill with smooth animation
- Gradient shimmer on the fill (subtle highlight sweep)
- Pause/resume support (striped pattern when paused)

### Dija Skin Mapping

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

## Android

Source: m3.material.io/components/progress-indicators/specs

### Variants

| Variant | Type | Description |
|---------|------|------------|
| Linear determinate | Horizontal bar | Known progress (file upload, download) |
| Linear indeterminate | Horizontal bar | Unknown duration (loading) |
| Circular determinate | Ring | Known progress (timer, loading %) |
| Circular indeterminate | Ring | Unknown duration (spinner) |

### Linear Progress Indicator

#### Metrics

| Property | Value |
|----------|-------|
| Track height | 4dp |
| Track corner radius | 2dp (rounded ends) |
| Active indicator corner radius | 2dp |
| Min width | 240dp (recommended) |
| Stop indicator diameter | 4dp |
| Gap between indicator and track | 4dp |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Active indicator | `#6750A4` (primary) | `#D0BCFF` |
| Track | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Stop indicator | `#6750A4` (primary) | `#D0BCFF` |

#### Determinate

- Active indicator width = progress percentage of total track width
- Stop indicator (4dp dot) at the end of the active track
- Gap between active indicator end and inactive track start

#### Indeterminate

- Two animated indicators slide across the track
- Animation cycle: Long 4 (600ms) per sweep
- Easing: Emphasized

### Circular Progress Indicator

#### Metrics

| Property | Value |
|----------|-------|
| Diameter | 48dp (default) |
| Track thickness (stroke) | 4dp |
| Track corner radius | 2dp (rounded cap) |
| Active indicator gap | 4dp |
| Padding | 4dp |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Active indicator | `#6750A4` (primary) | `#D0BCFF` |
| Track | `#E8DEF8` (secondaryContainer) | `#4A4458` |

#### Determinate

- Active arc length = progress percentage of full circle (360 degrees)
- Starts from 12 o'clock position
- Gap between active and inactive track arcs

#### Indeterminate

- Active arc grows and shrinks while rotating
- Rotation: continuous 360-degree, ~1333ms per revolution
- Arc sweep: oscillates between ~10 and ~270 degrees
- Easing: Standard

### Disabled State

| Element | Value |
|---------|-------|
| Active indicator | onSurface @ 38% |
| Track | onSurface @ 12% |

### Animation Details

#### Linear Indeterminate

```
Phase 1: First indicator enters from left, grows, exits right
Phase 2: Second indicator enters from left, overlaps, exits right
Cycle: ~2000ms total, repeating
```

#### Circular Indeterminate

```
Rotation: continuous clockwise, 1333ms per revolution
Arc length: grows from ~10deg to ~270deg, then shrinks
Head and tail move at different speeds
```

## Windows

Source: WinUI 3 ProgressBar, ProgressRing controls

### ProgressBar (Linear)

#### Track Metrics

| Property | Value |
|----------|-------|
| Height | 3px (default), 1px (indeterminate track portion) |
| Corner radius | 1.5px (fully rounded) |
| Track color (unfilled) | ControlStrongFillColorDefault (`#72000000` / `#9AFFFFFF`) |
| Fill color | AccentFillColorDefault (SystemAccentColor) |
| Width | Fills available horizontal space |

#### Determinate Mode

A solid fill bar that advances from left to right based on `Value` (0-100).

| Property | Value |
|----------|-------|
| Fill height | 3px |
| Fill corner radius | 1.5px |
| Fill color | AccentFillColorDefault |

#### Indeterminate Mode

An animated looping pattern where a short accent bar slides back and forth across the track.

| Property | Value |
|----------|-------|
| Track height | 1px |
| Moving bar height | 3px |
| Moving bar width | ~33% of total width |
| Animation duration | 2000ms per cycle |
| Animation curve | Ease (cubic-bezier(0.8, 0, 0.2, 1)) |

The indeterminate animation: the accent bar starts from the left, accelerates to the right, decelerates, then reverses. It creates a smooth oscillating motion.

#### Paused State

| Property | Value |
|----------|-------|
| Fill color | SystemFillColorCaution (`#9D5D00` / `#FCE100`) |
| Animation | Stopped (bar freezes in place) |

#### Error State

| Property | Value |
|----------|-------|
| Fill color | SystemFillColorCritical (`#C42B1C` / `#FF99A4`) |
| Animation | Stopped |

### ProgressRing (Circular)

#### Ring Metrics

| Property | Value |
|----------|-------|
| Default diameter | 32x32px |
| Min diameter | 20x20px (cannot go smaller) |
| Max diameter | Unlimited (scales with container) |
| Stroke width | 3px (scales proportionally) |
| Track color | ControlStrongFillColorDefault |
| Fill color | AccentFillColorDefault |

#### Determinate Mode

A circular arc that sweeps clockwise from the top (12 o'clock position).

| Property | Value |
|----------|-------|
| Start angle | 270 degrees (top/12 o'clock) |
| Sweep direction | Clockwise |
| Background ring | Full circle, track color |
| Fill arc | Partial circle, accent color |

#### Indeterminate Mode

A rotating partial arc that continuously spins.

| Property | Value |
|----------|-------|
| Arc length | ~90 degrees (varies during animation) |
| Rotation speed | ~3000ms per revolution |
| Arc expansion/contraction | The arc length grows and shrinks as it rotates |
| Animation curve | Ease-in-out for arc length, Linear for rotation |

The indeterminate ring animation combines:
1. Continuous clockwise rotation (linear, 3s cycle)
2. Arc length oscillation: sweeps between ~30 degrees and ~270 degrees (ease-in-out)

#### Paused and Error States

Same color mapping as ProgressBar (caution yellow for paused, critical red for error).

### Sizing Behavior

| Container | ProgressBar | ProgressRing |
|-----------|-------------|-------------|
| No explicit size | Fills width, 3px height | 32x32px default |
| Explicit width/height | Stretches to fill | Uses smaller of w/h |
| Min constraint | No width minimum | 20x20px minimum |

### Custom Foreground

Both controls accept a `Foreground` property to override the accent color for the fill.

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| ProgressBar value change | 200ms | Ease |
| ProgressBar indeterminate cycle | 2000ms | Ease |
| ProgressRing value change | 200ms | Ease |
| ProgressRing indeterminate spin | 3000ms | Linear (rotation) |
| ProgressRing arc oscillation | 1500ms | Ease-in-out |
| State change (normal -> paused/error) | 200ms | Control fast |

## Linux

### GtkProgressBar

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Trough background | `rgba(0,0,0, 0.10)` | `rgba(255,255,255, 0.10)` |
| Fill (progress) | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Trough border | none | none |

#### Metrics

| Property | Value |
|----------|-------|
| Height (default) | 6px |
| Height (OSD) | 4px |
| Corner radius | 3px (fully rounded) |
| Fill corner radius | 3px |
| Min width | 100px |

#### Determinate Progress

```
[==========---------]  45%
 ^accent     ^trough
```

| Property | Value |
|----------|-------|
| Fill direction | Left to right (LTR) |
| Fill min-width | 2px (visible at any percentage > 0) |

#### Indeterminate (Pulse) Mode

| Property | Value |
|----------|-------|
| Pulse block width | 25% of trough |
| Animation | Bouncing left-right |
| Duration | 750ms per half-cycle |
| Easing | ease-in-out |

```
Frame 0:  [===             ]
Frame 1:  [   ===          ]
Frame 2:  [        ===     ]
Frame 3:  [           ===  ]  (bounces back)
```

#### OSD Variant

When `.osd` style class is applied:

| Property | Value |
|----------|-------|
| Height | 4px (thinner) |
| Trough | transparent (invisible) |
| Fill | accent color |
| Position | Typically at top of content area |
| Usage | Loading bars in media players, web browsers |

#### Inverted

When `.inverted` is applied, fill direction reverses (right to left).

#### Text Label

| Property | Value |
|----------|-------|
| Position | Centered above or below trough |
| Font | `.caption` (13px, Regular) |
| Show text | Optional (default: hidden) |
| Format | "45%" or custom |

### GtkSpinner

#### Appearance

GtkSpinner displays a rotating arc animation.

| Property | Light | Dark |
|----------|-------|------|
| Color | `--accent-color` | `--accent-color` |
| Style | Circular arc, gap in circle | Same |

#### Metrics

| Property | Value |
|----------|-------|
| Default size | 16x16px |
| Large size | 32x32px (set via width-request/height-request) |
| Line width | 2px (proportional to size) |
| Arc gap | ~90 degrees |

#### Animation

| Property | Value |
|----------|-------|
| Rotation | 1050ms per full cycle |
| Easing | Linear (constant speed) |
| Start | Immediate when `spinning = true` |
| Stop | Immediate when `spinning = false` |

#### Usage Guidelines

| Size | Usage |
|------|-------|
| 16x16px | Inline loading (next to text, in buttons) |
| 32x32px | Content area loading |
| 48x48px+ | Full page loading (with `AdwStatusPage`) |

For loading screens, GNOME recommends centering the spinner with `halign=CENTER`
and `valign=CENTER`, not placing it in a corner.

### AdwSpinner (libadwaita 1.6+)

libadwaita 1.6 introduced `AdwSpinner`, an improved spinner where both the icon
and animation are defined in CSS:

| Property | Value |
|----------|-------|
| Icon | Symbolic SVG (CSS-defined) |
| Animation | CSS animation |
| Sizing | Follows standard icon sizing |
| Color | Inherits current foreground color |

### Combined Usage Patterns

#### Inline Button Loading

```
+----------------------------+
| [Spinner] Saving...        |
+----------------------------+
```

| Property | Value |
|----------|-------|
| Spinner size | 16px |
| Spinner-to-text gap | 6px |
| Button state | Insensitive during loading |

#### Status Page Loading

```
+----------------------------------+
|                                  |
|          [  Spinner  ]           |
|           (32-48px)              |
|                                  |
|       Loading content...         |
|                                  |
+----------------------------------+
```

### CSS Node Structure

#### GtkProgressBar

```
progressbar[.horizontal/.vertical][.osd]
 +-- trough
 |    +-- progress[.pulse-left/.pulse-right]
 +-- text (optional)
```

#### GtkSpinner

```
spinner[.spinning]
```

### Accessibility

| Widget | Role | States |
|--------|------|--------|
| GtkProgressBar | progressbar | value, min, max |
| GtkSpinner | status | busy when spinning |
| Text label | -- | Live region (announces changes) |
