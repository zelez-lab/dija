# iOS — Activity Indicator (UIActivityIndicatorView)

Source: UIActivityIndicatorView, SwiftUI ProgressView (indeterminate)

## Styles and Sizes

| Style | Size | Usage |
|-------|------|-------|
| Medium | 20 x 20pt | Inline loading, buttons, cells |
| Large | 37 x 37pt | Full-screen loading, empty states |

The sizes are fixed for each style and should not be scaled (scaling causes blurriness).

## Appearance

| Property | Medium | Large |
|----------|--------|-------|
| Diameter | 20pt | 37pt |
| Line width | ~2pt | ~3pt |
| Spoke count | 8 | 8 |
| Color (default, light mode) | systemGray (`#8E8E93`) | systemGray |
| Color (default, dark mode) | systemGray (`#8E8E93`) | systemGray |

The default color is `systemGray`, but it can be customized via the `color` property.

## Animation

| Property | Value |
|----------|-------|
| Rotation speed | 1 full rotation per ~1.0s |
| Animation type | Stepped rotation (not smooth) |
| Steps | 8 discrete positions per rotation |
| Step duration | ~0.125s per step |
| Opacity gradient | Leading spokes are brighter, trailing spokes fade |
| Start | `startAnimating()` — begins spinning |
| Stop | `stopAnimating()` — stops and optionally hides |

### Spoke Opacity

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

## Behavior

| Property | Value |
|----------|-------|
| `hidesWhenStopped` | `true` (default) — hides when not animating |
| Auto-start | No — must call `startAnimating()` explicitly |
| Thread safety | Must be called on main thread |

## Common Patterns

### Inline (in button)

| Property | Value |
|----------|-------|
| Style | Medium |
| Color | Match button text color |
| Position | Replaces button title or icon |

### Full-screen Loading

| Property | Value |
|----------|-------|
| Style | Large |
| Background | Dimmed overlay (black @ 0.3) or material |
| Position | Centered on screen |
| Label | Optional "Loading..." below |
| Label font | SF Pro Regular, 17pt |
| Label color | secondaryLabel |
| Spacing (spinner to label) | 12pt |

### Pull to Refresh

The refresh control uses a similar spinning indicator:

| Property | Value |
|----------|-------|
| Diameter | ~20pt |
| Color | secondaryLabel (default), customizable |
| Pull distance to trigger | ~60pt |
| Animation | Spokes appear progressively during pull, then spin |

## SwiftUI ProgressView (Indeterminate)

`ProgressView()` without a value creates an indeterminate spinner:

| Property | Value |
|----------|-------|
| Default style | Same as UIActivityIndicatorView.medium |
| Label | Optional, displayed to the right |
| Tint | Follows accent color if set |

## Accessibility

| Property | Value |
|----------|-------|
| Role | Activity indicator |
| VoiceOver | "In progress" (when animating) |
| Trait | Updates automatically (announces when starts/stops) |
