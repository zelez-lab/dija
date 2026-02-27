# iOS — Text Field (UITextField)

Source: UITextField, UITextView

## Appearance

| Property | Value |
|----------|-------|
| Background | secondarySystemFill (light: `#787880` @ 0.12, dark: `#787880` @ 0.24) |
| Background (alternate) | systemGray6 (light: `#F2F2F7`, dark: `#1C1C1E`) |
| Corner radius | 10pt |
| Corner curve | `.continuous` (superellipse) |
| Border | None (flat fill, not outlined) |
| Height | 36pt (default), 44pt (in forms) |

Note: The background color varies by context. In search bars, it uses tertiarySystemFill. In forms/settings, it uses secondarySystemGroupedBackground (white/`#1C1C1E`).

## Metrics

| Property | Value |
|----------|-------|
| Padding (vertical) | 7pt |
| Padding (horizontal) | 8pt (left), 28pt (right, when clear button shown) |
| Font | SF Pro Regular, 17pt |
| Line height | 22pt |
| Placeholder font | SF Pro Regular, 17pt |
| Placeholder color | placeholderText (`#3C3C43` @ 0.30 / `#EBEBF5` @ 0.30) |
| Text color | label (`#000000` / `#FFFFFF`) |
| Cursor (caret) color | tintColor (systemBlue by default) |
| Cursor width | 2pt |
| Selection highlight | tintColor @ 0.25 |

## Clear Button

| Property | Value |
|----------|-------|
| Icon | Circle with X (SF Symbol: `xmark.circle.fill`) |
| Size | 17pt diameter |
| Color | tertiaryLabel (`#3C3C43` @ 0.30 / `#EBEBF5` @ 0.30) |
| Position | Right edge, vertically centered, 6pt right padding |
| Visibility | Appears when text is present (configurable) |

## Accessory Views

| Position | Usage | Padding |
|----------|-------|---------|
| Left view | Icons, labels, currency symbols | 8pt left margin |
| Right view | Clear button, disclosure, custom | 8pt right margin |

## States

| State | Effect |
|-------|--------|
| Normal | Standard appearance |
| Focused | No visible ring (cursor blinks, tint-colored). On iPad with keyboard: subtle shadow or highlight (system-managed) |
| Disabled | Reduced opacity (alpha 0.3), non-interactive |
| Error | No built-in error state (app must style manually) |

### Focus Animation

| Property | Value |
|----------|-------|
| Cursor blink rate | ~530ms on, ~530ms off |
| Cursor appear | Fade in, ~0.1s |
| Text selection handles | tintColor, capsule-shaped |

## Secure Text Entry

| Property | Value |
|----------|-------|
| Bullet character | `U+2022` (bullet) |
| Bullet size | Same as font size |
| Last character reveal | ~1.5s before replacing with bullet |
| Toggle button | Eye icon (SF Symbol: `eye` / `eye.slash`) |

## Keyboard Types

Common keyboard configurations affecting the text field's on-screen keyboard:

| Type | Description |
|------|-------------|
| `.default` | Standard alpha keyboard |
| `.numberPad` | Numbers only, no return key |
| `.decimalPad` | Numbers + decimal point |
| `.emailAddress` | Alpha + @ and . prominent |
| `.URL` | Alpha + .com, / prominent |
| `.phonePad` | Phone dial pad layout |
| `.asciiCapable` | Standard without emoji |

## Text View (UITextView) — Multi-line

| Property | Value |
|----------|-------|
| Padding (text container inset) | 8pt all sides (default) |
| Font | SF Pro Regular, 17pt |
| Scrollable | Yes (when content exceeds bounds) |
| Link detection | Optional (data detectors) |
| Link color | link color (`#007AFF` / `#0984FF`) |
