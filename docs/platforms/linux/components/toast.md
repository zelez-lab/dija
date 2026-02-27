# Linux (GNOME/Adwaita) — Toast (AdwToast / AdwToastOverlay)

## Overview

`AdwToast` is a brief, non-modal notification that appears at the bottom of the window.
It is managed by `AdwToastOverlay`, which stacks and animates toasts.

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#303030` (dark, always) | `#303030` |
| Text color | `#FFFFFF` (always light text) | `#FFFFFF` |
| Corner radius | 12px | 12px |
| Shadow | (0, 2) blur 8, black @ 0.20 | (0, 2) blur 8, black @ 0.20 |
| Border | none | none |

The toast intentionally uses a dark background in both light and dark themes,
creating a high-contrast floating element that draws attention.

## Layout

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

## Metrics

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

## Typography

| Element | Font | Size | Weight | Color |
|---------|------|------|--------|-------|
| Title | Adwaita Sans | 15px | Regular | `#FFFFFF` |
| Action button | Adwaita Sans | 15px | Bold | `--accent-color` (light variant, e.g., `#78AEED`) |

## Action Button

| Property | Value |
|----------|-------|
| Style | Flat, text-only |
| Text color | Accent color (lighter shade for dark bg) |
| Hover bg | `rgba(255,255,255, 0.10)` |
| Active bg | `rgba(255,255,255, 0.15)` |
| Corner radius | 6px |
| Padding | 4px 8px |

## Dismiss Button

| Property | Value |
|----------|-------|
| Icon | X (close), 16px |
| Style | Flat, circular |
| Size | 24x24px |
| Hover bg | `rgba(255,255,255, 0.10)` |
| Visibility | Shown only if `.dismissible` is set |

## Behavior

| Property | Value |
|----------|-------|
| Default timeout | 5 seconds |
| Custom timeout | 0 (indefinite), or any duration in seconds |
| Priority | `ADW_TOAST_PRIORITY_NORMAL` or `ADW_TOAST_PRIORITY_HIGH` |
| Stacking | New toasts replace current (with animation) |
| Queue | Toasts queue up, shown one at a time |
| Markup | Supported by default (use-markup property) |

### Priority Behavior

| Priority | Behavior |
|----------|----------|
| Normal | Queued, shown after current toast expires |
| High | Immediately replaces current toast |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Slide in (from bottom) | 350ms | ease-out-cubic |
| Slide out (to bottom) | 300ms | ease-in-cubic |
| Replace (current out, new in) | 300ms total | ease-in-out |
| Fade in (opacity) | 350ms | ease-out |
| Fade out (opacity) | 300ms | ease-in |

### Appear Animation

```
Start:  translateY(+50px), opacity(0)
End:    translateY(0),      opacity(1.0)
```

### Dismiss Animation

```
Start:  translateY(0),      opacity(1.0)
End:    translateY(+50px),  opacity(0)
```

## Toast Overlay

`AdwToastOverlay` is a container widget that manages toast positioning:

| Property | Value |
|----------|-------|
| Toast position | Bottom center of overlay |
| Z-order | Above all overlay children |
| Multiple toasts | Queued, one visible at a time |
| Passthrough | Clicks pass through to content (except on toast) |

## Keyboard Interaction

| Key | Action |
|-----|--------|
| Escape | Dismiss current toast |
| Enter / Space | Activate action button (if focused) |

Toasts are not focusable by default — they are informational. The action button
can receive focus through accessibility tools.

## Comparison to iOS

| Property | GNOME AdwToast | iOS (no direct equivalent) |
|----------|---------------|---------------------------|
| Position | Bottom center | Top or custom |
| Background | Dark opaque | System material |
| Duration | 5s default | 2-3s typical |
| Stacking | Queue (1 visible) | Multiple visible |
| Action | Optional text button | Tap to act |
| Dismiss | Auto or manual | Auto or swipe |
