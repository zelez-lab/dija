# Spinner

An animated indicator that shows an ongoing process of indeterminate duration, signaling that the app is working.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIActivityIndicatorView | Documented |
| macOS | NSProgressIndicator (spinning) | Documented |
| Android | CircularProgressIndicator (indeterminate) | Documented |
| Windows | ProgressRing | Documented |
| Linux | AdwSpinner | Documented |

## iOS

Source: UIActivityIndicatorView, SwiftUI ProgressView (indeterminate)

### Styles and Sizes

| Style | Size | Usage |
|-------|------|-------|
| Medium | 20 x 20pt | Inline loading, buttons, cells |
| Large | 37 x 37pt | Full-screen loading, empty states |

The sizes are fixed for each style and should not be scaled (scaling causes blurriness).

### Appearance

| Property | Medium | Large |
|----------|--------|-------|
| Diameter | 20pt | 37pt |
| Line width | ~2pt | ~3pt |
| Spoke count | 8 | 8 |
| Color (default, light mode) | systemGray (`#8E8E93`) | systemGray |
| Color (default, dark mode) | systemGray (`#8E8E93`) | systemGray |

The default color is `systemGray`, but it can be customized via the `color` property.

### Animation

| Property | Value |
|----------|-------|
| Rotation speed | 1 full rotation per ~1.0s |
| Animation type | Stepped rotation (not smooth) |
| Steps | 8 discrete positions per rotation |
| Step duration | ~0.125s per step |
| Opacity gradient | Leading spokes are brighter, trailing spokes fade |
| Start | `startAnimating()` — begins spinning |
| Stop | `stopAnimating()` — stops and optionally hides |

#### Spoke Opacity

The 8 spokes have varying opacity to create the spinning illusion:

| Spoke (from current) | Opacity |
|-----------------------|---------|
| 0 (brightest) | 1.0 |
| 1 | 0.85 |
| 2 | 0.70 |
| 3 | 0.55 |
| 4 | 0.40 |
| 5 | 0.30 |
| 6 | 0.20 |
| 7 | 0.12 |

### Behavior

| Property | Value |
|----------|-------|
| `hidesWhenStopped` | `true` (default) — hides when not animating |
| Auto-start | No — must call `startAnimating()` explicitly |
| Thread safety | Must be called on main thread |

### Common Patterns

#### Inline (in button)

| Property | Value |
|----------|-------|
| Style | Medium |
| Color | Match button text color |
| Position | Replaces button title or icon |

#### Full-screen Loading

| Property | Value |
|----------|-------|
| Style | Large |
| Background | Dimmed overlay (black @ 0.3) or material |
| Position | Centered on screen |
| Label | Optional "Loading..." below |
| Label font | SF Pro Regular, 17pt |
| Label color | secondaryLabel |
| Spacing (spinner to label) | 12pt |

#### Pull to Refresh

The refresh control uses a similar spinning indicator:

| Property | Value |
|----------|-------|
| Diameter | ~20pt |
| Color | secondaryLabel (default), customizable |
| Pull distance to trigger | ~60pt |
| Animation | Spokes appear progressively during pull, then spin |

### SwiftUI ProgressView (Indeterminate)

`ProgressView()` without a value creates an indeterminate spinner:

| Property | Value |
|----------|-------|
| Default style | Same as UIActivityIndicatorView.medium |
| Label | Optional, displayed to the right |
| Tint | Follows accent color if set |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Activity indicator |
| VoiceOver | "In progress" (when animating) |
| Trait | Updates automatically (announces when starts/stops) |

## macOS

Reference: NSProgressIndicator (spinning style), Apple HIG (macOS 14+).

### Overview

The spinning activity indicator is a circular indicator used when the duration of an operation is unknown. It is `NSProgressIndicator` with `.spinning` style. This is the classic macOS "spinner" seen throughout the system.

### Variants

#### Indeterminate Spinning (most common)

A circular ring of fading segments that rotates continuously. This is the standard "loading" indicator.

#### Determinate Spinning (less common)

A circular ring that fills clockwise to show progress. Less commonly used; most apps prefer the bar-style for determinate progress.

### Metrics

#### Size

| Control Size | Diameter (pt) | Line Width (pt) |
|-------------|---------------|-----------------|
| Mini        | 10            | 1.5             |
| Small       | 16            | 2               |
| Regular     | 32            | 2.5             |
| Large       | 48 (custom)   | 3               |

Note: The "standard" macOS spinner sizes are 16 and 32 pt. Mini (10) and Large (48) are less common.

#### Segment Geometry

The spinner consists of 12 radial segments (lines or rounded capsules) arranged in a circle.

| Property                | Value           |
|-------------------------|-----------------|
| Number of segments       | 12              |
| Segment shape            | Rounded capsule |
| Rotation per frame       | 30 degrees (360/12) |
| Full rotation period     | ~1000 ms        |
| Frame interval           | ~83 ms per step |

#### Segment Dimensions (Regular, 32 pt)

| Property                | Value           |
|-------------------------|-----------------|
| Segment length           | 8 pt            |
| Segment width            | 2.5 pt          |
| Segment corner radius    | 1.25 pt (capsule) |
| Inner radius (gap)       | 4 pt            |
| Outer radius             | 12 pt           |

### Colors

#### Segment Colors

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

#### Base Color

| Context              | Light Mode              | Dark Mode               |
|---------------------|-------------------------|-------------------------|
| On opaque background | `#4D4D4D` (dark gray)  | `#C8C8C8` (light gray)  |
| On vibrant surface   | labelColor (auto)       | labelColor (auto)        |
| Tinted / accent      | controlAccentColor      | controlAccentColor       |
| Disabled             | `rgba(0,0,0,0.15)`     | `rgba(255,255,255,0.15)` |

The base color is multiplied by the per-segment opacity values above.

### Animation

#### Indeterminate Rotation

| Property                | Value                    |
|-------------------------|--------------------------|
| Rotation direction       | Clockwise               |
| Step interval            | 83 ms (12 fps)          |
| Step size                | 30 degrees              |
| Full revolution          | ~1000 ms                |
| Start behavior           | Automatic on display     |
| Stop behavior            | Fades out on hide        |

Note: The spinner does NOT use smooth continuous rotation. It uses discrete 30-degree steps, giving it the characteristic macOS spinner look.

#### Determinate Fill (Circular)

When used as a determinate circular indicator:

| Property                | Value                    |
|-------------------------|--------------------------|
| Fill direction           | Clockwise from 12 o'clock |
| Track color              | `rgba(0,0,0,0.08)` light / `rgba(255,255,255,0.10)` dark |
| Fill color               | controlAccentColor        |
| Stroke width             | Line width from size table |
| Fill animation           | 250 ms ease-in-out per update |

#### Show/Hide Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Show (fade in)       | 200           | Ease Out      |
| Hide (fade out)      | 200           | Ease In       |
| Start spinning       | Immediate     | N/A           |
| Stop spinning        | Last frame holds, then fades | 200 ms |

### States

| State           | Visual Changes                              |
|-----------------|---------------------------------------------|
| Spinning        | Continuous rotation animation               |
| Stopped         | Static (last position) or hidden             |
| Hidden          | Not visible, no animation running            |
| Disabled        | Dimmed, may or may not animate               |

### Usage Patterns

#### Inline Loading

Small spinner next to text:

```
[*] Loading items...
```

- Spinner: 16 pt (small)
- Text: 13 pt body, labelColor
- Gap: 6 pt between spinner and text

#### Full-Area Loading

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

#### Button Loading State

Replace button content with spinner:

- Spinner size matches button's font size (13 pt regular)
- Spinner is white on accent-colored buttons
- Spinner is labelColor on standard buttons
- Button disabled during loading

#### Toolbar Loading

Status bar or toolbar spinner:

- Spinner: 16 pt (small)
- Color: secondaryLabelColor
- No label

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.progressIndicator`                      |
| Trait        | Indeterminate                             |
| Description  | "Loading" or custom label                  |
| Value        | None (indeterminate) or 0.0-1.0 (determinate) |

### Dija Skin Mapping

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

## Android

Source: Material Design 3 (M3), CircularProgressIndicator (indeterminate mode), material-components-android.

### Overview

The M3 CircularProgressIndicator in indeterminate mode displays a circular arc that continuously grows, shrinks, and rotates to signal ongoing work. Unlike the spoke-based iOS/macOS spinners, Android uses a single smooth arc on a circular track.

### Anatomy

| Element | Description |
|---------|-------------|
| Active indicator | Animated arc that sweeps along the circular track |
| Track | Background circular ring behind the active indicator |
| Gap | Space between active indicator ends and track |
| Stop indicator | Small dot at the start of the active indicator (M3 2023+) |

### Metrics

| Property | Value |
|----------|-------|
| Overall diameter | 48dp (default) |
| Indicator radius (from axial line) | 18dp |
| Inset (padding around ring) | 4dp |
| Track thickness | 4dp |
| Active indicator thickness | 4dp |
| Stroke cap | Round |
| Gap size (indicator to track) | 4dp (M3 2023+) |
| Stop indicator diameter | 4dp (M3 2023+) |
| Touch target | 48dp minimum |

### Colors

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Active indicator | `md.comp.circular-progress-indicator.active-indicator.color` | primary | primary |
| Track | `md.comp.circular-progress-indicator.track.color` | surfaceContainerHighest | surfaceContainerHighest |

The active indicator color defaults to the theme's `primary` color. The track was transparent in earlier M3 versions but defaults to `surfaceContainerHighest` in the M3 2023 update.

#### Typical Color Values (M3 Baseline)

| Element | Light | Dark |
|---------|-------|------|
| Active indicator | `#6750A4` (primary) | `#D0BCFF` (primary) |
| Track | `#E6E1E5` (surfaceContainerHighest) | `#49454F` (surfaceContainerHighest) |

### Animation

| Property | Value |
|----------|-------|
| Animation type | Smooth arc sweep (not stepped) |
| Rotation | Continuous clockwise rotation |
| Full rotation period | ~1333 ms (one outer rotation cycle) |
| Expand phase | Arc grows from ~0 to ~315 degrees |
| Shrink phase | Arc shrinks from ~315 to ~0 degrees |
| Head/tail movement | Head advances first (expand), then tail catches up (shrink) |
| Overall cycle | Expand + shrink + rotate forms a continuous loop |
| Easing | Standard M3 easing (cubic-bezier) |

The indeterminate animation combines two motions: the arc length oscillates between a minimum (~10 degrees) and maximum (~315 degrees), while the entire indicator rotates continuously. This creates the characteristic "breathing" sweep effect.

### States

| State | Visual |
|-------|--------|
| Active | Animated sweep + rotation |
| Inactive | Hidden or static |
| Disabled | Not applicable (hide instead) |

### Usage Patterns

#### Inline Loading

| Property | Value |
|----------|-------|
| Diameter | 24dp or 48dp |
| Position | Centered in content area or next to text |
| Track visibility | Visible (surfaceContainerHighest) |

#### Full-Screen Loading

| Property | Value |
|----------|-------|
| Diameter | 48dp (default) |
| Position | Centered on screen |
| Label | Optional "Loading..." below |
| Label font | Body Medium (Roboto 400, 14sp) |
| Label color | onSurfaceVariant |
| Spacing (spinner to label) | 16dp |

#### Button Loading

| Property | Value |
|----------|-------|
| Diameter | 24dp (reduced) |
| Track thickness | 3dp |
| Color | Match button content color (onPrimary for filled buttons) |
| Position | Replaces button label or icon |

### Accessibility

| Property | Value |
|----------|-------|
| Role | ProgressBar (indeterminate) |
| Content description | "Loading" or custom label |
| TalkBack | Announces "In progress" when visible |
| Live region | None by default (set if dynamically shown) |

## Windows

Source: WinUI 3, ProgressRing (Windows App SDK), Fluent Design System.

### Overview

The WinUI ProgressRing is a circular indeterminate progress indicator that displays an animated arc sweeping around a ring. It follows Fluent Design principles with smooth motion and system accent color integration. It supports both indeterminate (repeating animation) and determinate (fill-based) modes.

### Anatomy

| Element | Description |
|---------|-------------|
| Ring track | Circular background ring (subtle, low-contrast) |
| Active arc | Animated indicator arc that sweeps around the track |

### Metrics

| Property | Value |
|----------|-------|
| Default size | 32 x 32 epx |
| Minimum size | 20 x 20 epx |
| Maximum size | Unbounded (scales with container) |
| Stroke width | Proportional to ring size (~3 epx at 32x32) |
| Stroke cap | Round |

Size is set via `Width` and `Height` properties. If only one dimension is set, the control uses the minimum 20x20. If both are set to different values, the smaller dimension is used.

### Colors

| Element | Light Mode | Dark Mode |
|---------|------------|-----------|
| Active arc (foreground) | SystemAccentColor | SystemAccentColor |
| Ring track (background) | `ControlStrongFillColorDefault` (subtle gray) | `ControlStrongFillColorDefault` (subtle gray) |
| Disabled foreground | `TextFillColorDisabled` | `TextFillColorDisabled` |

The foreground color is customizable via the `Foreground` property. Theme resources used:

| Resource Key | Purpose |
|-------------|---------|
| `ProgressRingForegroundThemeBrush` | Active arc color |
| `ProgressRingIndeterminateForegroundThemeBrush` | Indeterminate arc color |
| `ProgressRingBackgroundThemeBrush` | Track background |

### Animation

| Property | Value |
|----------|-------|
| Animation type | Smooth arc sweep (continuous rotation) |
| Rotation direction | Clockwise |
| Arc behavior | Expands and contracts while rotating |
| Full cycle period | ~2000 ms |
| Easing | Fluent motion curves (decelerate / accelerate) |
| Start behavior | Automatic when `IsActive = true` (default) |
| Stop behavior | Fades out smoothly |

#### Show/Hide Transitions

| Transition | Duration | Curve |
|-----------|----------|-------|
| Show (fade in) | ~200 ms | Ease Out |
| Hide (fade out) | ~200 ms | Ease In |

### States

| State | Description |
|-------|-------------|
| Active (indeterminate) | Arc sweeps continuously around the ring |
| Active (determinate) | Arc fills proportionally to `Value` (0.0-100.0) |
| Inactive | Hidden, no animation |
| Disabled | Dimmed, no animation |

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `IsActive` | bool | `true` | Whether the ring is visible and animating |
| `IsIndeterminate` | bool | `true` | `true` = repeating animation, `false` = fill-based |
| `Value` | double | 0 | Progress value (0-100, determinate mode only) |
| `Minimum` | double | 0 | Minimum value |
| `Maximum` | double | 100 | Maximum value |

### Usage Patterns

#### Inline Loading

| Property | Value |
|----------|-------|
| Size | 16 x 16 or 20 x 20 epx |
| Position | Next to text or replacing content |
| Color | SystemAccentColor or match surrounding text |

#### Full-Area Loading

| Property | Value |
|----------|-------|
| Size | 32 x 32 epx (default) or larger |
| Position | Centered in content area |
| Label | Optional "Loading..." below |
| Label font | Segoe UI Variable, 14px |
| Label color | TextFillColorSecondary |
| Spacing (ring to label) | 12 epx |

#### Button Loading

| Property | Value |
|----------|-------|
| Size | 16 x 16 epx |
| Color | Match button foreground color |
| Position | Replaces button content |
| Button state | Disabled during loading |

### Accessibility

| Property | Value |
|----------|-------|
| Role | ProgressBar |
| UIA pattern | RangeValue (determinate) or none (indeterminate) |
| Narrator | "Busy" when indeterminate, "X percent" when determinate |
| Live region | Polite (announces changes) |

## Linux

Source: AdwSpinner (libadwaita 1.6+), GNOME HIG.

### Overview

AdwSpinner is the modern Adwaita spinner widget, introduced in libadwaita 1.6. It replaces the legacy GtkSpinner with a custom-drawn, resolution-independent animation. Unlike GtkSpinner (which used a CSS-animated icon), AdwSpinner uses custom paintable rendering for a smoother, more consistent appearance. It continues to spin even when system animations are disabled (accessibility consideration).

### Anatomy

| Element | Description |
|---------|-------------|
| Animated arcs | Custom-drawn sweeping arcs that rotate and pulse |

AdwSpinner uses custom drawing (not an icon or CSS animation). The visual is a series of arcs or segments rendered directly via GTK snapshot, giving GNOME full control over the animation.

### Metrics

| Property | Value |
|----------|-------|
| Default size | 48 x 48 px |
| Minimum size | Scales down (no hard minimum) |
| Maximum size | 64 x 64 px (capped for usability) |
| Scales with container | Yes, up to the 64 px cap |

Note: The legacy GtkSpinner defaults to 16 x 16 px and requires explicit `width-request` / `height-request` to resize. AdwSpinner is larger by default.

### Colors

| Element | Light Mode | Dark Mode |
|---------|------------|-----------|
| Spinner arcs | `@window_fg_color` (dark gray/black) | `@window_fg_color` (light gray/white) |

AdwSpinner uses the foreground color from the current Adwaita theme context. It cannot be themed via CSS because it uses custom drawing instead of icon + CSS. The Ubuntu Yaru theme team has noted this as a limitation (theming requires patching source).

#### Typical Color Values (Adwaita Default)

| Context | Light | Dark |
|---------|-------|------|
| Window foreground | `#3D3846` | `#FFFFFF` |
| On dark surface | `#FFFFFF` | `#FFFFFF` |

### CSS Node

AdwSpinner has a single CSS node:

| Node name | Style class |
|-----------|-------------|
| `image` | `.spinner` |

### Animation

| Property | Value |
|----------|-------|
| Animation type | Custom-drawn arc sweep (smooth, not stepped) |
| Rotation | Continuous |
| Full cycle period | ~1000 ms |
| Respects animation setting | Partially — keeps spinning even with animations off |
| Start behavior | Automatic when widget is mapped (visible) |
| Stop behavior | Stops when unmapped (hidden) |

Unlike GtkSpinner's simple icon rotation, AdwSpinner's animation is more elaborate: arcs expand, contract, and rotate in a fluid pattern similar to the Material Design spinner, adapted to the Adwaita visual language.

### States

| State | Visual |
|-------|--------|
| Spinning | Continuous arc animation |
| Unmapped | Not visible, animation paused |

AdwSpinner does not have explicit start/stop API — it spins whenever it is visible (mapped) and stops when hidden (unmapped).

### Related: AdwSpinnerPaintable

`AdwSpinnerPaintable` is a `GdkPaintable` variant of the same spinner animation. It can be used with:

- `GtkImage` (set as paintable)
- Status pages (`AdwStatusPage`)
- Any widget that accepts `GdkPaintable`
- Manual drawing via snapshot

### Related: GtkSpinner (Legacy)

GtkSpinner is the older GTK4 spinner, still available but superseded by AdwSpinner in GNOME apps.

| Property | GtkSpinner | AdwSpinner |
|----------|-----------|------------|
| Default size | 16 x 16 px | 48 x 48 px |
| Max size | Unbounded | 64 x 64 px |
| Rendering | CSS icon animation | Custom paintable drawing |
| Themeable via CSS | Yes | No |
| Animation when disabled | Stops | Keeps spinning |
| API | `start()` / `stop()` + `spinning` property | Automatic (visible = spinning) |

### Usage Patterns

#### Inline Loading

| Property | Value |
|----------|-------|
| Size | 16 x 16 or 24 x 24 px |
| Position | Next to label text |
| Gap | 8 px between spinner and text |

#### Full-Area Loading

| Property | Value |
|----------|-------|
| Size | 48 x 48 px (default) |
| Position | Centered in content area |
| Label | Optional, below spinner |
| Label font | Cantarell Regular, 14px |
| Label color | `@window_fg_color` at reduced opacity |
| Gap | 12 px between spinner and label |

#### Status Page

AdwStatusPage integrates the spinner via AdwSpinnerPaintable:

| Property | Value |
|----------|-------|
| Spinner size | 48 x 48 px or 64 x 64 px |
| Title below | Optional descriptive text |
| Description below title | Optional secondary text |
| Vertical spacing | 12 px |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Widget (image) |
| ATK/AT-SPI | Announces as "spinner" |
| Screen reader | "Loading" or label text |
| Animation override | Keeps spinning even when system animations are off |
