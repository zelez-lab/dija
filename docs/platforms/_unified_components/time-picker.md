# Time Picker

A control for selecting a time value (hours, minutes, and optionally AM/PM), displayed as spinning wheels, a clock dial, or text input fields.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIDatePicker (time / countdownTimer modes) | Documented |
| macOS | NSDatePicker (hourMinuteSecond elements) | Documented |
| Android | M3 TimePicker (dial / input) | Documented |
| Windows | TimePicker (WinUI 3, looping selector) | Documented |
| Linux | GtkSpinButton (time configuration) | Documented |

---

## iOS

Source: UIDatePicker (time mode), SwiftUI DatePicker

### Modes

| Mode | Components Shown |
|------|-----------------|
| Time | Hour, Minute, AM/PM |
| Countdown Timer | Hours, Minutes |

### Compact Style (Time)

Same compact appearance as DatePicker (see Date Picker). A tappable label displaying the current time; tapping expands to inline time wheels.

| Property | Value |
|----------|-------|
| Height (collapsed) | 34pt |
| Background (collapsed) | tertiarySystemFill |
| Corner radius (collapsed) | 6pt |
| Font (collapsed) | SF Pro Regular, 17pt |
| Text color (collapsed) | tintColor |

### Inline Time Component

| Property | Value |
|----------|-------|
| Layout | Two wheel columns (hours, minutes) |
| Wheel height | ~130pt |
| Row height | 32pt |
| AM/PM | Third column if 12-hour format |
| Font | SF Pro Regular, 23pt |
| Separator | Colon (:) between hours and minutes |

### Wheels Style

Same as UIPickerView metrics (see Select), with time-specific components:

| Component | Typical Width |
|-----------|--------------|
| Hour | ~50pt |
| Minute | ~50pt |
| AM/PM | ~65pt |

### Accessibility

| Property | Value |
|----------|-------|
| Time picker | "Time picker, [current time]" |
| Wheel | Each column adjustable via swipe up/down |

---

## macOS

Reference: NSDatePicker (time elements), Apple HIG (macOS 14+).

NSDatePicker handles time selection through its `datePickerElements` property. When set to `.hourMinuteSecond`, the control displays time components.

### Configuration

| Element              | Description                    |
|----------------------|--------------------------------|
| `.hourMinuteSecond`  | Time components (hour, minute, second) |

### Metrics

Same as NSDatePicker (see Date Picker). The `.textFieldAndStepper` style shows editable time segments with stepper arrows.

| Control Size | Height (pt) | Stepper Width (pt) | Font Size (pt) |
|-------------|-------------|---------------------|----------------|
| Mini        | 16          | 13                  | 9              |
| Small       | 19          | 14                  | 11             |
| Regular     | 22          | 15                  | 13             |
| Large       | 28          | 18                  | 15             |

### Clock Display (`.clockAndCalendar` with time elements)

| Property                  | Value (pt)     |
|---------------------------|----------------|
| Clock diameter             | 122            |
| Hour hand length           | ~35            |
| Minute hand length         | ~50            |
| Center dot                 | 6              |

### Colors

Same as NSDatePicker colors (see Date Picker).

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Tab             | Move to next time component                |
| Shift+Tab       | Move to previous time component            |
| Up Arrow        | Increment current component                |
| Down Arrow      | Decrement current component                |

---

## Android

Source: Material Design 3, TimePicker (dial / input modes)

### Styles

| Style | Description |
|-------|-------------|
| Dial | Clock dial with draggable handle for hour/minute |
| Input | Two text fields for hour and minute with keyboard entry |

### Dial Metrics

| Property | Value |
|----------|-------|
| Container width | 328dp |
| Clock face diameter | 256dp |
| Clock face corner radius | Full circle |
| Hour/minute number font | Body Large (Roboto Regular, 16sp) |
| Selected number bg | primary color circle |
| Selector handle size | 48dp |
| Selector line | 2dp, primary color |
| Center dot | 8dp, primary color |
| Period selector (AM/PM) | 52dp wide, 80dp tall, 8dp corner radius |

### Input Metrics

| Property | Value |
|----------|-------|
| Time field width | 96dp |
| Time field height | 72dp |
| Time field corner radius | 8dp |
| Time digit font | Display Large (Roboto Regular, 57sp) |
| Separator | Colon, Display Large font |
| AM/PM toggle | Segmented button, 52 x 38dp per segment |

### Accessibility

| Property | Value |
|----------|-------|
| TimePicker | "Time picker, [current time]" |

---

## Windows

Source: WinUI 3 / Windows App SDK, Fluent Design System

### TimePicker (Looping Selector)

Spinning-wheel style selector for time components.

#### Metrics

| Property | Value |
|----------|-------|
| Control height | 32px (collapsed flyout trigger) |
| Columns | Hour, Minute, AM/PM (if 12-hour) |
| Flyout column width | ~80px per column |
| Flyout row height | 40px |
| Flyout corner radius | 8px |
| Font | Segoe UI Variable, 14px (trigger), 16px (flyout items) |
| Visible items | ~5 per column |

#### Key Properties

| Property | Description |
|----------|-------------|
| Time | Currently selected TimeSpan |
| MinuteIncrement | Step for minute values (default 1) |
| ClockIdentifier | "12HourClock" or "24HourClock" |
| Header | Optional label above the control |

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Enter / Space | Open flyout |
| Up/Down Arrow | Scroll through values in focused column |
| Tab | Move to next column |
| Enter | Confirm selection |
| Escape | Close flyout |

### Accessibility

| Property | Value |
|----------|-------|
| TimePicker role | Group with looping selector children |
| Narrator | "Time picker, [current time]" |

---

## Linux

Source: GTK 4 (docs.gtk.org/gtk4), libadwaita

### Overview

GTK 4 does not provide a dedicated time picker widget. Time selection is typically implemented using **GtkSpinButton** widgets configured for hours/minutes, or via **AdwEntryRow** / **AdwSpinRow** in a boxed list for a more polished appearance.

### GtkSpinButton (Time)

#### Configuration

| Property | Hour | Minute |
|----------|------|--------|
| Range | 0-23 (24h) or 1-12 (12h) | 0-59 |
| Increment | 1 | 1 (or 5, 15) |
| Wrap | Yes | Yes |
| Digits | 0 | 0 |
| Output format | Zero-padded (01, 02, ...) | Zero-padded (00, 05, ...) |

#### Metrics (Adwaita)

| Property | Value |
|----------|-------|
| SpinButton height | 34px |
| SpinButton min width | 60px |
| +/- button width | 34px |
| Font | Adwaita Sans Regular, 15px |
| Corner radius | 6px |
| Separator between fields | Colon label, ~8px padding |

### Common Layout

```
+--------+     +--------+     +--------+
| [<] HH [>] : [<] MM [>] : [<] SS [>] |
+--------+     +--------+     +--------+
```

Typically arranged as a horizontal box with GtkLabel separators (":") between spin buttons.

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Up/Down Arrow | Increment/decrement value |
| Page Up/Page Down | Increment/decrement by 10 |
| Home | Set to minimum |
| End | Set to maximum |
| Tab | Move to next spin button |

### Accessibility

| Property | Value |
|----------|-------|
| Role | GTK_ACCESSIBLE_ROLE_SPIN_BUTTON |
| Value | Current numeric value announced |
| Range | Min/max bounds announced |
