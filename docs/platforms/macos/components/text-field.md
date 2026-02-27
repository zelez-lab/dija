# macOS Text Field (NSTextField)

Reference: NSTextField, NSTextField.BezelStyle, NSTextInputClient, Apple HIG (macOS 14+).

## Overview

`NSTextField` is the standard single-line text input on macOS. It supports two bezel styles, multiple control sizes, and integrates deeply with the macOS text system (spell checking, autocorrect, input methods).

## Bezel Styles

| Style                           | Description                                | Usage                       |
|---------------------------------|--------------------------------------------|-----------------------------|
| `.squareBezel` (default)        | Flat rectangular bezel with subtle border  | Forms, preferences          |
| `.roundedBezel`                 | Capsule/pill-shaped bezel                  | Search-like fields, toolbar |

## Metrics

### Square Bezel (`.squareBezel`)

| Control Size | Height (pt) | Corner Radius (pt) | Font Size (pt) | Vertical Padding (pt) | Horizontal Padding (pt) |
|-------------|-------------|---------------------|----------------|----------------------|------------------------|
| Mini        | 16          | 2                   | 9              | 2                    | 3                      |
| Small       | 19          | 3                   | 11             | 2                    | 4                      |
| Regular     | 22          | 5                   | 13             | 3                    | 5                      |
| Large       | 28          | 6                   | 15             | 4                    | 7                      |

### Rounded Bezel (`.roundedBezel`)

| Control Size | Height (pt) | Corner Radius (pt) | Font Size (pt) |
|-------------|-------------|---------------------|----------------|
| Mini        | 16          | 8 (capsule)         | 9              |
| Small       | 19          | 9.5 (capsule)       | 11             |
| Regular     | 22          | 11 (capsule)        | 13             |
| Large       | 28          | 14 (capsule)        | 15             |

## Colors

### Background

| State        | Light Mode                    | Dark Mode                     |
|-------------|-------------------------------|-------------------------------|
| Normal       | `#FFFFFF`                     | `#1E1E1E`                     |
| Focused      | `#FFFFFF`                     | `#1E1E1E`                     |
| Disabled     | `rgba(255,255,255,0.50)`      | `rgba(30,30,30,0.50)`         |

### Border

| State        | Light Mode                    | Dark Mode                     |
|-------------|-------------------------------|-------------------------------|
| Normal       | `rgba(0,0,0,0.12)`           | `rgba(255,255,255,0.12)`      |
| Hover        | `rgba(0,0,0,0.18)`           | `rgba(255,255,255,0.18)`      |
| Focused      | controlAccentColor (0.50 alpha focus ring) | controlAccentColor (0.50 alpha focus ring) |
| Disabled     | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.06)`      |
| Error        | `#FF3B30`                     | `#FF453A`                     |

Border width: 0.5 pt (1 px on Retina).

### Text Colors

| Element           | Light Mode                | Dark Mode                   |
|-------------------|---------------------------|-----------------------------|
| Text              | `#000000` (textColor)     | `#FFFFFF` (textColor)       |
| Placeholder       | `rgba(0,0,0,0.25)`       | `rgba(255,255,255,0.25)`    |
| Selection bg      | `#B3D7FF`                 | `#3F638B`                   |
| Disabled text     | `rgba(0,0,0,0.25)`       | `rgba(255,255,255,0.25)`    |

## Shadow

Text field has a subtle inner shadow:

```
Color:   rgba(0, 0, 0, 0.04)
Offset:  (0, 1) pt inward
Blur:    1 pt
Type:    inset
```

When focused, the inner shadow is removed and replaced by the focus ring.

## Focus Ring

```
Color:   controlAccentColor at 50% opacity
Width:   3 pt stroke
Offset:  2 pt outset from field bounds
Radius:  field corner radius + 3 pt
```

On focus, the field border color intensifies and the focus ring animates in over 150 ms.

## States

| State        | Visual Changes                                          |
|--------------|--------------------------------------------------------|
| Normal       | White background, 0.5 pt border, subtle inner shadow    |
| Hover        | Slightly darker border                                  |
| Focused      | Focus ring, no inner shadow, border matches accent color |
| Editing      | Cursor visible, text selectable                         |
| Disabled     | 50% opacity background, 25% opacity text/border         |
| Read-only    | Same as normal but cursor changes to arrow               |

## Cursor

| Context                | Cursor              |
|------------------------|---------------------|
| Over editable field    | I-Beam              |
| Over non-editable      | Arrow               |
| Dragging selection     | Arrow               |
| Over selection         | I-Beam              |

## Placeholder Text

- Font: Same as input text (system font at control's font size)
- Weight: Regular
- Color: `placeholderTextColor` (`rgba(0,0,0,0.25)` light, `rgba(255,255,255,0.25)` dark)
- Disappears when field has focus and user starts typing
- Optionally remains until text is entered (attributed placeholder)

## Text Selection

| Property                    | Value                              |
|-----------------------------|------------------------------------|
| Selection background        | `selectedTextBackgroundColor`      |
| Selection text color         | `selectedTextColor`               |
| Insertion point (caret)     | `insertionPointColor` (accent)    |
| Caret width                  | 1 pt                             |
| Caret blink rate             | 500 ms on, 500 ms off            |

## Secure Text Field (NSSecureTextField)

Same metrics as `NSTextField` but:
- Input is masked with bullet characters (U+2022)
- Bullet spacing: standard character width
- No copy/cut support
- No spell checking
- Password autofill integration (Keychain)

## Multi-line (NSTextView in NSScrollView)

For multi-line text input, macOS uses `NSTextView` embedded in `NSScrollView`, not `NSTextField`. Key differences:

| Property          | NSTextField            | NSTextView                  |
|-------------------|------------------------|-----------------------------|
| Lines             | Single                 | Multi                       |
| Scroll            | No (clips)             | Yes (scroll view)           |
| Rich text         | No (plain only)        | Yes (optional)              |
| Min height        | Control size height    | Arbitrary                   |
| Border            | Bezel style            | `NSScrollView` border       |

## Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Focus ring appear    | 150           | Ease Out      |
| Focus ring disappear | 200           | Ease In       |
| Placeholder fade     | 100           | Ease Out      |
| Error state border   | 200           | Ease In Out   |

## Keyboard Shortcuts

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

## Dija Skin Mapping

```
comp! TextInput {
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
