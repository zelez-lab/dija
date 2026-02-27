# Linux (GNOME/Adwaita) — Alert (AdwAlertDialog)

## Overview

`AdwAlertDialog` is a modal dialog for warnings, confirmations, and user decisions.
It replaces the deprecated `GtkMessageDialog` in modern GNOME apps.

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FAFAFA` (dialog_bg_color) | `#383838` |
| Text color | `#2E3436` | `#FFFFFF` |
| Corner radius | 12px | 12px |
| Shadow | (0, 12) blur 36, black @ 0.25 | (0, 12) blur 36, black @ 0.25 |
| Scrim (backdrop) | black @ 0.32 | black @ 0.32 |

## Layout

```
+----------------------------------+
|          [optional icon]         |
|                                  |
|        Title (centered)          |
|                                  |
|     Body text (centered,         |
|     multi-line wrapping)         |
|                                  |
|   [Extra child widget area]      |
|                                  |
+----------------------------------+
|  [Cancel]   |   [Destructive]    |
+----------------------------------+
```

## Metrics

| Property | Value |
|----------|-------|
| Max width | 480px |
| Min width | 300px |
| Content padding | 24px |
| Title-to-body gap | 8px |
| Body-to-buttons gap | 24px |
| Button area padding | 0px (buttons fill width) |
| Button separator | 1px `rgba(0,0,0, 0.15)` |
| Button height | 42px |

## Typography

| Element | Font | Weight | Size | Alignment |
|---------|------|--------|------|-----------|
| Title | Adwaita Sans | Bold | 18px (.title-3) | Center |
| Body | Adwaita Sans | Regular | 15px (.body) | Center |
| Button label | Adwaita Sans | Regular | 15px | Center |
| Suggested button label | Adwaita Sans | Bold | 15px | Center |

## Button Layout

Buttons are placed in a horizontal row at the bottom, separated by 1px borders.
For 2 buttons, they split 50/50 width. For 3+, they stack vertically.

### Horizontal Layout (2 buttons)

```
+------------------+---+------------------+
|     Cancel       | | | Suggested/Action |
+------------------+---+------------------+
```

### Vertical Layout (3+ buttons)

```
+------------------------------------+
|          Primary Action            |
+------------------------------------+
|          Secondary Action          |
+------------------------------------+
|            Cancel                  |
+------------------------------------+
```

## Button Styles

| Style | Background | Text Color | Usage |
|-------|-----------|------------|-------|
| Default | transparent | `--window-fg-color` | Cancel, dismiss |
| Suggested | transparent | `--accent-color` | Confirm, save |
| Destructive | transparent | `--destructive-color` | Delete, discard |

Note: Unlike standalone buttons, dialog buttons are **flat** (no background fill).
The accent/destructive color is applied to the text only.

### Button States (within dialog)

| State | Effect |
|-------|--------|
| Rest | Flat, text color only |
| Hover | `rgba(0,0,0, 0.04)` background |
| Active | `rgba(0,0,0, 0.08)` background |
| Focused | 2px accent outline (inset) |

## Response Types

| Response | Appearance | Keyboard |
|----------|-----------|----------|
| Default | Regular text | — |
| Suggested | Accent-colored text, bold | Enter activates |
| Destructive | Red text | — |
| Close | Hidden (dialog close) | Escape activates |

## Focus Behavior

| Property | Value |
|----------|-------|
| Initial focus | Suggested action button (if set) |
| Tab order | Buttons left-to-right, then content |
| Escape | Closes dialog (fires close response) |
| Enter | Activates default/suggested response |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Appear (scale + fade) | 250ms | ease-out-cubic |
| Dismiss (fade) | 200ms | ease-in-cubic |
| Scrim fade in | 250ms | ease-out |
| Scrim fade out | 200ms | ease-in |

### Appear Animation

```
Start:  scale(0.95), opacity(0)
End:    scale(1.0),  opacity(1.0)
```

### Dismiss Animation

```
Start:  scale(1.0),  opacity(1.0)
End:    scale(0.95), opacity(0)
```

## Comparison to iOS Alert

| Property | GNOME AdwAlertDialog | iOS UIAlertController |
|----------|---------------------|----------------------|
| Background | Opaque, flat | Translucent material |
| Corner radius | 12px (CSS arc) | 14pt (superellipse) |
| Max width | 480px | 270pt |
| Button style | Flat text in row | Flat text in row |
| Button separator | 1px | 0.33pt |
| Animation | Scale + fade | Spring + fade |
| Scrim | black @ 0.32 | black @ 0.40 |
