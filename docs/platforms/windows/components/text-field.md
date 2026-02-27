# Windows — TextBox

Source: WinUI 3 TextBox control

## Appearance

- Background: ControlFillColorDefault (`#B3FFFFFF` / `#0FFFFFFF`)
- Border: 1px ControlStrokeColorDefault (top/sides) + ControlStrokeColorSecondary (bottom)
- Corner radius: 4px (controlCornerRadius)
- No shadow

## Metrics

| Property | Value |
|----------|-------|
| Min height | 32px |
| Padding | 11px horizontal, 5px top, 6px bottom |
| Font | Segoe UI Variable, 14px, Regular (400) |
| Placeholder color | TextFillColorSecondary |
| Line height | 20px |
| Header label gap | 4px (between header and input) |
| Header font | 14px, Regular |

## Structure

```
┌────────────────────────────────────┐
│ Header label (optional)            │
├────────────────────────────────────┤
│ ┌────────────────────────────────┐ │
│ │ [text input area]    [clear X] │ │
│ └────────────────────────────────┘ │
│ Description text (optional)        │
└────────────────────────────────────┘
```

## States

| State | Background | Border | Bottom Stroke |
|-------|-----------|--------|---------------|
| Rest | ControlFillColorDefault | ControlStrokeColorDefault (1px) | ControlStrokeColorSecondary (slightly darker) |
| Hover | ControlFillColorSecondary | ControlStrokeColorDefault | ControlStrokeColorSecondary |
| Focused | ControlFillColorInputActive (`#FFFFFF` / `#1EFFFFFF`) | ControlStrokeColorDefault | **AccentColor (2px)** |
| Disabled | ControlFillColorDisabled | ControlStrokeColorDefault (reduced) | None |
| Error | Same as rest | — | SystemFillColorCritical (2px bottom) |

### Focus Bottom Accent

The key visual indicator for TextBox focus is a **2px accent-colored bottom stroke** that animates in from center:

- Color: SystemAccentColor
- Width: 2px
- Animation: Scales from 0% to 100% width, 200ms, Decelerate easing
- Originates from center of the bottom edge

This accent underline is the primary focus indicator; there is no outer focus ring on TextBox.

## Clear Button

- Appears when text is present and the control is focused
- Icon: `&#xE10A;` (Cancel/X glyph), 12x12px
- Hit area: 30x32px
- Background: SubtleFillColorTransparent → SubtleFillColorSecondary on hover
- Corner radius: 4px

## Multi-line (TextBox with AcceptsReturn)

| Property | Value |
|----------|-------|
| Min height | 64px (approximately 2 lines) |
| Max height | Configurable, scroll if overflow |
| Padding | Same as single-line |
| Vertical scrollbar | Auto-visible when content overflows |

## Character Count / Description

- Description text appears below the input
- Color: TextFillColorSecondary
- Font: 12px Caption, Regular

## Selection

- Selection highlight: AccentFillColorSelectedTextBackground
- Selected text color: TextOnAccentFillColorSelectedText (white)

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Bottom accent stroke in | 200ms | Decelerate |
| Bottom accent stroke out | 100ms | Accelerate |
| Clear button fade in | 100ms | Control fast |
| Background fill transition | 100ms | Control fast |
