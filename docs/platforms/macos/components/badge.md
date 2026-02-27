# macOS Badge

Reference: NSDockTile, NSToolbarItem, Apple HIG (macOS 14+).

## Overview

Badges on macOS appear in several contexts: the Dock icon badge (red circle with count), tab bar badges, toolbar item badges, and sidebar count badges. Each has slightly different styling but shares the same design language -- a small highlighted label indicating count or status.

## Dock Badge

The most recognizable macOS badge: a red circle on the app's Dock icon showing unread count.

### Metrics

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

### Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font                   | SF Pro             |
| Font size              | 13 pt             |
| Font weight            | Bold               |
| Text color             | `#FFFFFF`          |
| Text alignment         | Center             |
| Line height            | 22 pt (single line)|
| Minimum font size      | 10 pt (scales down for overflow) |

### Colors

| Element              | Value                              |
|---------------------|-------------------------------------|
| Background           | `#FF3B30` (systemRed)              |
| Text                 | `#FFFFFF`                           |
| Border               | None (or `rgba(0,0,0,0.10)` subtle)|

The Dock badge does NOT change between light and dark mode. It is always red with white text.

### Shadow

```
Color:   rgba(0, 0, 0, 0.20)
Offset:  (0, 1) pt
Blur:    2 pt
```

### Animation

When the badge count changes:

| Transition              | Duration (ms) | Curve          |
|------------------------|---------------|----------------|
| Badge appear (0 -> N)   | 200           | Spring (bouncy)|
| Count change (N -> M)   | 150           | Ease Out       |
| Badge disappear (N -> 0)| 150           | Ease In        |

The appear animation uses a scale-up spring from 0.5 to 1.0 with slight bounce.

## Tab Badge

Badges in NSTabView or SwiftUI TabView:

### Metrics

| Property                  | Value              |
|---------------------------|--------------------|
| Minimum diameter           | 16 pt             |
| Height                     | 16 pt             |
| Horizontal padding         | 4 pt              |
| Corner radius              | 8 pt (capsule)    |
| Position                   | Top-right of tab label |
| Offset from tab content    | (-4, -4) pt       |

### Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font size              | 10 pt             |
| Font weight            | Bold               |
| Text color             | `#FFFFFF`          |

### Colors

| Element              | Value                              |
|---------------------|-------------------------------------|
| Background           | `#FF3B30` (systemRed)              |
| Text                 | `#FFFFFF`                           |

## Sidebar Badge (Count Badge)

Used in sidebar rows to show item counts (see sidebar.md for context).

### Metrics

| Property                  | Value              |
|---------------------------|--------------------|
| Height                     | 18 pt             |
| Minimum width              | 18 pt             |
| Horizontal padding         | 6 pt              |
| Corner radius              | 9 pt (capsule)    |
| Position                   | Right side of row  |
| Right margin               | 6 pt from row edge |

### Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font size              | 10 pt             |
| Font weight            | Medium             |
| Text alignment         | Center             |

### Colors

| State                  | Background                         | Text                      |
|------------------------|------------------------------------|---------------------------|
| Normal (light)         | `rgba(0,0,0,0.08)`                | secondaryLabelColor       |
| Normal (dark)          | `rgba(255,255,255,0.10)`           | secondaryLabelColor       |
| Selected row (focused) | `rgba(255,255,255,0.25)`           | `#FFFFFF`                 |
| Selected row (unfocused)| `rgba(0,0,0,0.06)` / `rgba(255,255,255,0.08)` | secondaryLabelColor |

## Toolbar Badge

Badges on toolbar items (e.g., notification indicators).

### Metrics

| Property                  | Value              |
|---------------------------|--------------------|
| Dot diameter (no count)    | 8 pt              |
| Count badge diameter       | 16 pt             |
| Count badge padding        | 3 pt              |
| Corner radius              | Capsule            |
| Position                   | Top-right of toolbar item icon |
| Offset from icon           | (-2, -2) pt       |

### Colors

| Variant              | Background           | Text         |
|---------------------|----------------------|--------------|
| Dot (status only)    | `#FF3B30`            | N/A          |
| Count                | `#FF3B30`            | `#FFFFFF`    |
| Info / Neutral       | controlAccentColor   | `#FFFFFF`    |

### Typography (Count Badge)

| Property              | Value              |
|-----------------------|--------------------|
| Font size              | 9 pt              |
| Font weight            | Bold               |
| Text color             | `#FFFFFF`          |

## Menu Bar Badge

The red dot on menu bar icons (e.g., System Settings notifications):

| Property                  | Value              |
|---------------------------|--------------------|
| Dot diameter               | 6 pt              |
| Position                   | Top-right of menu bar icon |
| Color                      | `#FF3B30`         |
| No text                    | Dot only           |

## Status Dot (Inline)

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

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.incrementor` or `.staticText`           |
| Description  | "N new items" or "Badge: N"               |
| Announced    | VoiceOver reads badge value with context   |

## Dija Skin Mapping

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
