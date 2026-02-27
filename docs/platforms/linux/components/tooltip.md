# Linux (GNOME/Adwaita) — Tooltip (GtkTooltip)

## Overview

GtkTooltip displays a small popup with descriptive text when the user hovers over
a widget or focuses it via keyboard.

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#2E3436` (dark, always) | `#2E3436` |
| Text color | `#FFFFFF` (always) | `#FFFFFF` |
| Border | 1px `rgba(255,255,255, 0.10)` | 1px `rgba(255,255,255, 0.10)` |
| Corner radius | 6px | 6px |
| Shadow | (0, 2) blur 6, black @ 0.20 | (0, 2) blur 6, black @ 0.20 |

Like toasts, tooltips use a **dark background regardless of theme mode** to ensure
high visibility against any content.

## Metrics

| Property | Value |
|----------|-------|
| Horizontal padding | 8px |
| Vertical padding | 4px |
| Max width | 300px (text wraps beyond this) |
| Corner radius | 6px |
| Arrow/pointer | None (no arrow in GTK4/Adwaita) |
| Offset from element | 4px gap |

## Typography

| Element | Font | Size | Weight | Color |
|---------|------|------|--------|-------|
| Text (simple) | Adwaita Sans | 13px (.caption) | Regular | `#FFFFFF` |
| Text (with markup) | Adwaita Sans | 13px | Regular | `#FFFFFF` |

## Positioning

| Property | Value |
|----------|-------|
| Preferred position | Below the target element |
| Fallback | Above, then left/right if no space below |
| Alignment | Horizontally centered on target |
| Screen edge behavior | Shifts to stay within window bounds |
| Offset (from target) | 4px |

### Position Priority

```
1. Below center
2. Above center
3. Right center
4. Left center
```

## Trigger Behavior

### Mouse Hover

| Property | Value |
|----------|-------|
| Show delay | 500ms (after hover starts) |
| Hide delay | immediate (on mouse leave) |
| Re-show delay | 200ms (when moving between tooltip targets) |
| Sticky | Tooltip follows cursor within element |

### Keyboard Focus

| Property | Value |
|----------|-------|
| Show trigger | Focus arrives on element |
| Show delay | 500ms |
| Hide trigger | Focus leaves element |
| Hide delay | immediate |

### Touch

| Property | Value |
|----------|-------|
| Show trigger | Long press (~800ms) |
| Hide trigger | Release or tap elsewhere |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Appear (fade in) | 150ms | ease-out |
| Disappear (fade out) | 100ms | ease-in |
| Reposition | immediate | — |

### Appear

```
Start:  opacity(0)
End:    opacity(1.0)
```

No scale or slide animation — tooltips fade in place.

## Content Types

### Simple Text Tooltip

Set via `widget.set_tooltip_text("Description")`:

```
+---------------------------+
|  Descriptive text here    |
+---------------------------+
```

### Markup Tooltip

Set via `widget.set_tooltip_markup("<b>Bold</b> text")`:

Supports a subset of Pango markup (bold, italic, links).

### Custom Tooltip

Set via `widget.set_has_tooltip(true)` + `query-tooltip` signal:

Can contain any widget tree (icons, multi-line layout, images).

| Property | Value |
|----------|-------|
| Custom content padding | 8px |
| Max width | 300px |
| Custom widget | Any GtkWidget |

## Keyboard Shortcut Tooltip

For buttons with keyboard shortcuts, GNOME convention is to include the shortcut
in the tooltip:

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

## Accessibility

| Property | Value |
|----------|-------|
| Role | tooltip |
| Announced | Yes, by screen readers when element is focused |
| aria-describedby | Auto-set when tooltip-text is set |

## States

| State | Behavior |
|-------|----------|
| Target disabled | Tooltip still shows (describes why disabled) |
| Target insensitive | Tooltip does not show |
| Window unfocused | Tooltips disabled |
| Another tooltip visible | Previous hides, new shows after re-show delay |

## CSS Node Structure

```
tooltip
 +-- box (content container)
      +-- label (or custom widget)
```

## Comparison to iOS

| Property | GNOME Tooltip | iOS (no equivalent) |
|----------|--------------|-------------------|
| Trigger | Hover / focus | N/A (touch-first) |
| Background | Dark opaque | N/A |
| Arrow | None | N/A |
| Delay | 500ms | N/A |
| Max width | 300px | N/A |

iOS has no tooltip equivalent — contextual information is conveyed through
accessibility labels and long-press previews instead.
