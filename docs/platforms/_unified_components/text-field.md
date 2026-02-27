# Text Field

A single-line text input control that allows the user to enter and edit text, with support for placeholder text, validation states, and secure entry for passwords. For multi-line text input, see Text Area.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UITextField | Documented |
| macOS | NSTextField / NSSecureTextField | Documented |
| Android | Material Design 3 Text Fields (Filled / Outlined) | Documented |
| Windows | WinUI 3 TextBox | Documented |
| Linux | GtkEntry (GNOME/Adwaita) | Documented |

## iOS

Source: UITextField

### Appearance

| Property | Value |
|----------|-------|
| Background | secondarySystemFill (light: `#787880` @ 0.12, dark: `#787880` @ 0.24) |
| Background (alternate) | systemGray6 (light: `#F2F2F7`, dark: `#1C1C1E`) |
| Corner radius | 10pt |
| Corner curve | `.continuous` (superellipse) |
| Border | None (flat fill, not outlined) |
| Height | 36pt (default), 44pt (in forms) |

Note: The background color varies by context. In search bars, it uses tertiarySystemFill. In forms/settings, it uses secondarySystemGroupedBackground (white/`#1C1C1E`).

### Metrics

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

### Clear Button

| Property | Value |
|----------|-------|
| Icon | Circle with X (SF Symbol: `xmark.circle.fill`) |
| Size | 17pt diameter |
| Color | tertiaryLabel (`#3C3C43` @ 0.30 / `#EBEBF5` @ 0.30) |
| Position | Right edge, vertically centered, 6pt right padding |
| Visibility | Appears when text is present (configurable) |

### Accessory Views

| Position | Usage | Padding |
|----------|-------|---------|
| Left view | Icons, labels, currency symbols | 8pt left margin |
| Right view | Clear button, disclosure, custom | 8pt right margin |

### States

| State | Effect |
|-------|--------|
| Normal | Standard appearance |
| Focused | No visible ring (cursor blinks, tint-colored). On iPad with keyboard: subtle shadow or highlight (system-managed) |
| Disabled | Reduced opacity (alpha 0.3), non-interactive |
| Error | No built-in error state (app must style manually) |

#### Focus Animation

| Property | Value |
|----------|-------|
| Cursor blink rate | ~530ms on, ~530ms off |
| Cursor appear | Fade in, ~0.1s |
| Text selection handles | tintColor, capsule-shaped |

### Secure Text Entry

| Property | Value |
|----------|-------|
| Bullet character | `U+2022` (bullet) |
| Bullet size | Same as font size |
| Last character reveal | ~1.5s before replacing with bullet |
| Toggle button | Eye icon (SF Symbol: `eye` / `eye.slash`) |

### Keyboard Types

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

## macOS

Reference: NSTextField, NSTextField.BezelStyle, NSTextInputClient, Apple HIG (macOS 14+).

### Overview

`NSTextField` is the standard single-line text input on macOS. It supports two bezel styles, multiple control sizes, and integrates deeply with the macOS text system (spell checking, autocorrect, input methods).

### Bezel Styles

| Style                           | Description                                | Usage                       |
|---------------------------------|--------------------------------------------|-----------------------------|
| `.squareBezel` (default)        | Flat rectangular bezel with subtle border  | Forms, preferences          |
| `.roundedBezel`                 | Capsule/pill-shaped bezel                  | Search-like fields, toolbar |

### Metrics

#### Square Bezel (`.squareBezel`)

| Control Size | Height (pt) | Corner Radius (pt) | Font Size (pt) | Vertical Padding (pt) | Horizontal Padding (pt) |
|-------------|-------------|---------------------|----------------|----------------------|------------------------|
| Mini        | 16          | 2                   | 9              | 2                    | 3                      |
| Small       | 19          | 3                   | 11             | 2                    | 4                      |
| Regular     | 22          | 5                   | 13             | 3                    | 5                      |
| Large       | 28          | 6                   | 15             | 4                    | 7                      |

#### Rounded Bezel (`.roundedBezel`)

| Control Size | Height (pt) | Corner Radius (pt) | Font Size (pt) |
|-------------|-------------|---------------------|----------------|
| Mini        | 16          | 8 (capsule)         | 9              |
| Small       | 19          | 9.5 (capsule)       | 11             |
| Regular     | 22          | 11 (capsule)        | 13             |
| Large       | 28          | 14 (capsule)        | 15             |

### Colors

#### Background

| State        | Light Mode                    | Dark Mode                     |
|-------------|-------------------------------|-------------------------------|
| Normal       | `#FFFFFF`                     | `#1E1E1E`                     |
| Focused      | `#FFFFFF`                     | `#1E1E1E`                     |
| Disabled     | `rgba(255,255,255,0.50)`      | `rgba(30,30,30,0.50)`         |

#### Border

| State        | Light Mode                    | Dark Mode                     |
|-------------|-------------------------------|-------------------------------|
| Normal       | `rgba(0,0,0,0.12)`           | `rgba(255,255,255,0.12)`      |
| Hover        | `rgba(0,0,0,0.18)`           | `rgba(255,255,255,0.18)`      |
| Focused      | controlAccentColor (0.50 alpha focus ring) | controlAccentColor (0.50 alpha focus ring) |
| Disabled     | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.06)`      |
| Error        | `#FF3B30`                     | `#FF453A`                     |

Border width: 0.5 pt (1 px on Retina).

#### Text Colors

| Element           | Light Mode                | Dark Mode                   |
|-------------------|---------------------------|-----------------------------|
| Text              | `#000000` (textColor)     | `#FFFFFF` (textColor)       |
| Placeholder       | `rgba(0,0,0,0.25)`       | `rgba(255,255,255,0.25)`    |
| Selection bg      | `#B3D7FF`                 | `#3F638B`                   |
| Disabled text     | `rgba(0,0,0,0.25)`       | `rgba(255,255,255,0.25)`    |

### Shadow

Text field has a subtle inner shadow:

```
Color:   rgba(0, 0, 0, 0.04)
Offset:  (0, 1) pt inward
Blur:    1 pt
Type:    inset
```

When focused, the inner shadow is removed and replaced by the focus ring.

### Focus Ring

```
Color:   controlAccentColor at 50% opacity
Width:   3 pt stroke
Offset:  2 pt outset from field bounds
Radius:  field corner radius + 3 pt
```

On focus, the field border color intensifies and the focus ring animates in over 150 ms.

### States

| State        | Visual Changes                                          |
|--------------|--------------------------------------------------------|
| Normal       | White background, 0.5 pt border, subtle inner shadow    |
| Hover        | Slightly darker border                                  |
| Focused      | Focus ring, no inner shadow, border matches accent color |
| Editing      | Cursor visible, text selectable                         |
| Disabled     | 50% opacity background, 25% opacity text/border         |
| Read-only    | Same as normal but cursor changes to arrow               |

### Cursor

| Context                | Cursor              |
|------------------------|---------------------|
| Over editable field    | I-Beam              |
| Over non-editable      | Arrow               |
| Dragging selection     | Arrow               |
| Over selection         | I-Beam              |

### Placeholder Text

- Font: Same as input text (system font at control's font size)
- Weight: Regular
- Color: `placeholderTextColor` (`rgba(0,0,0,0.25)` light, `rgba(255,255,255,0.25)` dark)
- Disappears when field has focus and user starts typing
- Optionally remains until text is entered (attributed placeholder)

### Text Selection

| Property                    | Value                              |
|-----------------------------|------------------------------------|
| Selection background        | `selectedTextBackgroundColor`      |
| Selection text color         | `selectedTextColor`               |
| Insertion point (caret)     | `insertionPointColor` (accent)    |
| Caret width                  | 1 pt                             |
| Caret blink rate             | 500 ms on, 500 ms off            |

### Secure Text Field (NSSecureTextField)

Same metrics as `NSTextField` but:
- Input is masked with bullet characters (U+2022)
- Bullet spacing: standard character width
- No copy/cut support
- No spell checking
- Password autofill integration (Keychain)

### Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Focus ring appear    | 150           | Ease Out      |
| Focus ring disappear | 200           | Ease In       |
| Placeholder fade     | 100           | Ease Out      |
| Error state border   | 200           | Ease In Out   |

### Keyboard Shortcuts

| Action                   | Keys                        |
|--------------------------|-----------------------------|
| Select all               | Cmd+A                       |
| Copy                     | Cmd+C                       |
| Cut                      | Cmd+X                       |
| Paste                    | Cmd+V                       |
| Undo                     | Cmd+Z                       |
| Redo                     | Cmd+Shift+Z                 |
| Move to line start       | Cmd+Left / Ctrl+A           |
| Move to line end         | Cmd+Right / Ctrl+E          |
| Delete word back         | Option+Delete               |
| Delete word forward      | Option+Fn+Delete            |
| Move word left           | Option+Left                 |
| Move word right          | Option+Right                |

### Dija Skin Mapping

```
comp! TextField {
    attr placeholder, &str, default: ""
    attr disabled, bool, default: false
    attr secure, bool, default: false
    attr size, Size, default: Size::MD

    // macOS skin maps:
    // Size::XS  -> controlSize .mini   -> height 16, font 9
    // Size::SM  -> controlSize .small  -> height 19, font 11
    // Size::MD  -> controlSize .regular -> height 22, font 13
    // Size::LG  -> controlSize .large  -> height 28, font 15
    // bezel = squareBezel by default
}
```

## Android

Source: m3.material.io/components/text-fields/specs

### Variants

| Variant | Background | Border | Usage |
|---------|-----------|--------|-------|
| Filled | surfaceContainerHighest | bottom line 1dp | Default preference, forms |
| Outlined | transparent | outline 1dp all sides | When filled conflicts with background |

### Metrics

| Property | Filled | Outlined |
|----------|--------|----------|
| Height | 56dp | 56dp |
| Corner radius (top) | 4dp | 4dp |
| Corner radius (bottom) | 0dp | 4dp |
| Horizontal padding | 16dp | 16dp |
| Top padding (to label) | 8dp | -- |
| Bottom padding (to input) | 8dp | -- |
| Active indicator (bottom line) | 2dp (focused) / 1dp (rest) | -- |
| Outline width | -- | 2dp (focused) / 1dp (rest) |
| Input font | Body Large (Roboto Regular, 16sp) |
| Label font (resting) | Body Large (Roboto Regular, 16sp) |
| Label font (floating) | Body Small (Roboto Regular, 12sp) |
| Supporting text font | Body Small (Roboto Regular, 12sp) |
| Supporting text top padding | 4dp |

### Colors

#### Filled Text Field

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container | Enabled | `#E6E0E9` (surfContainerHighest) | `#36343B` |
| Active indicator | Enabled | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Active indicator | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Label | Resting | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Label | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Input text | -- | `#1D1B20` (onSurface) | `#E6E0E9` |
| Placeholder | -- | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Leading icon | -- | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Trailing icon | -- | `#49454F` (onSurfaceVariant) | `#CAC4D0` |

#### Outlined Text Field

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container | Enabled | transparent | transparent |
| Outline | Enabled | `#79747E` (outline) | `#938F99` |
| Outline | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Label | Resting | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Label | Focused | `#6750A4` (primary) | `#D0BCFF` |
| Input text | -- | `#1D1B20` (onSurface) | `#E6E0E9` |

#### Error State

| Element | Light | Dark |
|---------|-------|------|
| Active indicator / outline | `#B3261E` (error) | `#F2B8B5` |
| Label | `#B3261E` (error) | `#F2B8B5` |
| Supporting text | `#B3261E` (error) | `#F2B8B5` |
| Trailing icon | `#B3261E` (error) | `#F2B8B5` |

### States

| State | Visual effect |
|-------|--------------|
| Enabled | Default styling |
| Hovered | State layer 8% on container, indicator 1dp |
| Focused | Label floats, indicator 2dp, primary color |
| Error | Error color on indicator/label/supporting text |
| Disabled | Container onSurface @ 4%, content onSurface @ 38% |

### Label Animation

The label text animates between resting and floating positions:
- **Resting**: centered vertically in the field, Body Large (16sp)
- **Floating**: moved to top edge, Body Small (12sp)
- **Duration**: Medium 1 (250ms)
- **Easing**: Standard decelerate

For outlined variant, the floating label sits on the outline border with a gap cut in the border behind it.

### Supporting and Counter Text

- Supporting text appears below the field, 4dp gap
- Character counter right-aligned below the field
- Both use Body Small (12sp)
- Error state turns supporting text to error color

## Windows

Source: WinUI 3 TextBox control

### Appearance

- Background: ControlFillColorDefault (`#B3FFFFFF` / `#0FFFFFFF`)
- Border: 1px ControlStrokeColorDefault (top/sides) + ControlStrokeColorSecondary (bottom)
- Corner radius: 4px (controlCornerRadius)
- No shadow

### Metrics

| Property | Value |
|----------|-------|
| Min height | 32px |
| Padding | 11px horizontal, 5px top, 6px bottom |
| Font | Segoe UI Variable, 14px, Regular (400) |
| Placeholder color | TextFillColorSecondary |
| Line height | 20px |
| Header label gap | 4px (between header and input) |
| Header font | 14px, Regular |

### Structure

```
+------------------------------------+
| Header label (optional)            |
+------------------------------------+
| +--------------------------------+ |
| | [text input area]    [clear X] | |
| +--------------------------------+ |
| Description text (optional)        |
+------------------------------------+
```

### States

| State | Background | Border | Bottom Stroke |
|-------|-----------|--------|---------------|
| Rest | ControlFillColorDefault | ControlStrokeColorDefault (1px) | ControlStrokeColorSecondary (slightly darker) |
| Hover | ControlFillColorSecondary | ControlStrokeColorDefault | ControlStrokeColorSecondary |
| Focused | ControlFillColorInputActive (`#FFFFFF` / `#1EFFFFFF`) | ControlStrokeColorDefault | **AccentColor (2px)** |
| Disabled | ControlFillColorDisabled | ControlStrokeColorDefault (reduced) | None |
| Error | Same as rest | -- | SystemFillColorCritical (2px bottom) |

#### Focus Bottom Accent

The key visual indicator for TextBox focus is a **2px accent-colored bottom stroke** that animates in from center:

- Color: SystemAccentColor
- Width: 2px
- Animation: Scales from 0% to 100% width, 200ms, Decelerate easing
- Originates from center of the bottom edge

This accent underline is the primary focus indicator; there is no outer focus ring on TextBox.

### Clear Button

- Appears when text is present and the control is focused
- Icon: `&#xE10A;` (Cancel/X glyph), 12x12px
- Hit area: 30x32px
- Background: SubtleFillColorTransparent -> SubtleFillColorSecondary on hover
- Corner radius: 4px

### Character Count / Description

- Description text appears below the input
- Color: TextFillColorSecondary
- Font: 12px Caption, Regular

### Selection

- Selection highlight: AccentFillColorSelectedTextBackground
- Selected text color: TextOnAccentFillColorSelectedText (white)

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Bottom accent stroke in | 200ms | Decelerate |
| Bottom accent stroke out | 100ms | Accelerate |
| Clear button fade in | 100ms | Control fast |
| Background fill transition | 100ms | Control fast |

## Linux

GtkEntry in Adwaita is a flat-bottomed input with a subtle border that highlights on focus with the accent color.

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FFFFFF` (view_bg_color) | `#1E1E1E` (view_bg_color) |
| Text color | `#2E3436` | `#FFFFFF` |
| Placeholder color | `rgba(46,52,54, 0.50)` | `rgba(255,255,255, 0.50)` |
| Border (rest) | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Border (focused) | 2px `--accent-color` | 2px `--accent-color` |
| Border (error) | 2px `--error-color` (`#C01C28`) | 2px `--error-color` |
| Corner radius | 6px | 6px |
| Shadow | none | none |

### Metrics

| Property | Value |
|----------|-------|
| Min height | 34px |
| Horizontal padding | 12px |
| Vertical padding | 8px |
| Corner radius | 6px |
| Font | Adwaita Sans Regular, 15px |
| Caret width | 1px |
| Caret color | `--accent-color` |
| Selection bg | `--accent-bg-color` @ 0.30 |
| Selection text | foreground (unchanged) |

### States

| State | Border | Background | Notes |
|-------|--------|------------|-------|
| Rest | 1px, `rgba(0,0,0,0.15)` | view_bg_color | -- |
| Hover | 1px, `rgba(0,0,0,0.25)` | view_bg_color | Slightly stronger border |
| Focused | 2px, accent_color | view_bg_color | Accent highlight |
| Error | 2px, error_color | view_bg_color | Red border |
| Disabled | 1px, `rgba(0,0,0,0.10)` | `rgba(0,0,0,0.04)` | Content opacity 0.5 |

### Entry Variants

#### Default Entry (GtkEntry)

Single-line text input. Used standalone or inside other widgets.

#### Password Entry (GtkPasswordEntry)

| Property | Value |
|----------|-------|
| Input masking | Bullet characters |
| Peek button | Eye icon suffix, 16x16px |
| Caps lock indicator | Warning icon suffix |

#### Search Entry (GtkSearchEntry)

| Property | Value |
|----------|-------|
| Prefix icon | Search (magnifying glass), 16x16px |
| Clear button | X icon suffix, appears when text is present |
| Placeholder | "Search..." |

#### Editable Row (AdwEntryRow)

Used inside boxed lists. Label floats above input on focus/content.

| Property | Value |
|----------|-------|
| Label position (empty, unfocused) | Inside field, placeholder-style |
| Label position (focused/has content) | Floated above, `.caption` size (13px) |
| Label color (floating) | `--accent-color` when focused |
| Row min-height | 50px (taller to accommodate floating label) |
| Horizontal padding | 12px |
| Border | none (contained within boxed list card) |

#### Spin Row (AdwSpinRow)

Number input with increment/decrement buttons inside a boxed list row.

| Property | Value |
|----------|-------|
| +/- button size | 34x34px |
| +/- button style | flat, icon only |
| Input alignment | right |

### Focus Behavior

| Property | Value |
|----------|-------|
| Focus ring | 2px accent-colored border (replaces default 1px border) |
| Focus transition | 200ms ease-in-out |
| Tab order | natural (follows DOM order) |
| Auto-select on focus | All text selected on Tab-focus, caret placed on click |

### Keyboard Support

| Key | Action |
|-----|--------|
| Tab | Move to next focusable |
| Shift+Tab | Move to previous focusable |
| Ctrl+A | Select all |
| Ctrl+C / Ctrl+V | Copy / paste |
| Ctrl+Z / Ctrl+Shift+Z | Undo / redo |
| Escape | Clear search (search entry) |
| Enter | Activate default action / submit |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Border color change | 200ms | ease-in-out |
| Floating label rise | 200ms | ease-out-cubic |
| Placeholder fade | 150ms | ease-in-out |
