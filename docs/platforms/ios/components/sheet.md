# iOS — Bottom Sheet (UISheetPresentationController)

Source: UISheetPresentationController (iOS 15+), SwiftUI `.sheet` / `.presentationDetents`

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | systemBackground (`#FFFFFF`) | secondarySystemBackground (`#1C1C1E`) |
| Corner radius | 10pt (top-left and top-right only) | 10pt |
| Corner curve | `.continuous` (superellipse) | |
| Shadow | offset(0, -10) blur 40, black @ 0.2 | offset(0, -10) blur 40, black @ 0.3 |
| Bottom corners | Square (extend to bottom of screen) | |

Note: In dark mode, sheets use an **elevated** background (`#1C1C1E`) rather than the base `#000000` to create visual separation from the underlying content.

## Grabber Handle

| Property | Value |
|----------|-------|
| Size | 36 x 5pt |
| Corner radius | 2.5pt (fully rounded) |
| Color | systemGray3 (`#C7C7CC` / `#48484A`) |
| Position | Centered horizontally, 5pt from top |
| Visibility | Optional (shown by default when multiple detents) |
| Hit area | 44 x 44pt (for accessibility) |

## Detents

Predefined stop points for sheet height:

| Detent | Height | Notes |
|--------|--------|-------|
| Medium | ~50% of screen height | Approximately half |
| Large | Full screen (minus status bar) | Default |
| Custom | Arbitrary value | Fraction of container, fixed pt, or content-based |

### Detent Behavior

| Property | Value |
|----------|-------|
| Snap threshold | ~20% of distance between detents |
| Velocity threshold | High velocity overrides position threshold |
| Overdrag (past largest) | Rubber-band effect, springs back |
| Underdrag (past smallest) | Dismiss if `dismissible`, else rubber-band |

## Background Dimming

| Property | Value |
|----------|-------|
| Dimming at large detent | black @ 0.4 (default) |
| Dimming at medium detent | None (by default) |
| `largestUndimmedDetentIdentifier` | Controls which detent stops dimming |
| Interaction behind sheet | Allowed when undimmed |
| Dimming animation | Tracks sheet position (not separate animation) |

## Background Content Scaling

When presenting a sheet on top of another sheet or navigation:

| Property | Value |
|----------|-------|
| Background scale | Shrinks to ~0.92 of original size |
| Background corner radius | Matches device screen corners |
| Background offset | Moves up ~10pt |
| Transition | Synchronized with sheet presentation |
| `prefersEdgeAttachedInCompactHeight` | Sheet attaches to edge on compact |

## Animation

### Present

| Property | Value |
|----------|-------|
| Duration | 0.35s |
| Curve | Spring (damping ~0.85, response 0.35) |
| Direction | Slides up from bottom of screen |
| Backdrop dimming | Fades in during slide |
| Background scale | Animates to 0.92 simultaneously |
| Initial velocity | 0 (unless gesture-driven) |

### Dismiss

| Property | Value |
|----------|-------|
| Duration | 0.3s |
| Curve | ease-in (or spring if gesture-driven) |
| Direction | Slides down to bottom |
| Backdrop dimming | Fades out |
| Background scale | Animates back to 1.0 |

### Detent Transition

| Property | Value |
|----------|-------|
| Duration | 0.3s |
| Curve | Spring (damping ~0.8) |
| Snap | Springs to nearest detent |
| Velocity-based | Inherits gesture velocity |

## Interactive Dismissal

| Property | Value |
|----------|-------|
| Gesture | Pan down on sheet |
| Gesture area | Grabber or navigation bar (preferably) |
| Content scrolling | Sheet dismissal deferred until scroll reaches top |
| Dismiss threshold | ~50% of current detent height or high velocity |
| Cancel threshold | Released above 50% → springs back to detent |
| Rubber-band | Present when dragging past top detent |
| Haptic | None during drag |

## Scroll Integration

| Property | Value |
|----------|-------|
| `prefersScrollingExpandsWhenScrolledToEdge` | Scroll to top → expand sheet before bouncing |
| Scroll lock at medium | Content scrolls only when at large detent |
| Scroll-to-dismiss | Scroll to top at large detent → drag dismisses |

## Navigation Bar in Sheet

| Property | Value |
|----------|-------|
| Title | SF Pro Semibold, 17pt, centered |
| Close button position | Top-right (SF Symbol: `xmark.circle.fill`) |
| Close button color | systemGray3 |
| Close button size | 30pt |
| Bar background | Transparent (no material) until scrolled |

## Popover (iPad)

On iPad, `.sheet` can present as a popover or form sheet:

| Property | Value |
|----------|-------|
| Form sheet width | 540pt |
| Form sheet height | Content-dependent (max ~620pt) |
| Corner radius | 14pt (all four corners) |
| Shadow | offset(0, 10) blur 40, black @ 0.25 |
| Dimming | black @ 0.4 |
| Position | Centered on screen |

## Accessibility

| Property | Value |
|----------|-------|
| Grabber | "Sheet grabber, adjustable" |
| Dismiss | Escape gesture or swipe down |
| VoiceOver | Announces sheet content on presentation |
| Focus | Moves to sheet content on present |
