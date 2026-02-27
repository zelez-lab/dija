# iOS — Navigation Bar (UINavigationBar)

Source: UINavigationBar, UINavigationItem, SwiftUI NavigationStack

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background (scrolled to top) | Material Regular (translucent) | Material Regular |
| Background (content scrolled under) | Solid systemBackground | Solid `#000000` (elevated: `#1C1C1E`) |
| Bottom separator (at rest) | Hidden | Hidden |
| Bottom separator (scrolled) | 0.33pt separator color | 0.33pt separator color |
| Tint color (bar buttons) | systemBlue | systemBlue |

The navigation bar is transparent/material at rest and transitions to a solid opaque surface when content scrolls underneath it.

## Height

| Configuration | Height | Notes |
|--------------|--------|-------|
| Standard title | 44pt | Fixed |
| Large title (expanded) | 96pt | Title below bar buttons |
| Large title (collapsed) | 44pt | Same as standard after scroll |
| Total (with status bar) | 44pt + status bar height | Status bar: 54pt (Dynamic Island), 47pt (notch), 20pt (legacy) |

## Title

| Style | Font | Weight | Size | Color | Alignment |
|-------|------|--------|------|-------|-----------|
| Standard | SF Pro | Semibold | 17pt | label | Centered |
| Large | SF Pro | Bold | 34pt | label | Left-aligned, below bar buttons |
| Large (search visible) | SF Pro | Bold | 34pt | label | Left-aligned |

### Large Title Behavior

| Property | Value |
|----------|-------|
| Collapse threshold | ~50pt of scroll |
| Collapse animation | Smooth, tied to scroll offset (not spring) |
| Expand animation | Smooth, reverse of collapse |
| Large title left inset | 20pt |
| Large title bottom padding | 8pt |
| Transition | Title slides up and scales down to centered 17pt |

## Bar Buttons

| Property | Value |
|----------|-------|
| Font | SF Pro Regular, 17pt (text buttons) |
| Bold font | SF Pro Semibold, 17pt (emphasized/done buttons) |
| Icon size | SF Symbol, 22pt (medium weight) |
| Color | tintColor (systemBlue default) |
| Hit area | 44 x 44pt minimum |
| Spacing between buttons | 8pt |
| Left/right margin | 8pt from screen edge, 16pt content inset |

### Back Button

| Property | Value |
|----------|-------|
| Icon | Chevron left (SF Symbol: `chevron.backward`) |
| Icon size | ~21pt height |
| Title | Previous screen's title (or "Back") |
| Title font | SF Pro Regular, 17pt |
| Color | tintColor |
| Max title width | ~2/3 of bar width, then ellipsis or hidden |
| Hit area | 44 x 44pt (extends right of chevron) |
| Swipe-back gesture | Interactive edge swipe from left 20pt |

## Search Bar Integration

When a search bar is attached to the navigation bar:

| Property | Value |
|----------|-------|
| Position | Below large title, above content |
| Visibility | Hidden by default, revealed on pull-down |
| Background | tertiarySystemFill in a rounded rect |
| Corner radius | 10pt |
| Height | 36pt |
| Animation | Slides down from under navigation bar |
| Cancel button | Appears right of search bar on focus |
| Cancel font | SF Pro Regular, 17pt |
| Cancel color | tintColor |

## Navigation Transitions

| Transition | Duration | Curve |
|-----------|----------|-------|
| Push | 0.35s | ease-in-out (interactive: matches gesture) |
| Pop | 0.35s | ease-in-out (interactive: matches gesture) |
| Interactive pop (swipe) | Gesture-driven | Linear with gesture, then spring to complete/cancel |
| Title crossfade | 0.2s | Fade during push/pop |

### Push Animation Details

1. New view slides in from right edge
2. Current view slides left and dims slightly (parallax: moves ~1/3 speed)
3. Back button chevron slides in from left
4. New title fades in, old title fades out
5. If large title: new large title slides up into position

## Toolbar

A toolbar can appear at the bottom of the navigation controller.

| Property | Value |
|----------|-------|
| Height | 44pt (78pt with safe area) |
| Background | Material Regular (same as navigation bar) |
| Top separator | 0.33pt separator color |
| Button spacing | Flexible (equally distributed) |
| Button font | SF Pro Regular, 17pt |
| Button color | tintColor |

## Accessibility

| Property | Value |
|----------|-------|
| Back button | "Back" or previous title, button trait |
| Title | Header trait |
| VoiceOver navigation | Adjustable (swipe up/down to navigate sections) |
