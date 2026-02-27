# Tooltip

A small, transient popup that provides brief descriptive or contextual information about a UI element, typically triggered by hovering or focusing the element. On touch-first platforms like iOS, the pattern is expressed through context menus and tip views instead.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIContextMenuInteraction / TipKit (iOS 17+) | Documented |
| macOS | NSToolTipManager / NSView.toolTip | Documented |
| Android | Material Design 3 Tooltip (Plain / Rich) | Documented |
| Windows | WinUI 3 ToolTip / TeachingTip | Documented |
| Linux | GtkTooltip (GNOME/Adwaita) | Documented |

## iOS

Source: UIContextMenuInteraction, UIMenu, SwiftUI `.contextMenu`

iOS does not have a traditional tooltip component. Instead, it uses **context menus** (long-press menus with optional preview) and **menu buttons** (tap-triggered menus). This document covers both.

### Context Menu (Long-Press)

#### Trigger

| Property | Value |
|----------|-------|
| Gesture | Long press (~0.5s) or 3D Touch |
| Haptic | Medium impact on menu appear |
| Preview | Optional -- shows a scaled-up preview of the element |

#### Backdrop

| Property | Value |
|----------|-------|
| Dimming | Gaussian blur on entire screen + black @ 0.25 overlay |
| Background content | Scales down to ~0.85 |
| Background corner radius | Matches screen corners |
| Transition | 0.3s spring |

#### Preview

| Property | Value |
|----------|-------|
| Corner radius | 16pt (continuous/squircle) |
| Shadow | offset(0, 10) blur 30, black @ 0.2 |
| Max size | ~90% of screen width, proportional height |
| Clip | Content clips to rounded rect |
| Appear animation | Scale from element position, spring ~0.4s |
| Dismiss animation | Scale back to element position or fade |

#### Menu

| Property | Value |
|----------|-------|
| Background | Ultra-thick material (vibrancy) |
| Corner radius | 14pt (continuous/squircle) |
| Shadow | offset(0, 10) blur 30, black @ 0.2 |
| Width | ~250pt (content-dependent, max ~320pt) |
| Position | Adjacent to preview (above/below depending on space) |

#### Menu Items

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

#### Destructive Items

| Property | Value |
|----------|-------|
| Text color | systemRed |
| Icon color | systemRed |
| Icon | Typically `trash` or similar |

#### Disabled Items

| Property | Value |
|----------|-------|
| Text color | tertiaryLabel |
| Icon color | tertiaryLabel |
| Interaction | Non-tappable |

#### Submenus

| Property | Value |
|----------|-------|
| Indicator | Chevron right (>) on trailing edge |
| Expand animation | 0.2s slide/fade |
| Nesting | Up to 3 levels deep recommended |
| Back | System-managed (swipe or tap header) |

### Menu Sections

Menus can be grouped into sections:

| Property | Value |
|----------|-------|
| Section separator | 7pt gap with separator line |
| Section title | SF Pro Regular, 13pt, secondaryLabel (optional) |
| Inline section | No gap, just separator line |

### Menu Item Variants

| Variant | Appearance |
|---------|-----------|
| Standard | Label + optional icon |
| Destructive | Red label + red icon |
| Disabled | Grayed out, non-interactive |
| On/Off (checkmark) | Checkmark on leading edge when selected |
| Selected (palette) | Tinted background |

### Pull-Down Menu (UIButton.menu)

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

### Popover Tip (TipKit, iOS 17+)

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

### Animation

#### Context Menu Appear

| Phase | Duration | Effect |
|-------|----------|--------|
| 1. Haptic | Instant | Medium impact feedback |
| 2. Element lifts | 0.2s | Scale to ~1.05, shadow appears |
| 3. Backdrop dims | 0.3s | Blur + dim background |
| 4. Preview expands | 0.3s spring | Scale to preview size |
| 5. Menu slides in | 0.2s | Fade + slide from preview edge |

#### Context Menu Dismiss

| Trigger | Animation |
|---------|-----------|
| Tap action | Menu fades, preview snaps back to element (spring 0.3s) |
| Tap backdrop | Menu fades, preview shrinks back (0.25s) |
| Preview tap (custom) | Preview can navigate to full content |

### Accessibility

| Property | Value |
|----------|-------|
| VoiceOver | "Actions available" trait on element |
| Menu items | Each announced as button |
| Destructive | "Destructive" trait added |
| Submenu | "Has submenu" announced |

## macOS

Reference: NSView tooltip support, NSToolTipManager (private), Apple HIG (macOS 14+).

### Overview

Tooltips in macOS are small, transient text labels that appear when the user hovers over a UI element. They are managed by the system through `NSView.toolTip` and the internal `NSToolTipManager`. Tooltips have a distinct yellow-ish appearance in light mode and a gray appearance in dark mode.

### Timing

| Property                  | Value              |
|---------------------------|--------------------|
| Hover delay before show    | ~1000 ms          |
| Display duration           | ~10000 ms (10 sec)|
| Fade-in duration           | ~200 ms           |
| Fade-out duration          | ~200 ms           |
| Re-hover delay (same)      | ~100 ms           |
| Re-hover delay (different) | ~500 ms           |

The hover delay is measured from when the cursor enters the tooltip rect. If the user moves the mouse away and back quickly, the tooltip reappears faster (re-hover delay).

### Metrics

#### Sizing

| Property                  | Value              |
|---------------------------|--------------------|
| Maximum width              | 300 pt            |
| Padding (horizontal)       | 8 pt              |
| Padding (vertical)         | 4 pt              |
| Corner radius              | 4 pt              |
| Offset from cursor         | (0, 18) pt approx |

The tooltip is positioned below and slightly to the right of the cursor. If the tooltip would extend beyond the screen edge, it flips to appear above or to the left.

#### Position Rules

| Screen Edge          | Tooltip Position                          |
|---------------------|-------------------------------------------|
| Bottom too close     | Appears above cursor                      |
| Right too close      | Shifts left to fit on screen              |
| Top too close        | Appears below cursor (default behavior)   |
| Left too close       | Shifts right                              |

### Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font                   | SF Pro (system)    |
| Font size              | 11 pt             |
| Font weight            | Regular            |
| Line height            | 14 pt             |
| Max lines              | ~10 (wraps at max width) |
| Text alignment         | Left               |

### Colors

#### Background

| Mode      | Value                                  |
|-----------|----------------------------------------|
| Light     | `#FFFFCC` (pale yellow, tooltip classic) |
| Dark      | `#3C3C3C` (dark gray)                  |

With vibrancy enabled (macOS 10.14+), tooltips use the `.toolTip` material:

| Mode      | Vibrancy Material                      |
|-----------|----------------------------------------|
| Light     | `.toolTip` material (slightly warm tint)|
| Dark      | `.toolTip` material (neutral gray)      |

Fallback when vibrancy is disabled:

| Mode      | Fallback                               |
|-----------|----------------------------------------|
| Light     | `#FFFFCC`                              |
| Dark      | `#3C3C3C`                              |

#### Text

| Mode      | Color                                  |
|-----------|----------------------------------------|
| Light     | `#000000`                              |
| Dark      | `#FFFFFF`                              |

#### Border

| Mode      | Color                                  |
|-----------|----------------------------------------|
| Light     | `rgba(0,0,0,0.15)`                    |
| Dark      | `rgba(255,255,255,0.10)`              |

Border width: 0.5 pt.

#### Shadow

```
Color:   rgba(0, 0, 0, 0.12)
Offset:  (0, 2) pt
Blur:    8 pt
```

### Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Appear (fade in)     | 200           | Ease Out      |
| Disappear (fade out) | 200           | Ease In       |
| Reposition           | 0             | Immediate     |

### Interaction

| Event                    | Behavior                                |
|--------------------------|------------------------------------------|
| Mouse enters tooltip rect | Start hover delay timer                 |
| Mouse exits tooltip rect  | Dismiss tooltip (with fade)             |
| Mouse button click        | Dismiss tooltip immediately              |
| Mouse moves within rect   | Tooltip stays visible                    |
| Keyboard event            | Dismiss tooltip immediately              |
| Scroll event              | Dismiss tooltip immediately              |
| Window becomes inactive   | Dismiss tooltip immediately              |

### Rich Tooltips

macOS 14+ introduced richer tooltip content through accessibility descriptions, but the visual tooltip itself remains text-only. For rich content, apps typically use custom popover views, not the tooltip system.

### Custom Tooltip Rects

`NSView.addToolTipRect(_:owner:userData:)` allows defining rectangular regions with distinct tooltips:

| Property              | Description                            |
|-----------------------|----------------------------------------|
| Tracking rect          | NSRect defining the hover area        |
| Owner                  | Object providing tooltip string        |
| User data              | Optional context pointer               |

Multiple tooltip rects can exist on a single view.

### System Tooltips in Standard Controls

Standard AppKit controls provide built-in tooltips:

| Control              | Default Tooltip Content                |
|---------------------|----------------------------------------|
| NSToolbarItem        | Item label (when icon-only display)   |
| NSButton (toolbar)   | Button title or accessibility label    |
| NSSegmentedControl   | Per-segment via `setToolTip(_:forSegment:)` |
| Truncated text       | Full text (automatic for NSTextField)  |
| Menu bar item        | Help tag text                          |

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.helpTag` (system tooltip)               |
| Announced    | Tooltip text read by VoiceOver             |
| Timing       | VoiceOver reads immediately (no delay)     |

### Dija Skin Mapping

```
comp! Tooltip {
    attr text, &str, default: ""
    attr delay_ms, u32, default: 1000
    attr max_width, f32, default: 300.0

    // macOS skin maps:
    // Background: #FFFFCC (light) / #3C3C3C (dark)
    // Or: .toolTip vibrancy material
    // Text: 11 pt system font, regular weight
    // Padding: 8 pt horizontal, 4 pt vertical
    // Corner radius: 4 pt
    // Border: 0.5 pt at rgba(0,0,0,0.15) / rgba(255,255,255,0.10)
    // Shadow: rgba(0,0,0,0.12) offset (0,2) blur 8
    // Show delay: 1000 ms
    // Fade: 200 ms
}
```

## Android

Source: m3.material.io/components/tooltips/specs

### Variants

| Variant | Content | Duration | Interaction |
|---------|---------|----------|------------|
| Plain | Short text label | Short (1500ms) | Long-press or hover |
| Rich | Title, text, actions, link | Persistent until dismissed | Long-press or hover |

### Plain Tooltip

#### Metrics

| Property | Value |
|----------|-------|
| Height | 24dp (single line, auto-height for wrap) |
| Max width | 200dp |
| Corner radius | 4dp (extra-small) |
| Horizontal padding | 8dp |
| Vertical padding | 4dp |
| Label font | Body Small (Roboto Regular, 12sp) |
| Caret (arrow) height | 5dp |
| Caret width | 8dp |
| Offset from anchor | 8dp |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#322F35` (inverseSurface) | `#E6E0E9` |
| Label | `#F5EFF7` (inverseOnSurface) | `#322F35` |

### Rich Tooltip

#### Metrics

| Property | Value |
|----------|-------|
| Max width | 320dp |
| Min width | 180dp |
| Corner radius | 12dp (medium) |
| Padding | 16dp (all sides) |
| Subhead font | Title Small (Roboto Medium, 14sp) |
| Supporting text font | Body Medium (Roboto Regular, 14sp) |
| Action font | Label Large (Roboto Medium, 14sp) |
| Subhead-to-text gap | 4dp |
| Text-to-action gap | 16dp |
| Caret height | 5dp |
| Caret width | 8dp |
| Offset from anchor | 8dp |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainer) | `#2B2930` |
| Subhead | `#1D1B20` (onSurfaceVariant) | `#E6E0E9` |
| Supporting text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Action button | `#6750A4` (primary) | `#D0BCFF` |

### Caret (Arrow)

Optional triangular pointer connecting the tooltip to its anchor:

| Property | Value |
|----------|-------|
| Width | 8dp |
| Height | 5dp |
| Shape | Triangle / rounded triangle |
| Position | Centered on anchor, auto-adjusted to stay on screen |
| Color | Same as container |

Caret can point up, down, left, or right depending on tooltip position relative to its anchor.

### Positioning

Tooltips auto-position relative to their anchor in 8dp increments:

| Preference | Description |
|-----------|------------|
| Below | Default placement |
| Above | When below would clip screen |
| Start/End | When vertical space is limited |

Margin from screen edges: 8dp minimum.

### Behavior

#### Plain Tooltip

| Trigger | Duration |
|---------|----------|
| Long-press | Show after 500ms hold, auto-hide after 1500ms |
| Hover (desktop) | Show after 500ms hover, auto-hide after 1500ms |
| Focus (keyboard) | Show immediately, hide on blur |

#### Rich Tooltip

| Trigger | Duration |
|---------|----------|
| Long-press | Persistent until tap elsewhere |
| Hover (desktop) | Persistent while hovering tooltip or anchor |
| Focus (keyboard) | Persistent until Escape or blur |

Rich tooltips can include:
- Subhead (optional)
- Supporting text (required)
- Action button (optional, max 1)
- Close icon (optional for persistent tooltips)

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Enter (fade in + scale) | Short 4 (200ms) | Emphasized decelerate |
| Exit (fade out) | Short 3 (150ms) | Standard accelerate |

Enter scales from 0.85 to 1.0 with simultaneous fade from 0 to 1.

### Layout

#### Plain Tooltip

```
         +-------------------+
         | 8dp  Label  8dp  |  24dp height
         +-------------------+
               \/  caret 5dp
         +-----------+
         |  Anchor   |
         +-----------+
```

#### Rich Tooltip

```
+-------------------------------+
|  16dp                         |
|  Subhead (Title Small)        |
|  4dp                          |
|  Supporting text (Body Med)   |
|  Supporting text line 2       |
|  16dp                         |
|            [Action]     16dp  |
+-------------------------------+
        180-320dp width
        12dp corner radius
```

### Comparison with iOS

iOS does not have a native tooltip component. Closest alternatives:
- `UIPopoverPresentationController` (iPad only)
- `UIMenuController` (deprecated)
- Custom popover views

| Property | M3 Plain Tooltip | M3 Rich Tooltip |
|----------|-----------------|-----------------|
| Corner radius | 4dp | 12dp |
| Background | inverseSurface | surfaceContainer |
| Max width | 200dp | 320dp |
| Caret | Optional | Optional |
| Actions | None | Up to 1 button |

## Windows

Source: WinUI 3 ToolTip, TeachingTip controls

### ToolTip

A lightweight popup that shows explanatory text when the user hovers over or focuses a control.

#### Metrics

| Property | Value |
|----------|-------|
| Max width | 320px |
| Padding | 8px horizontal, 6px vertical |
| Corner radius | 4px (controlCornerRadius) |
| Background | SolidBackgroundFillColorSecondary (`#EEEEEE` / `#1C1C1C`) |
| Border | 1px ControlStrokeColorDefault |
| Shadow | Shadow 2 |
| Font | 12px Caption, Regular (400) |
| Text color | TextFillColorPrimary |
| Max lines | Unlimited (wraps at max width) |

#### Timing

| Event | Delay |
|-------|-------|
| Show delay (initial hover) | 400ms |
| Show delay (subsequent, BetweenShowDelay) | 100ms |
| Auto-dismiss | 5000ms (configurable) |

#### Placement

| Mode | Description |
|------|------------|
| Top | Above the target (default) |
| Bottom | Below the target |
| Left | Left of target |
| Right | Right of target |
| Mouse | Near mouse cursor |
| Auto | System chooses based on space |

Offset from target: 4px gap.

#### States

ToolTip is non-interactive. It disappears when:
- Mouse leaves the target control
- Auto-dismiss timer expires
- Target control loses focus
- User scrolls the page

### TeachingTip

A rich, contextual popup for user education, first-run tips, and feature discovery. Can include title, message, action buttons, an image/illustration, and a close button.

#### Container Metrics

| Property | Value |
|----------|-------|
| Max width | 336px |
| Min width | 320px |
| Padding | 16px |
| Corner radius | 8px (layerCornerRadius) |
| Background | SolidBackgroundFillColorSecondary |
| Border | 1px SurfaceStrokeColorDefault |
| Shadow | Shadow 16 |

#### Structure

```
+----------------------------------+
| [Hero image (optional)]         |  <- Full width, above content
+----------------------------------+
| [Icon]  Title               [X] |  <- 14px SemiBold + close button
|                                  |
| Message body text                |  <- 14px Regular, TextFillColorSecondary
|                                  |
|                   [Action] [X]   |  <- Optional action button + close
+------------^---------------------+
             | Tail (triangle pointer)
```

#### Title

| Property | Value |
|----------|-------|
| Font | 14px Body Strong, SemiBold (600) |
| Color | TextFillColorPrimary |
| Icon size | 16x16px (optional, left of title) |

#### Subtitle / Message

| Property | Value |
|----------|-------|
| Font | 14px Body, Regular (400) |
| Color | TextFillColorSecondary |
| Top margin | 4px (below title) |

#### Close Button

| Property | Value |
|----------|-------|
| Icon | `&#xE711;` (X glyph), 8x8px visible, 32x32px hit area |
| Position | Top-right corner |
| Style | Subtle (transparent rest, hover fill) |

#### Action Button

| Property | Value |
|----------|-------|
| Style | AccentButtonStyle or DefaultButtonStyle |
| Height | 32px |
| Position | Bottom-right of content area |
| Max: 2 buttons | Action + Close (text variant) |

#### Tail (Pointer Arrow)

| Property | Value |
|----------|-------|
| Width | 16px |
| Height | 8px |
| Shape | Isoceles triangle |
| Fill | Same as TeachingTip background |
| Border | 1px, same as container border |
| Shadow | None (cannot shadow non-rectangular surfaces) |
| Margin from edges | 12px minimum from container corners |
| Position | Centers on target element when possible |

#### Placement Modes (Targeted)

| Mode | Description |
|------|------------|
| Top | Above target, tail points down |
| Bottom | Below target, tail points up |
| Left | Left of target, tail points right |
| Right | Right of target, tail points left |
| Center | Overlapping target center |
| TopRight, TopLeft | Offset variants |
| BottomRight, BottomLeft | Offset variants |
| LeftTop, LeftBottom | Offset variants |
| RightTop, RightBottom | Offset variants |
| Auto | System chooses based on space |

#### Non-Targeted (Global) TeachingTip

When no target is specified, the TeachingTip appears at the bottom of the window without a tail.

| Property | Value |
|----------|-------|
| Position | Bottom-center of window |
| Margin from bottom | 16px |
| Tail | Hidden |
| Width | Up to 336px, centered |

#### Hero Image

| Property | Value |
|----------|-------|
| Position | Top of TeachingTip (above title) |
| Width | Full width (minus border) |
| Max height | 200px |
| Corner radius | Inherits top corners from container (8px top-left, 8px top-right, 0 bottom) |

### Behavior

| Behavior | ToolTip | TeachingTip |
|----------|---------|-------------|
| Trigger | Hover / focus | Programmatic (IsOpen) |
| Light dismiss | N/A (auto-dismiss) | Yes (click outside closes) |
| Escape key | N/A | Closes |
| Interactive content | No | Yes (buttons, links) |
| Persist on hover | No | Yes (stays while interacting) |
| Preferred placement | Top | Auto |
| Multiple visible | No (one at a time) | No (one at a time) |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| ToolTip fade in | 100ms | Decelerate |
| ToolTip fade out | 50ms | Accelerate |
| TeachingTip open (scale + fade) | 300ms | Decelerate |
| TeachingTip close (fade) | 200ms | Accelerate |
| TeachingTip tail appear | Matches container | -- |

## Linux

### Overview

GtkTooltip displays a small popup with descriptive text when the user hovers over a widget or focuses it via keyboard.

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#2E3436` (dark, always) | `#2E3436` |
| Text color | `#FFFFFF` (always) | `#FFFFFF` |
| Border | 1px `rgba(255,255,255, 0.10)` | 1px `rgba(255,255,255, 0.10)` |
| Corner radius | 6px | 6px |
| Shadow | (0, 2) blur 6, black @ 0.20 | (0, 2) blur 6, black @ 0.20 |

Like toasts, tooltips use a **dark background regardless of theme mode** to ensure high visibility against any content.

### Metrics

| Property | Value |
|----------|-------|
| Horizontal padding | 8px |
| Vertical padding | 4px |
| Max width | 300px (text wraps beyond this) |
| Corner radius | 6px |
| Arrow/pointer | None (no arrow in GTK4/Adwaita) |
| Offset from element | 4px gap |

### Typography

| Element | Font | Size | Weight | Color |
|---------|------|------|--------|-------|
| Text (simple) | Adwaita Sans | 13px (.caption) | Regular | `#FFFFFF` |
| Text (with markup) | Adwaita Sans | 13px | Regular | `#FFFFFF` |

### Positioning

| Property | Value |
|----------|-------|
| Preferred position | Below the target element |
| Fallback | Above, then left/right if no space below |
| Alignment | Horizontally centered on target |
| Screen edge behavior | Shifts to stay within window bounds |
| Offset (from target) | 4px |

#### Position Priority

```
1. Below center
2. Above center
3. Right center
4. Left center
```

### Trigger Behavior

#### Mouse Hover

| Property | Value |
|----------|-------|
| Show delay | 500ms (after hover starts) |
| Hide delay | immediate (on mouse leave) |
| Re-show delay | 200ms (when moving between tooltip targets) |
| Sticky | Tooltip follows cursor within element |

#### Keyboard Focus

| Property | Value |
|----------|-------|
| Show trigger | Focus arrives on element |
| Show delay | 500ms |
| Hide trigger | Focus leaves element |
| Hide delay | immediate |

#### Touch

| Property | Value |
|----------|-------|
| Show trigger | Long press (~800ms) |
| Hide trigger | Release or tap elsewhere |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Appear (fade in) | 150ms | ease-out |
| Disappear (fade out) | 100ms | ease-in |
| Reposition | immediate | -- |

#### Appear

```
Start:  opacity(0)
End:    opacity(1.0)
```

No scale or slide animation -- tooltips fade in place.

### Content Types

#### Simple Text Tooltip

Set via `widget.set_tooltip_text("Description")`:

```
+---------------------------+
|  Descriptive text here    |
+---------------------------+
```

#### Markup Tooltip

Set via `widget.set_tooltip_markup("<b>Bold</b> text")`:

Supports a subset of Pango markup (bold, italic, links).

#### Custom Tooltip

Set via `widget.set_has_tooltip(true)` + `query-tooltip` signal:

Can contain any widget tree (icons, multi-line layout, images).

| Property | Value |
|----------|-------|
| Custom content padding | 8px |
| Max width | 300px |
| Custom widget | Any GtkWidget |

### Keyboard Shortcut Tooltip

For buttons with keyboard shortcuts, GNOME convention is to include the shortcut in the tooltip:

```
+----------------------------------+
|  Copy  (Ctrl+C)                  |
+----------------------------------+
```

| Element | Formatting |
|---------|-----------|
| Label | Regular text |
| Shortcut | Parenthesized, same font |
| Separator | Space before parenthesis |

With `AdwButtonContent` + `GtkShortcutController`, the tooltip can be auto-generated.

### Accessibility

| Property | Value |
|----------|-------|
| Role | tooltip |
| Announced | Yes, by screen readers when element is focused |
| aria-describedby | Auto-set when tooltip-text is set |

### States

| State | Behavior |
|-------|----------|
| Target disabled | Tooltip still shows (describes why disabled) |
| Target insensitive | Tooltip does not show |
| Window unfocused | Tooltips disabled |
| Another tooltip visible | Previous hides, new shows after re-show delay |

### CSS Node Structure

```
tooltip
 +-- box (content container)
      +-- label (or custom widget)
```

### Comparison to iOS

| Property | GNOME Tooltip | iOS (no equivalent) |
|----------|--------------|-------------------|
| Trigger | Hover / focus | N/A (touch-first) |
| Background | Dark opaque | N/A |
| Arrow | None | N/A |
| Delay | 500ms | N/A |
| Max width | 300px | N/A |

iOS has no tooltip equivalent -- contextual information is conveyed through accessibility labels and long-press previews instead.
