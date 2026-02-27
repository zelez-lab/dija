# Badge

A small visual indicator -- typically a colored dot or count label -- displayed on icons, tabs, or list items to signal new content, unread counts, or status.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UITabBarItem.badgeValue / SwiftUI .badge() | Documented |
| macOS | NSDockTile / NSToolbarItem | Documented |
| Android | Badge (Material Design 3) | Documented |
| Windows | InfoBadge | Documented |
| Linux | Custom styling (no dedicated widget) | Documented |

## iOS

Source: UITabBarItem.badgeValue, UIBarButtonItem, SwiftUI `.badge()`

iOS badges are red notification indicators displayed on tab bar items, app icons, and list rows. There is no standalone UIBadge class; badges are built into specific components.

### Tab Bar Badge

The most common badge in iOS -- a red circle with a count on a tab bar item.

#### Appearance

| Property | Value |
|----------|-------|
| Background | systemRed (`#FF3B30` / `#FF453A`) |
| Text color | white |
| Font | SF Pro Regular, 13pt |
| Font weight | Regular (some sources show Medium) |
| Corner radius | Fully rounded (pill/capsule) |
| Border | 1pt white border (separates from icon) |

#### Sizing

| Content | Width | Height |
|---------|-------|--------|
| Empty (dot) | 6pt | 6pt |
| Single digit (1-9) | 18pt | 18pt |
| Double digit (10-99) | Dynamic (~24pt) | 18pt |
| Triple digit+ (100+) | Dynamic (~30pt) | 18pt |
| Text ("New") | Dynamic | 18pt |

| Property | Value |
|----------|-------|
| Minimum width | 18pt (for single character) |
| Horizontal padding | 5pt each side (when content wider than circle) |
| Maximum characters | No hard limit, but typically 1-4 (e.g., "999+") |

#### Position

| Property | Value |
|----------|-------|
| Anchor | Top-right of the tab bar icon |
| Offset | ~(-8, -4)pt from top-right corner of icon bounds |
| Z-order | Above icon, above tab bar content |
| Clipping | Badge extends beyond tab bar item bounds (not clipped) |

### App Icon Badge (Home Screen)

| Property | Value |
|----------|-------|
| Background | systemRed |
| Text color | white |
| Font | SF Pro Bold, ~14pt |
| Size | 24pt diameter (single digit), pill for multi-digit |
| Horizontal padding | 6pt (multi-digit) |
| Position | Top-right corner of app icon |
| Border | 2pt white border |
| Max display | "99+" or "999+" (system-managed truncation) |
| Shadow | Subtle, offset(0, 1) blur 2, black @ 0.2 |

### List Row Badge (SwiftUI)

SwiftUI `.badge()` on List rows:

| Property | Value |
|----------|-------|
| Background | systemRed (numeric) or systemGray2 (text) |
| Text color | white (numeric), secondaryLabel (text) |
| Font | SF Pro Regular, 17pt (text badge), 17pt (count) |
| Shape | Pill (numeric), plain text (string) |
| Position | Trailing edge of row, before accessories |
| Corner radius | Fully rounded (numeric pill) |
| Padding | 5pt horizontal, 2pt vertical |

Note: In List/sidebar context, text badges may appear as plain secondary text rather than colored pills.

### Custom Badge Colors

`UITabBarItem.badgeColor` allows custom background colors:

| Property | Default |
|----------|---------|
| `badgeColor` | systemRed |
| `badgeTextAttributes` | White, SF Pro 13pt (customizable per state) |

### Animation

| Transition | Duration | Effect |
|-----------|----------|--------|
| Badge appear | 0.3s | Scale from 0 to 1 + fade in (spring, bounce 0.3) |
| Badge disappear | 0.2s | Scale from 1 to 0 + fade out |
| Badge update (value change) | 0.2s | Scale bounce (1.0 -> 1.2 -> 1.0) |
| First appearance | 0.3s spring | Slight overshoot |

### Metrics (Summary)

```
Tab bar item with badge:

      +---+
      | 3 |  <- badge (18pt circle, red, white text)
   +--+---+
   |       |  <- icon (25pt SF Symbol)
   | Home  |  <- label (10pt)
   +-------+
```

### Badge Dot (Empty Badge)

When no count is needed, just a notification indicator:

| Property | Value |
|----------|-------|
| Diameter | 6pt |
| Color | systemRed |
| Border | 1pt white |
| Position | Same as numbered badge |
| Total visual size | ~8pt with border |

### Accessibility

| Property | Value |
|----------|-------|
| VoiceOver (tab) | "[Tab label], [badge value] items, tab" |
| VoiceOver (app icon) | "[App name], [badge value] notifications" |
| VoiceOver (list) | "[Row label], badge, [badge value]" |
| Empty badge | "Has unread notifications" or similar |

## macOS

Reference: NSDockTile, NSToolbarItem, Apple HIG (macOS 14+).

### Overview

Badges on macOS appear in several contexts: the Dock icon badge (red circle with count), tab bar badges, toolbar item badges, and sidebar count badges. Each has slightly different styling but shares the same design language -- a small highlighted label indicating count or status.

### Dock Badge

The most recognizable macOS badge: a red circle on the app's Dock icon showing unread count.

#### Metrics

| Property                  | Value              |
|---------------------------|--------------------|
| Minimum diameter           | 22 pt             |
| Height                     | 22 pt             |
| Horizontal padding         | 6 pt (each side)  |
| Corner radius              | 11 pt (capsule)   |
| Position                   | Top-right of Dock icon |
| Offset from icon edge      | Overlaps by ~4 pt  |

For multi-digit numbers, the badge stretches horizontally:

| Content          | Badge Width (pt) |
|------------------|-------------------|
| 1 digit (1-9)    | 22 (circle)       |
| 2 digits (10-99) | ~30               |
| 3 digits (100+)  | ~38               |
| "999+"           | ~44               |

#### Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font                   | SF Pro             |
| Font size              | 13 pt             |
| Font weight            | Bold               |
| Text color             | `#FFFFFF`          |
| Text alignment         | Center             |
| Line height            | 22 pt (single line)|
| Minimum font size      | 10 pt (scales down for overflow) |

#### Colors

| Element              | Value                              |
|---------------------|-------------------------------------|
| Background           | `#FF3B30` (systemRed)              |
| Text                 | `#FFFFFF`                           |
| Border               | None (or `rgba(0,0,0,0.10)` subtle)|

The Dock badge does NOT change between light and dark mode. It is always red with white text.

#### Shadow

```
Color:   rgba(0, 0, 0, 0.20)
Offset:  (0, 1) pt
Blur:    2 pt
```

#### Animation

When the badge count changes:

| Transition              | Duration (ms) | Curve          |
|------------------------|---------------|----------------|
| Badge appear (0 -> N)   | 200           | Spring (bouncy)|
| Count change (N -> M)   | 150           | Ease Out       |
| Badge disappear (N -> 0)| 150           | Ease In        |

The appear animation uses a scale-up spring from 0.5 to 1.0 with slight bounce.

### Tab Badge

Badges in NSTabView or SwiftUI TabView:

#### Metrics

| Property                  | Value              |
|---------------------------|--------------------|
| Minimum diameter           | 16 pt             |
| Height                     | 16 pt             |
| Horizontal padding         | 4 pt              |
| Corner radius              | 8 pt (capsule)    |
| Position                   | Top-right of tab label |
| Offset from tab content    | (-4, -4) pt       |

#### Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font size              | 10 pt             |
| Font weight            | Bold               |
| Text color             | `#FFFFFF`          |

#### Colors

| Element              | Value                              |
|---------------------|-------------------------------------|
| Background           | `#FF3B30` (systemRed)              |
| Text                 | `#FFFFFF`                           |

### Sidebar Badge (Count Badge)

Used in sidebar rows to show item counts (see sidebar.md for context).

#### Metrics

| Property                  | Value              |
|---------------------------|--------------------|
| Height                     | 18 pt             |
| Minimum width              | 18 pt             |
| Horizontal padding         | 6 pt              |
| Corner radius              | 9 pt (capsule)    |
| Position                   | Right side of row  |
| Right margin               | 6 pt from row edge |

#### Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font size              | 10 pt             |
| Font weight            | Medium             |
| Text alignment         | Center             |

#### Colors

| State                  | Background                         | Text                      |
|------------------------|------------------------------------|---------------------------|
| Normal (light)         | `rgba(0,0,0,0.08)`                | secondaryLabelColor       |
| Normal (dark)          | `rgba(255,255,255,0.10)`           | secondaryLabelColor       |
| Selected row (focused) | `rgba(255,255,255,0.25)`           | `#FFFFFF`                 |
| Selected row (unfocused)| `rgba(0,0,0,0.06)` / `rgba(255,255,255,0.08)` | secondaryLabelColor |

### Toolbar Badge

Badges on toolbar items (e.g., notification indicators).

#### Metrics

| Property                  | Value              |
|---------------------------|--------------------|
| Dot diameter (no count)    | 8 pt              |
| Count badge diameter       | 16 pt             |
| Count badge padding        | 3 pt              |
| Corner radius              | Capsule            |
| Position                   | Top-right of toolbar item icon |
| Offset from icon           | (-2, -2) pt       |

#### Colors

| Variant              | Background           | Text         |
|---------------------|----------------------|--------------|
| Dot (status only)    | `#FF3B30`            | N/A          |
| Count                | `#FF3B30`            | `#FFFFFF`    |
| Info / Neutral       | controlAccentColor   | `#FFFFFF`    |

#### Typography (Count Badge)

| Property              | Value              |
|-----------------------|--------------------|
| Font size              | 9 pt              |
| Font weight            | Bold               |
| Text color             | `#FFFFFF`          |

### Menu Bar Badge

The red dot on menu bar icons (e.g., System Settings notifications):

| Property                  | Value              |
|---------------------------|--------------------|
| Dot diameter               | 6 pt              |
| Position                   | Top-right of menu bar icon |
| Color                      | `#FF3B30`         |
| No text                    | Dot only           |

### Status Dot (Inline)

A small colored dot indicating status (online, away, etc.):

| Property                  | Value              |
|---------------------------|--------------------|
| Diameter                   | 8 pt              |
| Border                     | 1.5 pt white ring  |

| Status               | Color              |
|----------------------|--------------------|
| Online / Active       | `#34C759` (systemGreen) |
| Away / Idle           | `#FFCC00` (systemYellow) |
| Busy / Do Not Disturb | `#FF3B30` (systemRed)   |
| Offline               | `#8E8E93` (gray)        |

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.incrementor` or `.staticText`           |
| Description  | "N new items" or "Badge: N"               |
| Announced    | VoiceOver reads badge value with context   |

### Dija Skin Mapping

```
comp! Badge {
    attr count, u32, default: 0
    attr color, Color, default: Color::system_red()
    attr size, Size, default: Size::SM
    attr variant, BadgeVariant, default: BadgeVariant::Count

    // macOS skin maps:
    // BadgeVariant::Count -> capsule with number text
    // BadgeVariant::Dot   -> solid circle, no text
    // BadgeVariant::Status -> colored dot with white border
    //
    // Size::XS  -> 14 pt height, 9 pt font (menu bar dot: 6 pt)
    // Size::SM  -> 16 pt height, 10 pt font (tab badge)
    // Size::MD  -> 18 pt height, 10 pt font (sidebar badge)
    // Size::LG  -> 22 pt height, 13 pt font (dock badge)
    //
    // Colors:
    //   Default: systemRed bg, white text
    //   Sidebar: gray bg, secondary text (normal)
    //   Status: varies by status enum
    //
    // Animation: spring scale on appear, ease-out on count change
}
```

## Android

Source: m3.material.io/components/badges/specs

### Variants

| Variant | Size | Content |
|---------|------|---------|
| Small (dot) | 6dp x 6dp | No content, presence indicator |
| Large (number) | 16dp height, variable width | 1-3 digit count |

### Small Badge (Dot)

| Property | Value |
|----------|-------|
| Width | 6dp |
| Height | 6dp |
| Corner radius | 3dp (full circle) |
| Color | error (`#B3261E` light / `#F2B8B5` dark) |

### Large Badge (Number)

| Property | Value |
|----------|-------|
| Min width | 16dp |
| Height | 16dp |
| Corner radius | 8dp (full pill) |
| Horizontal padding | 4dp |
| Label font | Label Small (Roboto Medium 500, 11sp) |
| Max digits | 3 (displays "999+" for larger values) |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#B3261E` (error) | `#F2B8B5` |
| Label | `#FFFFFF` (onError) | `#601410` |

### Positioning

Badges are positioned relative to their anchor element (typically an icon):

| Anchor | Small badge offset | Large badge offset |
|--------|-------------------|-------------------|
| Icon (24dp) | top: -2dp, right: -4dp | top: -4dp, right: -6dp |
| Navigation icon | top: 2dp, right: 4dp (from icon center) | top: 0dp, right: 0dp |

Badge should not clip outside the component container bounds. If it would,
adjust position inward.

### States

Badges themselves have no interactive states (not tappable). They reflect
the state of their parent component:

| Parent state | Badge effect |
|-------------|-------------|
| Enabled | Visible |
| Disabled | Hidden or reduced opacity |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Enter (scale up) | Short 3 (150ms) | Emphasized decelerate |
| Exit (scale down) | Short 2 (100ms) | Standard accelerate |
| Count change | Short 2 (100ms) | Cross-fade |

Enter animation scales from 0 to 1.0 at the badge center point.

### Layout

#### On Icon Button

```
+---[Badge 6dp]---+
|  +-----------+  |
|  | Icon 24dp |  |
|  +-----------+  |
+------------------+
```

#### On Navigation Bar Icon

```
    [16dp Badge: 3]
  +-----------+
  | Icon 24dp |
  +-----------+
     Label
```

## Windows

Source: WinUI 3 InfoBadge control

### Variants

| Style | Shape | Size |
|-------|-------|------|
| Dot | Circle | 4px diameter |
| Icon | Circle | 16px diameter |
| Numeric | Rounded pill | 16px height, variable width |

### Dot Badge

Minimal indicator showing presence of new content or attention needed.

| Property | Value |
|----------|-------|
| Diameter | 4px |
| Corner radius | 2px (circle) |
| Background | SystemFillColorCritical (default), or SystemFillColorCaution, SystemFillColorSuccess, SystemFillColorAttention |
| Border | None |

### Icon Badge

Circle containing a small icon glyph.

| Property | Value |
|----------|-------|
| Diameter | 16px |
| Corner radius | 8px (circle) |
| Background | SystemFillColorCritical (default) |
| Icon size | 10x10px |
| Icon color | White (`#FFFFFF`) |
| Border | None |

#### Built-in Icon Types

| Type | Icon |
|------|------|
| Attention | Asterisk (`*`) |
| Informational | `i` glyph |
| Success | Checkmark |
| Critical | `!` exclamation |

### Numeric Badge

Rounded pill showing a count.

| Property | Value |
|----------|-------|
| Height | 16px |
| Min width | 16px (single digit) |
| Padding | 4px horizontal |
| Corner radius | 8px (pill shape) |
| Background | SystemFillColorCritical (default) |
| Font | 11px, SemiBold (600) |
| Text color | White (`#FFFFFF`) |
| Border | None |

#### Overflow

When the number exceeds display width, the pill stretches horizontally. No built-in max-count truncation (app must handle "99+" logic).

### Color Presets

| Preset | Background color (Light) | Background color (Dark) |
|--------|-------------------------|------------------------|
| Critical (default) | `#C42B1C` | `#FF99A4` |
| Attention | SystemAccentColor | SystemAccentColor |
| Informational | SystemFillColorNeutral | SystemFillColorNeutral |
| Success | `#0F7B0F` | `#6CCB5F` |
| Caution | `#9D5D00` | `#FCE100` |

### Position

InfoBadge is designed to be placed on:

| Host | Position | Offset |
|------|----------|--------|
| NavigationViewItem | Top-right of icon area | Overlaps slightly |
| IconButton | Top-right corner | Inset by 2px |
| Tab | Top-right of tab label | Inset by 2px |
| Custom placement | Absolute position via layout |

### States

InfoBadge does not have interactive states (no hover, press, or focus). It is a pure visual indicator.

| State | Behavior |
|-------|----------|
| Value = -1 or unset | Hides the badge |
| Value = 0 | Shows dot or hides (configurable) |
| Value > 0 | Shows numeric or icon badge |

### Dija Mapping

The dija-ui Badge component maps directly:

| Dija Badge | WinUI InfoBadge |
|-----------|----------------|
| `Size::XXS` (dot) | Dot variant (4px) |
| `Size::XS` | Icon variant (16px) |
| `Size::SM` | Numeric variant (16px height) |
| Color attribute | Maps to Fluent preset colors |

## Linux

### Overview

GNOME does not have a dedicated badge widget in GTK4 or libadwaita. Notification
badges are implemented through custom styling -- typically a small colored dot or
count label overlaid on an icon or sidebar row.

### Dot Badge (Unread Indicator)

Used in sidebars, tab bars, and app indicators to signal new/unread content.

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Border | none | 2px (parent bg color, for contrast) |
| Shape | Circle | Circle |

#### Metrics

| Property | Value |
|----------|-------|
| Diameter | 8px |
| Border (when overlaid) | 2px, matches parent background |
| Total visual size | 12px (8px + 2px border each side) |
| Position | Top-right of parent icon/element |
| Offset from parent | -2px right, -2px top |

### Count Badge

Displays a numeric count (unread messages, notifications).

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Text color | `--accent-fg-color` (`#FFFFFF`) | `#FFFFFF` |
| Border | none | 2px parent-bg-colored ring |
| Shape | Pill (capsule) | Pill |

#### Metrics

| Property | Value |
|----------|-------|
| Min-width | 18px |
| Height | 18px |
| Corner radius | 9px (fully rounded) |
| Horizontal padding | 4px |
| Font | Adwaita Sans Bold, 11px |
| Text alignment | Center |
| Max digits shown | 2 ("99+") |

#### Count Formatting

| Count | Display |
|-------|---------|
| 0 | Hidden (no badge) |
| 1-99 | Numeric ("1", "42") |
| 100+ | "99+" |

### Sidebar Badge (Inline Count)

Used in navigation sidebars to show item counts (e.g., mailbox unread count).

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `rgba(0,0,0, 0.08)` | `rgba(255,255,255, 0.08)` |
| Text color | dim-label color | dim-label color |
| Corner radius | 9px (pill) | 9px |

#### Metrics

| Property | Value |
|----------|-------|
| Height | 18px |
| Min-width | 18px |
| Padding | 2px 6px |
| Font | Adwaita Sans Regular, 13px (.caption) |
| Position | Right-aligned in sidebar row (suffix) |
| Margin from row edge | 8px |

This variant uses muted colors to avoid competing with the sidebar selection highlight.

### Badge Position (Overlay)

When used as an overlay on icons:

```
+--------+
| Icon  *|  (* = badge, top-right corner)
|        |
+--------+
```

| Property | Value |
|----------|-------|
| Anchor | Top-right corner of parent |
| Offset X | -25% of badge width (overlaps parent) |
| Offset Y | -25% of badge height (overlaps parent) |
| Z-index | Above parent element |

### States

| State | Dot Badge | Count Badge |
|-------|-----------|-------------|
| Visible | accent circle | accent pill with number |
| Empty (count = 0) | Hidden | Hidden |
| Disabled parent | opacity 0.5 | opacity 0.5 |
| Selected parent row | May change to white/inverse | Stays accent |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Appear (scale) | 200ms | ease-out-cubic |
| Disappear (scale) | 150ms | ease-in-cubic |
| Count change | none (immediate update) | -- |

#### Appear Animation

```
Start:  scale(0.0), opacity(0)
End:    scale(1.0), opacity(1.0)
```

### Dija Skin Mapping

```
skin! {
    BadgeSkin {
        field main
        field label

        platform linux {
            light {
                main: {
                    min_width: 18, height: 18,
                    padding: 2 4,
                    border_radius: 9,
                    background: #3584E4,
                }
                label: {
                    font_size: 11,
                    font_weight: bold,
                    color: #FFFFFF,
                }
            }
        }
    }
}
```
