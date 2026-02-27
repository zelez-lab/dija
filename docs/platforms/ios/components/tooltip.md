# iOS — Context Menu / Tooltip (UIContextMenuInteraction)

Source: UIContextMenuInteraction, UIMenu, SwiftUI `.contextMenu`

iOS does not have a traditional tooltip component. Instead, it uses **context menus** (long-press menus with optional preview) and **menu buttons** (tap-triggered menus). This document covers both.

## Context Menu (Long-Press)

### Trigger

| Property | Value |
|----------|-------|
| Gesture | Long press (~0.5s) or 3D Touch |
| Haptic | Medium impact on menu appear |
| Preview | Optional — shows a scaled-up preview of the element |

### Backdrop

| Property | Value |
|----------|-------|
| Dimming | Gaussian blur on entire screen + black @ 0.25 overlay |
| Background content | Scales down to ~0.85 |
| Background corner radius | Matches screen corners |
| Transition | 0.3s spring |

### Preview

| Property | Value |
|----------|-------|
| Corner radius | 16pt (continuous/squircle) |
| Shadow | offset(0, 10) blur 30, black @ 0.2 |
| Max size | ~90% of screen width, proportional height |
| Clip | Content clips to rounded rect |
| Appear animation | Scale from element position, spring ~0.4s |
| Dismiss animation | Scale back to element position or fade |

### Menu

| Property | Value |
|----------|-------|
| Background | Ultra-thick material (vibrancy) |
| Corner radius | 14pt (continuous/squircle) |
| Shadow | offset(0, 10) blur 30, black @ 0.2 |
| Width | ~250pt (content-dependent, max ~320pt) |
| Position | Adjacent to preview (above/below depending on space) |

### Menu Items

| Property | Value |
|----------|-------|
| Row height | 44pt |
| Font | SF Pro Regular, 17pt |
| Text color | label |
| Icon size | 20pt (SF Symbol) |
| Icon position | Right side (trailing) |
| Icon color | label (or specific color for destructive) |
| Separator | 0.33pt, separator color |
| Padding (horizontal) | 16pt |
| Padding (vertical) | 12pt (first/last items) |

### Destructive Items

| Property | Value |
|----------|-------|
| Text color | systemRed |
| Icon color | systemRed |
| Icon | Typically `trash` or similar |

### Disabled Items

| Property | Value |
|----------|-------|
| Text color | tertiaryLabel |
| Icon color | tertiaryLabel |
| Interaction | Non-tappable |

### Submenus

| Property | Value |
|----------|-------|
| Indicator | Chevron right (>) on trailing edge |
| Expand animation | 0.2s slide/fade |
| Nesting | Up to 3 levels deep recommended |
| Back | System-managed (swipe or tap header) |

## Menu Sections

Menus can be grouped into sections:

| Property | Value |
|----------|-------|
| Section separator | 7pt gap with separator line |
| Section title | SF Pro Regular, 13pt, secondaryLabel (optional) |
| Inline section | No gap, just separator line |

## Menu Item Variants

| Variant | Appearance |
|---------|-----------|
| Standard | Label + optional icon |
| Destructive | Red label + red icon |
| Disabled | Grayed out, non-interactive |
| On/Off (checkmark) | Checkmark on leading edge when selected |
| Selected (palette) | Tinted background |

## Pull-Down Menu (UIButton.menu)

Tap-triggered menus without preview, attached to a button:

| Property | Value |
|----------|-------|
| Trigger | Tap (when `showsMenuAsPrimaryAction = true`) or long-press |
| Position | Below or above button (system-managed) |
| Arrow | Points toward the button |
| Width | ~250pt |
| Appearance | Same as context menu (material background, 14pt radius) |
| No preview | Only the menu, no preview card |
| No dimming | No backdrop blur |

## Popover Tip (TipKit, iOS 17+)

iOS 17 introduced TipKit for instructional tooltips:

| Property | Value |
|----------|-------|
| Background | systemBackground (opaque) |
| Corner radius | 14pt |
| Arrow | Pointed toward the anchor element |
| Arrow size | ~13pt height |
| Shadow | offset(0, 4) blur 16, black @ 0.15 |
| Title font | SF Pro Semibold, 15pt |
| Message font | SF Pro Regular, 13pt |
| Title color | label |
| Message color | secondaryLabel |
| Action button font | SF Pro Semibold, 15pt |
| Action button color | tintColor |
| Close button | X icon, top-right, systemGray3 |
| Close button size | ~17pt |
| Max width | ~300pt |
| Padding | 12pt |

## Animation

### Context Menu Appear

| Phase | Duration | Effect |
|-------|----------|--------|
| 1. Haptic | Instant | Medium impact feedback |
| 2. Element lifts | 0.2s | Scale to ~1.05, shadow appears |
| 3. Backdrop dims | 0.3s | Blur + dim background |
| 4. Preview expands | 0.3s spring | Scale to preview size |
| 5. Menu slides in | 0.2s | Fade + slide from preview edge |

### Context Menu Dismiss

| Trigger | Animation |
|---------|-----------|
| Tap action | Menu fades, preview snaps back to element (spring 0.3s) |
| Tap backdrop | Menu fades, preview shrinks back (0.25s) |
| Preview tap (custom) | Preview can navigate to full content |

## Accessibility

| Property | Value |
|----------|-------|
| VoiceOver | "Actions available" trait on element |
| Menu items | Each announced as button |
| Destructive | "Destructive" trait added |
| Submenu | "Has submenu" announced |
