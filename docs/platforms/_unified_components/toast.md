# Toast

A brief, non-modal notification that appears temporarily to provide feedback about an operation.

| Platform | Native Component | Status |
|---|---|---|
| iOS | --- | No native equivalent |
| macOS | --- | No native equivalent |
| Android | Snackbar (M3) | Documented |
| Windows | InfoBar | Documented |
| Linux | AdwToast | Documented |

## iOS

No native equivalent. Dija renders as a small floating notification following iOS styling conventions.

## macOS

No native equivalent. Dija renders as a small floating notification following macOS styling conventions.

## Android

Source: m3.material.io/components/snackbar/specs

### Variants

| Variant | Layout | Duration |
|---------|--------|----------|
| Single-line | Text only | 4-10 seconds |
| Single-line with action | Text + action button | 4-10 seconds |
| Two-line | Longer text | 4-10 seconds |
| Two-line with action | Longer text + action below | 4-10 seconds |

### Metrics

| Property | Value |
|----------|-------|
| Min height (single-line) | 48dp |
| Min height (two-line) | 68dp |
| Corner radius | 4dp (extra-small) |
| Elevation | Level 3 (6dp) |
| Surface | inverseSurface |
| Horizontal padding | 16dp |
| Vertical padding | 14dp (single-line) |
| Vertical padding (two-line) | 12dp top, 12dp bottom |
| Action button padding | 8dp from right edge |
| Close icon padding | 12dp from right edge |
| Message font | Body Medium (Roboto Regular, 14sp) |
| Action font | Label Large (Roboto Medium, 14sp) + inversePrimary |
| Max width | 600dp |
| Min width | (fills available width on mobile minus margins) |
| Margin from screen edges | 8dp (bottom), 8dp (left/right) on mobile |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#322F35` (inverseSurface) | `#E6E0E9` |
| Message | `#F5EFF7` (inverseOnSurface) | `#322F35` |
| Action button | `#D0BCFF` (inversePrimary) | `#6750A4` |
| Close icon | `#F5EFF7` (inverseOnSurface) | `#322F35` |

The snackbar uses **inverse** color roles to contrast with the surface behind it.

### Action Button

- Text button style (no container)
- Right-aligned, vertically centered (single-line)
- Below message (two-line with longer action text)
- Color: inversePrimary

### Close Icon (Optional)

- 24dp icon (X)
- Shown when the snackbar action is important and shouldn't auto-dismiss
- Right-most element

### Positioning

| Context | Position |
|---------|----------|
| Default | Bottom of screen, centered horizontally |
| With FAB | Slides up above FAB |
| With bottom nav | Above navigation bar |
| Tablet/desktop | Bottom-left corner, 8dp margin |

### States

Snackbars are not interactive except for:
- Action button: standard text button states (hover/focus/pressed)
- Close icon: standard icon button states

### Duration

| Type | Duration |
|------|----------|
| Short | 4000ms |
| Default | 6000ms |
| Long | 10000ms |
| Indefinite | Until dismissed (requires close icon) |

Snackbars auto-dismiss after duration. Only one snackbar visible at a time.
New snackbar replaces current one.

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Enter (slide up + fade) | Medium 2 (300ms) | Emphasized decelerate |
| Exit (fade out) | Short 4 (200ms) | Standard accelerate |
| Queue replace | Exit current, then enter next |

### Layout

#### Single-line

```
+---------------------------------------------+
|  16dp  Message text          [Action]  16dp  |
+---------------------------------------------+
                    48dp height
```

#### Single-line with close icon

```
+------------------------------------------------------+
|  16dp  Message text       [Action]  [X]  12dp  16dp  |
+------------------------------------------------------+
```

#### Two-line with action

```
+---------------------------------------------+
|  12dp                                        |
|  16dp  Message text line 1                   |
|        Message text line 2      [Action]     |
|  12dp                             8dp        |
+---------------------------------------------+
                    68dp min height
```

### Comparison with iOS

M3 snackbar has no direct iOS equivalent. Closest:
- iOS toast (third-party)
- iOS notification banner (system-level)

| Property | M3 Snackbar | iOS (no native equiv) |
|----------|------------|----------------------|
| Position | Bottom | Top (banners) |
| Background | inverseSurface (opaque) | Material blur |
| Corner radius | 4dp | 14dp (squircle) |
| Action button | Text, inversePrimary | Tinted text |

## Windows

Source: WinUI 3 InfoBar control

### Appearance

An inline notification bar that appears within the app content area to inform users of status changes, errors, warnings, or informational messages. Does NOT block interaction.

#### Container Metrics

| Property | Value |
|----------|-------|
| Min height | 40px |
| Padding | 12px horizontal, 8px vertical |
| Corner radius | 8px (layerCornerRadius) |
| Border | 1px (varies by severity) |
| Background | Varies by severity (see below) |
| Icon size | 20x20px |
| Icon-to-content gap | 12px |
| Close button size | 32x32px hit area, 16x16px icon |

### Structure

```
+--------------------------------------------------+
| [i] Title  Message text              [Action] [X] |
+--------------------------------------------------+
```

Multi-line variant:
```
+--------------------------------------------------+
| [i] Title                                    [X]  |
|      Message text that wraps to multiple lines     |
|                                        [Action]    |
+--------------------------------------------------+
```

### Severity Colors

| Severity | Icon | Background (Light) | Background (Dark) | Border (Light) | Border (Dark) |
|----------|------|-------------------|-------------------|----------------|---------------|
| Informational | `i` circle | `#F6F6F6` | `#08FFFFFF` | `#0F000000` | `#15FFFFFF` |
| Success | Checkmark circle | `#DFF6DD` | `#393D1B` | `#0F000000` | `#15FFFFFF` |
| Warning | Exclamation triangle | `#FFF4CE` | `#433519` | `#0F000000` | `#15FFFFFF` |
| Error | X circle | `#FDE7E9` | `#442726` | `#0F000000` | `#15FFFFFF` |

#### Severity Icon Colors

| Severity | Icon color (Light) | Icon color (Dark) |
|----------|-------------------|-------------------|
| Informational | TextFillColorSecondary | TextFillColorSecondary |
| Success | `#0F7B0F` | `#6CCB5F` |
| Warning | `#9D5D00` | `#FCE100` |
| Error | `#C42B1C` | `#FF99A4` |

### Typography

| Element | Font | Color |
|---------|------|-------|
| Title | 14px Body Strong, SemiBold (600) | TextFillColorPrimary |
| Message | 14px Body, Regular (400) | TextFillColorPrimary |
| Hyperlink (in message) | 14px, Regular | AccentTextFillColorPrimary |

### Close Button

| Property | Value |
|----------|-------|
| Icon | `&#xE711;` (X glyph) |
| Size | 32x32px hit area |
| Position | Top-right corner |
| Style | Subtle (transparent -> hover fill) |
| Corner radius | 4px |

Close button uses subtle style states:

| State | Background |
|-------|-----------|
| Rest | Transparent |
| Hover | SubtleFillColorSecondary |
| Pressed | SubtleFillColorTertiary |

### Action Button

| Property | Value |
|----------|-------|
| Style | HyperlinkButton or DefaultButtonStyle |
| Height | 32px |
| Position | Right side (single-line) or bottom-right (multi-line) |
| Font | 14px, SemiBold |

### Custom Content

InfoBar supports custom content below the message text:

| Property | Value |
|----------|-------|
| Content area | Below message, full width minus icon/close areas |
| Padding | 0px additional (inherits container padding) |

### Layout Behavior

| Condition | Layout |
|-----------|--------|
| Short content (fits single line) | Horizontal: icon, title, message, action, close |
| Long content | Wraps: title on first line, message below, action below message |
| Very long message | Message text wraps freely |
| Width < 500px | Stacks to multi-line layout |

### Position

InfoBar is placed inline in the content area. Common placements:

| Position | Description |
|----------|------------|
| Top of page | Directly below header/navigation |
| Above content area | Pushes content down |
| Bottom of page | Above status bar or footer |

InfoBar takes up space in the layout and pushes sibling elements. It is NOT a floating overlay.

### IsClosable

When `IsClosable = false`:
- Close button is hidden
- InfoBar remains visible until programmatically removed
- Used for persistent status messages

### IsIconVisible

When `IsIconVisible = false`:
- Severity icon is hidden
- Content shifts left to fill the space
- Background and border still reflect severity

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| InfoBar appear (expand height + fade) | 300ms | Decelerate |
| InfoBar close (collapse height + fade) | 200ms | Accelerate |
| Content reflow (after close) | 200ms | Decelerate |

The appear animation: starts at 0 height and 0 opacity, expands to full height while fading in. The close animation reverses this: collapses height while fading out, and surrounding content smoothly fills the space.

## Linux

`AdwToast` is a brief, non-modal notification that appears at the bottom of the window.
It is managed by `AdwToastOverlay`, which stacks and animates toasts.

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#303030` (dark, always) | `#303030` |
| Text color | `#FFFFFF` (always light text) | `#FFFFFF` |
| Corner radius | 12px | 12px |
| Shadow | (0, 2) blur 8, black @ 0.20 | (0, 2) blur 8, black @ 0.20 |
| Border | none | none |

The toast intentionally uses a dark background in both light and dark themes,
creating a high-contrast floating element that draws attention.

### Layout

```
+----------------------------------------------+
|  Title text message        [Action] [X]      |
+----------------------------------------------+
```

| Element | Description |
|---------|-------------|
| Title | Required, primary message text |
| Action button | Optional, text button for undo/action |
| Dismiss button | Optional X button (shown if dismissible) |

### Metrics

| Property | Value |
|----------|-------|
| Max width | 450px |
| Min width | (auto, fits content) |
| Height | ~42px (single line) |
| Horizontal padding | 12px |
| Vertical padding | 8px |
| Corner radius | 12px |
| Bottom margin | 12px (from window bottom) |
| Horizontal alignment | Centered |
| Title-action gap | 8px |

### Typography

| Element | Font | Size | Weight | Color |
|---------|------|------|--------|-------|
| Title | Adwaita Sans | 15px | Regular | `#FFFFFF` |
| Action button | Adwaita Sans | 15px | Bold | `--accent-color` (light variant, e.g., `#78AEED`) |

### Action Button

| Property | Value |
|----------|-------|
| Style | Flat, text-only |
| Text color | Accent color (lighter shade for dark bg) |
| Hover bg | `rgba(255,255,255, 0.10)` |
| Active bg | `rgba(255,255,255, 0.15)` |
| Corner radius | 6px |
| Padding | 4px 8px |

### Dismiss Button

| Property | Value |
|----------|-------|
| Icon | X (close), 16px |
| Style | Flat, circular |
| Size | 24x24px |
| Hover bg | `rgba(255,255,255, 0.10)` |
| Visibility | Shown only if `.dismissible` is set |

### Behavior

| Property | Value |
|----------|-------|
| Default timeout | 5 seconds |
| Custom timeout | 0 (indefinite), or any duration in seconds |
| Priority | `ADW_TOAST_PRIORITY_NORMAL` or `ADW_TOAST_PRIORITY_HIGH` |
| Stacking | New toasts replace current (with animation) |
| Queue | Toasts queue up, shown one at a time |
| Markup | Supported by default (use-markup property) |

#### Priority Behavior

| Priority | Behavior |
|----------|----------|
| Normal | Queued, shown after current toast expires |
| High | Immediately replaces current toast |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Slide in (from bottom) | 350ms | ease-out-cubic |
| Slide out (to bottom) | 300ms | ease-in-cubic |
| Replace (current out, new in) | 300ms total | ease-in-out |
| Fade in (opacity) | 350ms | ease-out |
| Fade out (opacity) | 300ms | ease-in |

#### Appear Animation

```
Start:  translateY(+50px), opacity(0)
End:    translateY(0),      opacity(1.0)
```

#### Dismiss Animation

```
Start:  translateY(0),      opacity(1.0)
End:    translateY(+50px),  opacity(0)
```

### Toast Overlay

`AdwToastOverlay` is a container widget that manages toast positioning:

| Property | Value |
|----------|-------|
| Toast position | Bottom center of overlay |
| Z-order | Above all overlay children |
| Multiple toasts | Queued, one visible at a time |
| Passthrough | Clicks pass through to content (except on toast) |

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Escape | Dismiss current toast |
| Enter / Space | Activate action button (if focused) |

Toasts are not focusable by default -- they are informational. The action button
can receive focus through accessibility tools.

### Comparison to iOS

| Property | GNOME AdwToast | iOS (no direct equivalent) |
|----------|---------------|---------------------------|
| Position | Bottom center | Top or custom |
| Background | Dark opaque | System material |
| Duration | 5s default | 2-3s typical |
| Stacking | Queue (1 visible) | Multiple visible |
| Action | Optional text button | Tap to act |
| Dismiss | Auto or manual | Auto or swipe |
