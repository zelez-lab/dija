# Windows — Button

Source: WinUI 3 Button, ToggleButton, HyperlinkButton

## Variants

| Style | Background (rest) | Foreground | Border |
|-------|-------------------|-----------|--------|
| Standard (Default) | ControlFillColorDefault (`#B3FFFFFF` / `#0FFFFFFF`) | TextFillColorPrimary | ControlStrokeColorDefault (1px) + bottom ControlStrokeColorSecondary |
| Accent | AccentFillColorDefault (SystemAccentColor) | TextOnAccentFillColorPrimary (white/black) | ControlStrokeColorOnAccentDefault (1px) + bottom ControlStrokeColorOnAccentSecondary |
| Subtle | Transparent | TextFillColorPrimary | None |
| Toggle (off) | Same as Standard | TextFillColorPrimary | Same as Standard |
| Toggle (on) | Same as Accent | TextOnAccentFillColorPrimary | Same as Accent |
| Hyperlink | Transparent | AccentTextFillColorPrimary | None, underline on hover |

## Metrics

| Property | Value |
|----------|-------|
| Min height | 32px |
| Min width | 120px (for dialog buttons), no global min |
| Padding | 11px left, 5px top, 11px right, 6px bottom |
| Corner radius | 4px (controlCornerRadius) |
| Font | Segoe UI Variable, 14px, SemiBold (600) |
| Icon size (when present) | 16x16px |
| Icon-to-text gap | 8px |
| Border | 1px top/sides + subtle bottom gradient stroke |

The asymmetric vertical padding (5px top, 6px bottom) accounts for optical centering of text with the bottom border accent.

## States

### Standard Button

| State | Background | Border | Text |
|-------|-----------|--------|------|
| Rest | ControlFillColorDefault | ControlStrokeColorDefault | TextFillColorPrimary |
| Hover | ControlFillColorSecondary | ControlStrokeColorDefault | TextFillColorPrimary |
| Pressed | ControlFillColorTertiary | ControlStrokeColorDefault | TextFillColorSecondary |
| Disabled | ControlFillColorDisabled | ControlStrokeColorDefault (reduced) | TextFillColorDisabled |
| Focused | Rest appearance + dual focus ring | FocusStrokeColorOuter (2px) + FocusStrokeColorInner (1px) | — |

### Accent Button

| State | Background | Border | Text |
|-------|-----------|--------|------|
| Rest | AccentFillColorDefault | ControlStrokeColorOnAccentDefault | TextOnAccentFillColorPrimary |
| Hover | AccentFillColorSecondary | ControlStrokeColorOnAccentDefault | TextOnAccentFillColorPrimary |
| Pressed | AccentFillColorTertiary | ControlStrokeColorOnAccentTertiary | TextOnAccentFillColorSecondary |
| Disabled | AccentFillColorDisabled | transparent | TextOnAccentFillColorDisabled |

### Subtle Button

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |
| Disabled | Transparent | TextFillColorDisabled |

### Hyperlink Button

| State | Text | Decoration |
|-------|------|-----------|
| Rest | AccentTextFillColorPrimary | None |
| Hover | AccentTextFillColorSecondary | Underline |
| Pressed | AccentTextFillColorTertiary | None |
| Disabled | AccentTextFillColorDisabled | None |

## Bottom Border Effect

Standard and Accent buttons have a subtle gradient border effect: the bottom edge of the border is slightly darker than the top/sides. This creates a subtle 3D "shelf" appearance.

- Top/sides border: `ControlStrokeColorDefault` (light: `#0F000000`, dark: `#12FFFFFF`)
- Bottom border: `ControlStrokeColorSecondary` (light: `#29000000`, dark: `#18FFFFFF`)

For Accent buttons, the bottom border uses `ControlStrokeColorOnAccentSecondary`.

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Rest → Hover (fill) | 100ms | Control fast |
| Hover → Pressed (fill) | 50ms | Linear |
| Pressed → Rest (fill) | 200ms | Decelerate |
| Focus ring appear | 100ms | Control fast |

## Compact Mode

When `Compact` density is applied:
- Height: 24px
- Padding: 11px horizontal, 1px vertical
- Font size remains 14px
