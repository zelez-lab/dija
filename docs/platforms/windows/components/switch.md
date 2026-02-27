# Windows — ToggleSwitch

Source: WinUI 3 ToggleSwitch control

## Track

| Property | Off (rest) | On (rest) |
|----------|-----------|-----------|
| Width | 40px | 40px |
| Height | 20px | 20px |
| Corner radius | 10px (fully rounded pill) |
| Fill (off) | ControlAltFillColorSecondary (`#06000000` / `#19FFFFFF`) | AccentFillColorDefault (SystemAccentColor) |
| Border (off) | ControlStrongStrokeColorDefault (`#72000000` / `#9AFFFFFF`) 1px | ControlStrokeColorOnAccentDefault 1px |
| Fill (on) | — | AccentFillColorDefault |

## Knob (Thumb)

| Property | Off | On |
|----------|-----|-----|
| Diameter | 12px | 14px (grows on toggle) |
| Color | TextFillColorSecondary (`#9E000000` / `#C5FFFFFF`) | TextOnAccentFillColorPrimary (white/black) |
| Shape | Circle, centered vertically |
| Horizontal position | Left inset ~4px | Right inset ~4px |

The knob grows from 12px to 14px when the switch is in the "on" position.

## States

### Off States

| State | Track fill | Track border | Knob |
|-------|-----------|-------------|------|
| Rest | ControlAltFillColorSecondary | ControlStrongStrokeColorDefault (1px) | 12px, TextFillColorSecondary |
| Hover | ControlAltFillColorTertiary | ControlStrongStrokeColorDefault (1px) | 14px, TextFillColorPrimary |
| Pressed | ControlAltFillColorQuarternary | ControlStrongStrokeColorDisabled (1px) | 17px wide (oval stretch), TextFillColorSecondary |
| Disabled | ControlAltFillColorDisabled | ControlStrongStrokeColorDisabled (1px) | 12px, TextFillColorDisabled |

### On States

| State | Track fill | Track border | Knob |
|-------|-----------|-------------|------|
| Rest | AccentFillColorDefault | ControlStrokeColorOnAccentDefault (1px) | 14px, white |
| Hover | AccentFillColorSecondary | ControlStrokeColorOnAccentDefault (1px) | 14px, white |
| Pressed | AccentFillColorTertiary | ControlStrokeColorOnAccentTertiary (1px) | 17px wide (oval stretch), white |
| Disabled | AccentFillColorDisabled | transparent | 12px, TextOnAccentFillColorDisabled |

## Labels

| Property | Value |
|----------|-------|
| On label | "On" (localizable) |
| Off label | "Off" (localizable) |
| Font | 14px, Regular |
| Position | Right of track |
| Gap (track to label) | 8px |
| Header (optional) | Above the control, 14px Regular, 4px gap |

## Full Control Layout

```
Header label (optional)
┌──────────────────────────┐
│ [═══●]  On/Off label     │
└──────────────────────────┘
```

Total control area:
- Min width: 154px (ThemeResource `ToggleSwitchThemeMinWidth`)
- Height: 32px (touch target)

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Knob slide (off → on) | 200ms | Decelerate |
| Knob slide (on → off) | 200ms | Decelerate |
| Track fill color change | 100ms | Control fast |
| Knob size change (rest → hover) | 100ms | Control fast |
| Knob stretch (pressed) | 100ms | Control fast |
| Knob unstretch (release) | 150ms | Decelerate |
