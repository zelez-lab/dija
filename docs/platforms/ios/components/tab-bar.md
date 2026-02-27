# iOS — Tab Bar (UITabBar)

Source: UITabBar, UITabBarItem, SwiftUI TabView

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | Material Thin/Regular (translucent) | Material Thin/Regular |
| Background (scrolled) | Solid systemBackground | Solid `#000000` (elevated: `#1C1C1E`) |
| Top separator | 0.33pt separator color | 0.33pt separator color |
| Separator (at rest, no content scrolled under) | Hidden | Hidden |

Like the navigation bar, the tab bar transitions from translucent material to solid opaque when content scrolls underneath.

## Dimensions

| Property | Value |
|----------|-------|
| Height (without safe area) | 49pt |
| Height (with bottom safe area) | 83pt (49pt + 34pt home indicator) |
| Maximum items | 5 (6th item triggers "More" tab) |
| Item width | Equally distributed across bar width |

## Tab Items

| Property | Unselected | Selected |
|----------|-----------|----------|
| Icon size | 25pt (SF Symbol, medium weight) | 25pt (SF Symbol, medium weight) |
| Icon color | systemGray (`#8E8E93`) | tintColor (systemBlue default) |
| Label font | SF Pro Medium, 10pt | SF Pro Medium, 10pt |
| Label color | systemGray (`#8E8E93`) | tintColor |
| Icon-to-label spacing | 2pt | 2pt |
| Label baseline | 2pt above bottom edge | |

### Icon Rendering

| Property | Value |
|----------|-------|
| Symbol configuration | `.unspecified` (25pt default for tab bars) |
| Symbol weight | Medium |
| Rendering mode | Template (single color, tinted) |
| Selected animation (iOS 18+) | Bounce effect on symbol |
| Fill variant | Selected icons use `.fill` variant (e.g., `house` -> `house.fill`) |

## Badge

| Property | Value |
|----------|-------|
| Background | systemRed (`#FF3B30` / `#FF453A`) |
| Text color | white |
| Font | SF Pro, 13pt |
| Corner radius | Fully rounded (pill) |
| Minimum size | 18pt diameter (for single digit) |
| Padding | 5pt horizontal (for multi-digit) |
| Position | Top-right of icon, offset by ~(-8, -4)pt |
| Border | 1pt white border (to separate from icon) |
| Max characters | Typically 1-4 (e.g., "9", "99", "99+") |
| Empty badge | Red dot, 6pt diameter |

## States

| State | Effect |
|-------|--------|
| Normal (unselected) | Gray icon + label |
| Selected | tintColor icon + label |
| Pressed | Brief opacity reduction on icon |
| Disabled | Alpha 0.3, non-interactive |

## Animation

| Property | Value |
|----------|-------|
| Tab selection | Instant (no crossfade) |
| View transition | No animation by default (abrupt swap) |
| Icon bounce (iOS 18+) | Spring, ~0.5s, bounce 0.3 |
| Badge appear | Scale from 0 + fade, ~0.3s spring |
| Badge update | Scale bounce, ~0.2s |

## Landscape Layout (iPhone)

On iPhone in landscape orientation:

| Property | Value |
|----------|-------|
| Height | 32pt (+ safe area) |
| Layout | Icon left, label right (side-by-side) |
| Icon size | 19pt |
| Label font | SF Pro Medium, 10pt |
| Spacing (icon to label) | 5pt |

## iPad Tab Bar (iOS 18+)

On iPad, iOS 18 moved the tab bar to a sidebar/top-bar hybrid:

| Property | Value |
|----------|-------|
| Position | Top of screen (compact) or leading sidebar |
| Appearance | Floating pill, material background |
| Behavior | Expandable to sidebar on tap |

## More Tab

When there are more than 5 items:

| Property | Value |
|----------|-------|
| Icon | Ellipsis (three dots) |
| Label | "More" |
| Screen | Table view listing remaining tabs |
| Reordering | Users can drag tabs from More list to tab bar |

## Accessibility

| Property | Value |
|----------|-------|
| Role | Tab bar |
| Each item | Tab (button with "selected" trait) |
| VoiceOver | "[Label], tab, [N] of [total]" |
| Badge announcement | "[Label], [badge value], tab" |
