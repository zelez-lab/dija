# Tab Bar

A bar typically at the bottom of the screen for switching between top-level views in an app.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UITabBar | Documented |
| macOS | — | No native equivalent |
| Android | NavigationBar (bottom) | Documented |
| Windows | NavigationView (top) | Documented |
| Linux | — | No native equivalent |

## iOS

Source: UITabBar, UITabBarItem, SwiftUI TabView

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | Material Thin/Regular (translucent) | Material Thin/Regular |
| Background (scrolled) | Solid systemBackground | Solid `#000000` (elevated: `#1C1C1E`) |
| Top separator | 0.33pt separator color | 0.33pt separator color |
| Separator (at rest, no content scrolled under) | Hidden | Hidden |

Like the navigation bar, the tab bar transitions from translucent material to solid opaque when content scrolls underneath.

### Dimensions

| Property | Value |
|----------|-------|
| Height (without safe area) | 49pt |
| Height (with bottom safe area) | 83pt (49pt + 34pt home indicator) |
| Maximum items | 5 (6th item triggers "More" tab) |
| Item width | Equally distributed across bar width |

### Tab Items

| Property | Unselected | Selected |
|----------|-----------|----------|
| Icon size | 25pt (SF Symbol, medium weight) | 25pt (SF Symbol, medium weight) |
| Icon color | systemGray (`#8E8E93`) | tintColor (systemBlue default) |
| Label font | SF Pro Medium, 10pt | SF Pro Medium, 10pt |
| Label color | systemGray (`#8E8E93`) | tintColor |
| Icon-to-label spacing | 2pt | 2pt |
| Label baseline | 2pt above bottom edge | |

#### Icon Rendering

| Property | Value |
|----------|-------|
| Symbol configuration | `.unspecified` (25pt default for tab bars) |
| Symbol weight | Medium |
| Rendering mode | Template (single color, tinted) |
| Selected animation (iOS 18+) | Bounce effect on symbol |
| Fill variant | Selected icons use `.fill` variant (e.g., `house` -> `house.fill`) |

### Badge

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

### States

| State | Effect |
|-------|--------|
| Normal (unselected) | Gray icon + label |
| Selected | tintColor icon + label |
| Pressed | Brief opacity reduction on icon |
| Disabled | Alpha 0.3, non-interactive |

### Animation

| Property | Value |
|----------|-------|
| Tab selection | Instant (no crossfade) |
| View transition | No animation by default (abrupt swap) |
| Icon bounce (iOS 18+) | Spring, ~0.5s, bounce 0.3 |
| Badge appear | Scale from 0 + fade, ~0.3s spring |
| Badge update | Scale bounce, ~0.2s |

### Landscape Layout (iPhone)

On iPhone in landscape orientation:

| Property | Value |
|----------|-------|
| Height | 32pt (+ safe area) |
| Layout | Icon left, label right (side-by-side) |
| Icon size | 19pt |
| Label font | SF Pro Medium, 10pt |
| Spacing (icon to label) | 5pt |

### iPad Tab Bar (iOS 18+)

On iPad, iOS 18 moved the tab bar to a sidebar/top-bar hybrid:

| Property | Value |
|----------|-------|
| Position | Top of screen (compact) or leading sidebar |
| Appearance | Floating pill, material background |
| Behavior | Expandable to sidebar on tap |

### More Tab

When there are more than 5 items:

| Property | Value |
|----------|-------|
| Icon | Ellipsis (three dots) |
| Label | "More" |
| Screen | Table view listing remaining tabs |
| Reordering | Users can drag tabs from More list to tab bar |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Tab bar |
| Each item | Tab (button with "selected" trait) |
| VoiceOver | "[Label], tab, [N] of [total]" |
| Badge announcement | "[Label], [badge value], tab" |

## macOS

No native equivalent. Dija renders as a bottom bar with icon+label items following macOS styling conventions.

## Android

Source: m3.material.io/components/navigation-bar/specs

Bottom navigation bar for primary destinations (3-5 items).

### Metrics

| Property | Value |
|----------|-------|
| Height | 80dp |
| Elevation | Level 2 (3dp) |
| Surface | surfaceContainer |
| Icon size | 24dp |
| Active indicator width | 64dp |
| Active indicator height | 32dp |
| Active indicator corner radius | 16dp (full pill) |
| Label font (active) | Label Medium (Roboto Medium 500, 12sp) |
| Label font (inactive) | Label Medium (Roboto Medium 500, 12sp) |
| Icon-to-label gap | 4dp |
| Min item width | 48dp |
| Max item width | 80dp |
| Item padding (horizontal) | 0dp (items equally spaced) |
| Top padding (to icon) | 12dp |
| Bottom padding (to label) | 16dp |

### Active Indicator

The active indicator is a pill shape that appears behind the selected icon:

| Property | Value |
|----------|-------|
| Width | 64dp |
| Height | 32dp |
| Corner radius | 16dp |
| Color | secondaryContainer |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#F3EDF7` (surfaceContainer) | `#211F26` |
| Active icon | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |
| Active indicator | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Active label | `#1D1B20` (onSurface) | `#E6E0E9` |
| Inactive icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Inactive label | `#49454F` (onSurfaceVariant) | `#CAC4D0` |

### States

| State | Effect |
|-------|--------|
| Hovered | State layer 8% on indicator area |
| Focused | State layer 10% on indicator area |
| Pressed | State layer 10% + ripple on indicator area |

State layer color: onSurface for inactive items, onSecondaryContainer for active.

### Animation

- Indicator scale: Short 3 (150ms), Emphasized decelerate
- Icon transition (filled/outlined): Short 2 (100ms)
- Label fade: Short 2 (100ms)
- Label Y translation: up 4dp on select, down on deselect

### Badge Position

Badges appear on the top-right of the icon:
- Small dot badge: offset (8dp, -4dp) from icon center-right
- Large number badge: offset (4dp, -4dp)
- Badge must not overlap other items

### Layout

```
+------------------------------------------------------------------+
|  12dp padding top                                                |
|  [Icon]   [==Indicator==]   [Icon]          [Icon]               |
|           [  Active Icon ]                                       |
|  4dp gap                                                         |
|  Label     Label (bold)      Label           Label               |
|  16dp padding bottom                                             |
+------------------------------------------------------------------+
                              80dp
```

3-5 destinations. Below 3, use different navigation. Above 5, use
navigation drawer or navigation rail.

## Windows

Source: WinUI 3 NavigationView control (`PaneDisplayMode="Top"`)

When NavigationView is set to Top display mode, it acts as a horizontal tab bar across the top of the app.

### Top Navigation Mode Metrics

| Property | Value |
|----------|-------|
| Bar height | 48px |
| Item padding | 12px horizontal |
| Selection indicator | 3px wide accent pill at bottom (horizontal, same 16px length) |
| Overflow | Items that don't fit go into a "More" dropdown |
| Background | Transparent (inherits parent background) |

### Navigation Item

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px horizontal |
| Corner radius | 4px |
| Icon size | 16x16px |
| Icon-to-text gap | 12px |
| Font | 14px, Regular |

### Item States

| State | Background | Text | Indicator |
|-------|-----------|------|-----------|
| Rest | Transparent | TextFillColorPrimary | None |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary | None |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary | None |
| Selected | SubtleFillColorSecondary | TextFillColorPrimary | 3px accent pill (bottom) |
| Selected + Hover | SubtleFillColorTertiary | TextFillColorPrimary | 3px accent pill |
| Disabled | Transparent | TextFillColorDisabled | None |

### Selection Indicator (Pill)

| Property | Value |
|----------|-------|
| Width | 3px |
| Height | 16px |
| Corner radius | 1.5px |
| Color | AccentFillColorDefault |
| Animation | Slides horizontally between items (200ms, Decelerate) |

### Content Area

| Property | Value |
|----------|-------|
| Margin (minimal mode) | 12px |
| Margin (expanded mode) | 24px |
| Transition | Slide + fade (300ms, Decelerate) on page navigation |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Selection pill slide (between items) | 200ms | Decelerate |
| Page content enter (slide + fade) | 300ms | Decelerate |
| Page content exit | 150ms | Accelerate |

## Linux

No native equivalent. Dija renders as a bottom bar following GNOME/Adwaita styling conventions.
