# Linux (GNOME/Adwaita) — Progress Bar & Spinner (GtkProgressBar / GtkSpinner)

## GtkProgressBar

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Trough background | `rgba(0,0,0, 0.10)` | `rgba(255,255,255, 0.10)` |
| Fill (progress) | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Trough border | none | none |

### Metrics

| Property | Value |
|----------|-------|
| Height (default) | 6px |
| Height (OSD) | 4px |
| Corner radius | 3px (fully rounded) |
| Fill corner radius | 3px |
| Min width | 100px |

### Determinate Progress

```
[==========---------]  45%
 ^accent     ^trough
```

| Property | Value |
|----------|-------|
| Fill direction | Left to right (LTR) |
| Fill min-width | 2px (visible at any percentage > 0) |

### Indeterminate (Pulse) Mode

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

### OSD Variant

When `.osd` style class is applied:

| Property | Value |
|----------|-------|
| Height | 4px (thinner) |
| Trough | transparent (invisible) |
| Fill | accent color |
| Position | Typically at top of content area |
| Usage | Loading bars in media players, web browsers |

### Inverted

When `.inverted` is applied, fill direction reverses (right to left).

### Text Label

| Property | Value |
|----------|-------|
| Position | Centered above or below trough |
| Font | `.caption` (13px, Regular) |
| Show text | Optional (default: hidden) |
| Format | "45%" or custom |

## GtkSpinner

### Appearance

GtkSpinner displays a rotating arc animation.

| Property | Light | Dark |
|----------|-------|------|
| Color | `--accent-color` | `--accent-color` |
| Style | Circular arc, gap in circle | Same |

### Metrics

| Property | Value |
|----------|-------|
| Default size | 16x16px |
| Large size | 32x32px (set via width-request/height-request) |
| Line width | 2px (proportional to size) |
| Arc gap | ~90 degrees |

### Animation

| Property | Value |
|----------|-------|
| Rotation | 1050ms per full cycle |
| Easing | Linear (constant speed) |
| Start | Immediate when `spinning = true` |
| Stop | Immediate when `spinning = false` |

### Usage Guidelines

| Size | Usage |
|------|-------|
| 16x16px | Inline loading (next to text, in buttons) |
| 32x32px | Content area loading |
| 48x48px+ | Full page loading (with `AdwStatusPage`) |

For loading screens, GNOME recommends centering the spinner with `halign=CENTER`
and `valign=CENTER`, not placing it in a corner.

## AdwSpinner (libadwaita 1.6+)

libadwaita 1.6 introduced `AdwSpinner`, an improved spinner where both the icon
and animation are defined in CSS:

| Property | Value |
|----------|-------|
| Icon | Symbolic SVG (CSS-defined) |
| Animation | CSS animation |
| Sizing | Follows standard icon sizing |
| Color | Inherits current foreground color |

## Combined Usage Patterns

### Inline Button Loading

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

### Status Page Loading

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

## CSS Node Structure

### GtkProgressBar

```
progressbar[.horizontal/.vertical][.osd]
 +-- trough
 |    +-- progress[.pulse-left/.pulse-right]
 +-- text (optional)
```

### GtkSpinner

```
spinner[.spinning]
```

## Accessibility

| Widget | Role | States |
|--------|------|--------|
| GtkProgressBar | progressbar | value, min, max |
| GtkSpinner | status | busy when spinning |
| Text label | — | Live region (announces changes) |
