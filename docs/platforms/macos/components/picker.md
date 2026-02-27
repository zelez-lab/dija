# macOS Picker (NSPopUpButton / NSDatePicker)

Reference: NSPopUpButton, NSDatePicker, NSComboBox, Apple HIG (macOS 14+).

## Overview

macOS has several picker controls for selecting values from a set of options. The primary ones are `NSPopUpButton` (dropdown selection), `NSDatePicker` (date/time selection), and `NSComboBox` (editable dropdown).

---

## NSPopUpButton (Dropdown Picker)

### Types

| Type              | Description                                      |
|-------------------|--------------------------------------------------|
| Pop-up (default)  | Displays selected item, dropdown shows all options |
| Pull-down         | Displays title, dropdown shows action list        |

### Metrics

| Control Size | Height (pt) | Corner Radius (pt) | Font Size (pt) | Arrow Width (pt) |
|-------------|-------------|---------------------|----------------|------------------|
| Mini        | 16          | 3                   | 9              | 7                |
| Small       | 19          | 4                   | 11             | 8                |
| Regular     | 22          | 6                   | 13             | 9                |
| Large       | 28          | 8                   | 15             | 11               |

| Property                  | Value (pt) |
|---------------------------|------------|
| Horizontal padding (text)  | 8          |
| Arrow padding (right)      | 6          |
| Menu item height           | 22         |
| Menu item padding (H)      | 12         |
| Menu separator height      | 9          |
| Menu corner radius         | 6          |

### Colors

| Element              | Light Mode                    | Dark Mode                      |
|----------------------|-------------------------------|--------------------------------|
| Background           | White gradient (#FFFFFF-#F5F5F5) | `rgba(255,255,255,0.10)`    |
| Border               | `rgba(0,0,0,0.12)`           | `rgba(255,255,255,0.12)`       |
| Text                 | labelColor                    | labelColor                     |
| Arrow (chevron)      | secondaryLabelColor           | secondaryLabelColor            |
| Hover bg             | Slightly brighter             | Slightly brighter              |
| Pressed bg           | `#DCDCDC`                     | `rgba(255,255,255,0.06)`       |
| Disabled bg          | `rgba(0,0,0,0.04)`           | `rgba(255,255,255,0.04)`       |
| Disabled text        | disabledControlTextColor      | disabledControlTextColor       |

### Menu Appearance

The dropdown menu uses the `.menu` vibrancy material:

| Element              | Light Mode                    | Dark Mode                      |
|----------------------|-------------------------------|--------------------------------|
| Menu background       | Menu material vibrancy        | Menu material vibrancy         |
| Fallback background   | `#FFFFFF`                     | `#353535`                      |
| Menu shadow           | rgba(0,0,0,0.20) offset (0,4) blur 20 | rgba(0,0,0,0.40) offset (0,4) blur 20 |
| Selected item bg      | controlAccentColor            | controlAccentColor             |
| Selected item text    | `#FFFFFF`                     | `#FFFFFF`                      |
| Separator             | separatorColor                | separatorColor                 |

### Arrow Indicator

The popup button shows a chevron (up/down arrows):

| Property              | Value            |
|-----------------------|------------------|
| Symbol                | Up/down chevron  |
| Size                  | ~7 pt (regular)  |
| Color                 | secondaryLabelColor |
| Position              | Right edge, vertically centered |

### Animation

| Transition              | Duration (ms) | Curve          |
|------------------------|---------------|----------------|
| Menu appear             | 150           | Ease Out       |
| Menu dismiss            | 100           | Ease In        |
| Item highlight          | 0             | Immediate      |
| Press feedback          | 30            | Ease Out       |

---

## NSDatePicker

### Styles

| Style                        | Description                                    |
|------------------------------|------------------------------------------------|
| `.textFieldAndStepper`       | Text field with stepper arrows                 |
| `.clockAndCalendar`          | Visual calendar and/or analog clock            |
| `.textField`                 | Text field only, no stepper                    |

### Elements (configurable via `datePickerElements`)

| Element              | Description                    |
|----------------------|--------------------------------|
| `.yearMonthDay`      | Date components                |
| `.hourMinuteSecond`  | Time components                |
| `.yearMonth`         | Month and year only            |
| `.era`               | Era (AD/BC)                    |
| `.timeZone`          | Time zone display              |

### Metrics (`.textFieldAndStepper`)

| Control Size | Height (pt) | Stepper Width (pt) | Font Size (pt) |
|-------------|-------------|---------------------|----------------|
| Mini        | 16          | 13                  | 9              |
| Small       | 19          | 14                  | 11             |
| Regular     | 22          | 15                  | 13             |
| Large       | 28          | 18                  | 15             |

Stepper consists of up/down arrow buttons:

| Property                  | Value          |
|---------------------------|----------------|
| Stepper button height      | Half of control height |
| Arrow size                 | ~5 pt          |
| Stepper border             | Same as text field |

### Calendar Picker (`.clockAndCalendar`)

| Property                  | Value (pt)     |
|---------------------------|----------------|
| Calendar width             | 218            |
| Calendar height            | 200            |
| Day cell size              | 28x28          |
| Header height              | 30             |
| Clock diameter             | 122            |
| Combined width             | ~340           |

### Colors (`.textFieldAndStepper`)

| Element                  | Light Mode              | Dark Mode               |
|--------------------------|-------------------------|-------------------------|
| Background               | controlBackgroundColor  | controlBackgroundColor  |
| Border                   | `rgba(0,0,0,0.12)`     | `rgba(255,255,255,0.12)`|
| Text                     | textColor               | textColor               |
| Selected segment bg      | controlAccentColor      | controlAccentColor      |
| Selected segment text    | `#FFFFFF`               | `#FFFFFF`               |
| Stepper arrows           | secondaryLabelColor     | secondaryLabelColor     |

### Calendar Colors

| Element                  | Light Mode              | Dark Mode               |
|--------------------------|-------------------------|-------------------------|
| Calendar background       | controlBackgroundColor  | controlBackgroundColor  |
| Today highlight           | controlAccentColor at 15% opacity | controlAccentColor at 15% opacity |
| Selected day              | controlAccentColor      | controlAccentColor      |
| Selected day text         | `#FFFFFF`               | `#FFFFFF`               |
| Day text (current month)  | labelColor              | labelColor              |
| Day text (other month)    | tertiaryLabelColor      | tertiaryLabelColor      |
| Weekday headers           | secondaryLabelColor     | secondaryLabelColor     |
| Navigation arrows         | controlAccentColor      | controlAccentColor      |

---

## NSComboBox (Editable Dropdown)

A text field with a dropdown list. The user can type a custom value or select from the list.

### Metrics

| Control Size | Height (pt) | Font Size (pt) |
|-------------|-------------|----------------|
| Mini        | 16          | 9              |
| Small       | 19          | 11             |
| Regular     | 22          | 13             |
| Large       | 28          | 15             |

Same as NSTextField metrics, plus a dropdown button on the right side (same width as NSPopUpButton arrow area).

### Colors

Same as NSTextField, with the dropdown arrow colored as secondaryLabelColor.

---

## Keyboard Interaction

### NSPopUpButton

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Space / Return  | Open menu                                  |
| Up/Down Arrow   | Navigate menu items (when open)            |
| Return          | Select highlighted item                    |
| Escape          | Close menu without selection               |
| Type character  | Jump to matching item (type-ahead)         |

### NSDatePicker

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Tab             | Move to next date component                |
| Shift+Tab       | Move to previous date component            |
| Up Arrow        | Increment current component                |
| Down Arrow      | Decrement current component                |
| Left Arrow      | Move to previous component                 |
| Right Arrow     | Move to next component                     |

## Dija Skin Mapping

```
comp! Picker {
    attr size, Size, default: Size::MD
    attr disabled, bool, default: false

    // macOS skin maps:
    // Standard dropdown: white gradient bg, chevron arrow
    // Menu: vibrancy material background, accent selection
    // Height: 22 pt (regular), per control size table
    // Corner radius: 6 pt (regular)
}

comp! DatePicker {
    attr mode, DatePickerMode, default: DatePickerMode::Date
    attr size, Size, default: Size::MD

    // macOS skin maps:
    // DatePickerMode::Date     -> yearMonthDay elements
    // DatePickerMode::Time     -> hourMinuteSecond elements
    // DatePickerMode::DateTime -> both
    // DatePickerMode::Calendar -> clockAndCalendar style
}
```
