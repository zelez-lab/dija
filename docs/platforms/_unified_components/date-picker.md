# Date Picker

A control for selecting a calendar date, displayed as a calendar grid, spinning wheels, or a compact tappable label that expands into a calendar.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIDatePicker (date modes) | Documented |
| macOS | NSDatePicker | Documented |
| Android | M3 DatePicker (modal / docked) | Documented |
| Windows | CalendarDatePicker / DatePicker (looping selector) | Documented |
| Linux | GtkCalendar | Documented |

---

## iOS

Source: UIDatePicker (date and dateAndTime modes), SwiftUI DatePicker

### Styles (iOS 14+)

| Style | Appearance | Size | Usage |
|-------|-----------|------|-------|
| Wheels | Classic spinning wheel | 216pt tall | Legacy, embedded |
| Compact | Tappable label, expands to inline | ~34pt collapsed | Space-efficient, default |
| Inline | Calendar grid + time wheels | ~350pt tall | Embedded in scrollable content |
| Automatic | System chooses (compact on iPhone) | Varies | Default |

### Compact Style

| Property | Value |
|----------|-------|
| Height (collapsed) | 34pt |
| Background (collapsed) | tertiarySystemFill |
| Corner radius (collapsed) | 6pt |
| Font (collapsed) | SF Pro Regular, 17pt |
| Text color (collapsed) | tintColor |
| Expanded popover | Inline calendar in a popover |
| Popover corner radius | 14pt |

### Inline Style (Calendar)

| Property | Value |
|----------|-------|
| Calendar grid cell size | ~44 x 44pt |
| Day number font | SF Pro Regular, 20pt |
| Selected day | tintColor circle, white text |
| Today (unselected) | tintColor text, no fill |
| Month/year header | SF Pro Semibold, 17pt |
| Weekday labels | SF Pro Regular, 13pt, tertiaryLabel color |
| Navigation arrows | Chevron left/right, tintColor |
| Total width | ~320pt |
| Total height | ~350pt (date + time) |

### Wheels Style

Same as UIPickerView metrics (see Select), with date-specific components:

| Component | Typical Width |
|-----------|--------------|
| Month | ~130pt |
| Day | ~50pt |
| Year | ~80pt |

### Date Picker Modes

| Mode | Components Shown |
|------|-----------------|
| Date | Month, Day, Year |
| Date and Time | Date (compact) + Hour, Minute, AM/PM |

### Accessibility

| Property | Value |
|----------|-------|
| Date picker | "Date picker, [current date]" |

---

## macOS

Reference: NSDatePicker, Apple HIG (macOS 14+).

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

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Tab             | Move to next date component                |
| Shift+Tab       | Move to previous date component            |
| Up Arrow        | Increment current component                |
| Down Arrow      | Decrement current component                |
| Left Arrow      | Move to previous component                 |
| Right Arrow     | Move to next component                     |

### Dija Skin Mapping

```
comp! DatePicker {
    attr mode, DatePickerMode, default: DatePickerMode::Date
    attr size, Size, default: Size::MD

    // macOS skin maps:
    // DatePickerMode::Date     -> yearMonthDay elements
    // DatePickerMode::Calendar -> clockAndCalendar style
}
```

---

## Android

Source: Material Design 3 (m3.material.io), material-components-android

### DatePicker (M3)

#### Styles

| Style | Description | Size |
|-------|-------------|------|
| Modal | Full-screen dialog with calendar grid | 360 x 568dp |
| Docked (input) | Inline text field with date format | 56dp height |
| Range | Two-date range selection in modal | 360 x 568dp |

#### Modal Calendar Metrics

| Property | Value |
|----------|-------|
| Container width | 360dp |
| Container height | 568dp |
| Container corner radius | 28dp (extra-large) |
| Header height | 120dp |
| Header horizontal padding | 24dp |
| Title font | Label Large (Roboto Medium, 14sp) |
| Selected date font | Headline Large (Roboto Regular, 32sp) |
| Day cell size | 40dp |
| Day cell touch target | 48dp |
| Day font | Body Large (Roboto Regular, 16sp) |
| Selected day fill | primary color, circle |
| Today indicator | primary color ring, no fill |
| Month/year header font | Title Small (Roboto Medium, 14sp) |
| Navigation icon size | 24dp |
| Day grid horizontal padding | 12dp |

#### Colors (Modal Calendar)

| Element | Light | Dark |
|---------|-------|------|
| Container bg | surfaceContainerHigh | surfaceContainerHigh |
| Header bg | surfaceContainerHigh | surfaceContainerHigh |
| Title text | onSurfaceVariant | onSurfaceVariant |
| Selected date text | onSurfaceVariant | onSurfaceVariant |
| Day text | onSurface | onSurface |
| Selected day bg | primary | primary |
| Selected day text | onPrimary | onPrimary |
| Today ring | primary | primary |
| Today text | primary | primary |
| Disabled day text | onSurface @ 38% | onSurface @ 38% |

### Accessibility

| Property | Value |
|----------|-------|
| DatePicker | "Date picker, [current date]" |

---

## Windows

Source: WinUI 3 / Windows App SDK, Fluent Design System

### CalendarDatePicker

A text field that opens a flyout containing a CalendarView for date selection.

#### Metrics

| Property | Value |
|----------|-------|
| Control height | 32px |
| Min width | 296px |
| Corner radius | 4px |
| Font | Segoe UI Variable, 14px |
| Calendar flyout width | ~296px |
| Calendar flyout corner radius | 8px |
| Day cell size | 40 x 40px |
| Navigation arrows | 32px touch target |

#### Key Properties

| Property | Description |
|----------|-------------|
| Date | Currently selected DateTimeOffset (nullable) |
| MinDate | Earliest selectable date |
| MaxDate | Latest selectable date |
| PlaceholderText | Text when no date is selected |
| IsTodayHighlighted | Whether today's date is marked |
| FirstDayOfWeek | Start day of the calendar week |
| DateFormat | Display format string for the selected date |
| DateChanged | Event fired when Date value changes |

### DatePicker (Looping Selector)

Spinning-wheel style selector for date components.

#### Metrics

| Property | Value |
|----------|-------|
| Control height | 32px (collapsed flyout trigger) |
| Flyout column width | ~80px per column |
| Flyout row height | 40px |
| Flyout corner radius | 8px |
| Font | Segoe UI Variable, 14px (trigger), 16px (flyout items) |
| Visible items | ~5 per column |
| Columns | Day, Month, Year (order per locale) |

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Enter / Space | Open calendar flyout |
| Arrow keys | Navigate calendar days |
| Page Up/Down | Previous/next month |
| Enter | Select highlighted date |
| Escape | Close calendar flyout |

### Accessibility

| Property | Value |
|----------|-------|
| CalendarDatePicker | "Calendar date picker, [date or placeholder]" |

---

## Linux

Source: GTK 4 (docs.gtk.org/gtk4), libadwaita

### GtkCalendar

A calendar widget displaying one month at a time with day selection.

#### Anatomy

```
+-------------------------------------------+
|  [<]   Month Year              [>]        |
+-------------------------------------------+
|  Mo  Tu  We  Th  Fr  Sa  Su              |
+-------------------------------------------+
|       1   2   3   4   5   6              |
|   7   8   9  10  11  12  13              |
|  14  15 [16] 17  18  19  20              |
|  21  22  23  24  25  26  27              |
|  28  29  30  31                          |
+-------------------------------------------+
```

#### Properties

| Property | Type | Description |
|----------|------|-------------|
| year | int | Displayed year |
| month | int | Displayed month (0-11) |
| day | int | Selected day of month |
| show-heading | gboolean | Whether the month/year heading is shown |
| show-day-names | gboolean | Whether weekday name headers are shown |
| show-week-numbers | gboolean | Whether week numbers are shown at left |

#### Metrics (Adwaita)

| Property | Value |
|----------|-------|
| Min width | ~280px |
| Day cell size | 36 x 36px |
| Day cell touch target | 40 x 40px |
| Day font | System default, ~11pt |
| Header font | System default, ~11pt, bold |
| Weekday labels font | System default, ~9pt, dim |
| Navigation button size | 32px |
| Header height | ~40px |
| Cell corner radius | Full circle (selected/today) |
| Vertical spacing (rows) | 2px |
| Horizontal padding | 6px |

#### CSS Structure

```
calendar
+-- header
|   +-- button (prev month)
|   +-- label (month + year)
|   +-- button (next month)
+-- grid
    +-- label.day-name  (x7)
    +-- label.day-number
    +-- label.day-number.other-month
    +-- label.day-number.today
    +-- label.day-number:selected
```

#### Colors (Adwaita)

| Element | Light | Dark |
|---------|-------|------|
| Background | `#FFFFFF` | `#383838` |
| Header text | `#1E1E1E` | `#FFFFFF` |
| Day text | `#1E1E1E` | `#FFFFFF` |
| Other month text | `rgba(0,0,0,0.35)` | `rgba(255,255,255,0.35)` |
| Today bg | `#3584E4` @ 15% | `#3584E4` @ 15% |
| Today text | `#3584E4` | `#78AEED` |
| Selected bg | `#3584E4` | `#3584E4` |
| Selected text | `#FFFFFF` | `#FFFFFF` |
| Weekday headers | `rgba(0,0,0,0.55)` | `rgba(255,255,255,0.55)` |
| Navigation arrows | `#1E1E1E` | `#FFFFFF` |

#### Signals

| Signal | Description |
|--------|-------------|
| day-selected | Emitted when the user selects a day |
| next-month | Emitted when the user navigates to the next month |
| prev-month | Emitted when the user navigates to the previous month |
| next-year | Emitted when the user navigates to the next year |
| prev-year | Emitted when the user navigates to the previous year |

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Arrow keys | Navigate between days |
| Space / Enter | Select highlighted day |
| Page Up | Previous month |
| Page Down | Next month |
| Shift + Page Up | Previous year |
| Shift + Page Down | Next year |
| Home | First day of month |
| End | Last day of month |

### Accessibility

| Property | Value |
|----------|-------|
| GtkCalendar role | GTK_ACCESSIBLE_ROLE_WIDGET |
| Calendar day | Individual cells announced with date |
