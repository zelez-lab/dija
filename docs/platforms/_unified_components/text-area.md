# Text Area

A multi-line text input control that allows users to enter and edit longer text content, with support for scrolling, rich text, and auto-sizing.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UITextView | Documented |
| macOS | NSTextView (in NSScrollView) | Documented |
| Android | M3 TextField (multiline) | Documented |
| Windows | WinUI 3 TextBox (AcceptsReturn) | Documented |
| Linux | GtkTextView (GNOME/Adwaita) | Documented |

---

## iOS

Source: UITextView

### Metrics

| Property | Value |
|----------|-------|
| Padding (text container inset) | 8pt all sides (default) |
| Font | SF Pro Regular, 17pt |
| Text color | label (`#000000` / `#FFFFFF`) |
| Scrollable | Yes (when content exceeds bounds) |
| Link detection | Optional (data detectors) |
| Link color | link color (`#007AFF` / `#0984FF`) |
| Cursor color | tintColor (systemBlue by default) |
| Cursor width | 2pt |
| Selection highlight | tintColor @ 0.25 |

### Appearance

UITextView has no built-in border or background by default. Apps typically add:

| Property | Value |
|----------|-------|
| Background | systemBackground or secondarySystemBackground |
| Corner radius | 10pt (when styled) |
| Border | Optional, 0.5pt separator color |

### States

| State | Effect |
|-------|--------|
| Normal | Standard appearance |
| Focused | Cursor blinks, keyboard appears |
| Disabled | Reduced opacity (alpha 0.3), non-interactive |
| Read-only | Selectable but not editable (`isEditable = false`) |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Text field (multiline) |
| VoiceOver | "[Content], text field, [trait]" |

---

## macOS

Reference: NSTextView in NSScrollView, Apple HIG (macOS 14+).

### Overview

For multi-line text input, macOS uses `NSTextView` embedded in `NSScrollView`, not `NSTextField`.

### Comparison with NSTextField

| Property          | NSTextField            | NSTextView                  |
|-------------------|------------------------|-----------------------------|
| Lines             | Single                 | Multi                       |
| Scroll            | No (clips)             | Yes (scroll view)           |
| Rich text         | No (plain only)        | Yes (optional)              |
| Min height        | Control size height    | Arbitrary                   |
| Border            | Bezel style            | `NSScrollView` border       |

### Metrics

| Property | Value |
|----------|-------|
| Text container inset | 5pt horizontal, 0pt vertical (default) |
| Font | SF Pro Regular, 13pt (system default) |
| Line spacing | ~1.2x font size |
| Scroll view border | 1px, same as NSTextField |
| Corner radius | 5pt (matches NSTextField .squareBezel) |

### Colors

| Element | Light Mode | Dark Mode |
|---------|------------|-----------|
| Background | `#FFFFFF` | `#1E1E1E` |
| Text | textColor | textColor |
| Selection bg | `#B3D7FF` | `#3F638B` |
| Insertion point | controlAccentColor | controlAccentColor |

### Focus Ring

Same as NSTextField: 3pt accent-colored stroke, 2pt outset.

### Keyboard Shortcuts

Standard macOS text editing shortcuts apply (Cmd+A, Cmd+C, Cmd+V, etc.), plus:

| Action | Keys |
|--------|------|
| New line | Return |
| Insert tab | Option+Tab (when tab moves focus) |
| Move to paragraph start | Ctrl+A / Cmd+Up |
| Move to paragraph end | Ctrl+E / Cmd+Down |

---

## Android

Source: M3 TextField (multiline mode)

### Overview

Android's M3 TextField supports multiline input via `singleLine = false` in Compose or `android:inputType="textMultiLine"` in XML. The same Filled/Outlined variants apply.

### Metrics

Same as single-line TextField (see Text Field), with these additions:

| Property | Value |
|----------|-------|
| Min height | 56dp (same as single-line) |
| Max height | Configurable, scrollable when exceeded |
| Line count | Configurable via `minLines` / `maxLines` |
| Vertical padding (content) | 16dp top and bottom |
| Scrollable | Yes (when content exceeds maxLines) |

### Behavior

| Property | Value |
|----------|-------|
| Label | Floats when focused/has content (same as single-line) |
| Character counter | Optional, right-aligned below field |
| Supporting text | Below field, 4dp gap |
| Error state | Same styling as single-line (error color on indicator/label) |

---

## Windows

Source: WinUI 3 TextBox (AcceptsReturn = true)

### Overview

A WinUI 3 TextBox becomes multi-line when `AcceptsReturn` is set to `true`. The same TextBox control handles both modes.

### Metrics

| Property | Value |
|----------|-------|
| Min height | 64px (approximately 2 lines) |
| Max height | Configurable, scroll if overflow |
| Padding | Same as single-line (11px horizontal, 5px top, 6px bottom) |
| Vertical scrollbar | Auto-visible when content overflows |
| Font | Segoe UI Variable, 14px, Regular (400) |
| Line height | 20px |

### States

Same as single-line TextBox (see Text Field), including the 2px accent bottom stroke on focus.

### Behavior

| Property | Value |
|----------|-------|
| Text wrapping | TextWrapping.Wrap (default when AcceptsReturn) |
| Scroll | Vertical scrollbar appears on overflow |
| Tab | Inserts tab character (when AcceptsReturn, Tab doesn't move focus) |
| Clear button | Not shown in multi-line mode |

---

## Linux

Source: GTK 4 (docs.gtk.org/gtk4), libadwaita

### Overview

GTK 4 uses `GtkTextView` for multi-line text input, typically wrapped in a `GtkScrolledWindow`. This is distinct from `GtkEntry` (single-line).

### Metrics

| Property | Value |
|----------|-------|
| Min height | Configurable (default expands to content) |
| Padding | 6px all sides |
| Font | Adwaita Sans Regular, 15px |
| Corner radius | 6px (when styled directly) |
| Border | 1px, same style as GtkEntry |
| Scrollbar | Overlay style via GtkScrolledWindow |

### Colors

Same as GtkEntry (see Text Field):

| Element | Light | Dark |
|---------|-------|------|
| Background | `#FFFFFF` (view_bg_color) | `#1E1E1E` |
| Text | `#2E3436` | `#FFFFFF` |
| Border (rest) | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Border (focused) | 2px accent_color | 2px accent_color |

### States

| State | Border | Notes |
|-------|--------|-------|
| Rest | 1px subtle | -- |
| Focused | 2px accent | -- |
| Disabled | 1px dim | Content opacity 0.5 |

### CSS Node

```
textview
+-- text
+-- [scrollbar]  (via GtkScrolledWindow)
```

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Return | Insert new line |
| Tab | Insert tab (when not in a form context) |
| Ctrl+A | Select all |
| Ctrl+C / Ctrl+V | Copy / paste |
| Ctrl+Z / Ctrl+Shift+Z | Undo / redo |
