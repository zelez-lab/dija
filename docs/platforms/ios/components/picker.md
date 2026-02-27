# iOS — Picker (UIPickerView / UIDatePicker)

Source: UIPickerView, UIDatePicker, SwiftUI Picker, SwiftUI DatePicker

## UIPickerView (Wheel Picker)

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | transparent (inherits from parent) | transparent |
| Selection indicator | Rounded rect, systemFill background | systemFill background |
| Selection indicator height | 32pt | 32pt |
| Selection indicator corner radius | 8pt | 8pt |
| Total height | 216pt (default) | 216pt |
| Width | Fills container | |

### Row Metrics

| Property | Value |
|----------|-------|
| Row height (default) | 32pt |
| Row height (custom range) | 20pt–100pt |
| Font | SF Pro Regular, 23pt (center), smaller at edges |
| Text color | label |
| Text alignment | Center (per component) |
| Component spacing | 5pt between components |

### Scrolling Physics

| Property | Value |
|----------|-------|
| Deceleration | Fast (~0.99 deceleration rate) |
| Snap to row | Spring animation, ~0.3s |
| Haptic | Light selection feedback on each row crossing |
| Visible rows | ~5 above and below selection |
| Edge fade | Text fades and scales down away from center |
| Perspective | Slight 3D wheel effect (barrel distortion) |

### Animation

| Property | Value |
|----------|-------|
| Scroll to row | 0.3s ease-in-out (animated) |
| Momentum | Deceleration with snap at end |
| Spring snap | ~0.2s, damping 0.8 |

## UIDatePicker

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

### Time Component (Inline)

| Property | Value |
|----------|-------|
| Layout | Two wheel columns (hours, minutes) |
| Wheel height | ~130pt |
| Row height | 32pt |
| AM/PM | Third column if 12-hour format |
| Font | SF Pro Regular, 23pt |
| Separator | Colon (:) between hours and minutes |

### Wheels Style

Same as UIPickerView metrics above, with date-specific components:

| Component | Typical Width |
|-----------|--------------|
| Month | ~130pt |
| Day | ~50pt |
| Year | ~80pt |
| Hour | ~50pt |
| Minute | ~50pt |
| AM/PM | ~65pt |

### Date Picker Modes

| Mode | Components Shown |
|------|-----------------|
| Date | Month, Day, Year |
| Time | Hour, Minute, AM/PM |
| Date and Time | Date (compact) + Hour, Minute, AM/PM |
| Countdown Timer | Hours, Minutes |

## SwiftUI Picker

SwiftUI Picker can render in several styles:

| Style | Appearance |
|-------|-----------|
| `.automatic` | Context-dependent (wheel in forms, menu elsewhere) |
| `.wheel` | Standard wheel picker |
| `.segmented` | UISegmentedControl (for small option sets) |
| `.menu` | Drop-down menu (default outside forms) |
| `.inline` | Inline list of options |
| `.navigationLink` | Pushes to a selection list |
| `.palette` | Color palette style (watchOS) |

### Menu Picker

| Property | Value |
|----------|-------|
| Trigger | Label text, tintColor, with chevron indicator |
| Menu style | Standard context menu appearance |
| Selected item | Checkmark to the left |
| Item font | SF Pro Regular, 17pt |
| Corner radius | 14pt (menu container) |
| Shadow | offset(0, 10) blur 30, black @ 0.2 |

## Accessibility

| Property | Value |
|----------|-------|
| Picker role | Picker (adjustable) |
| Wheel | "Picker item, [value], adjustable" |
| Date picker | "Date picker, [current date/time]" |
| Increment/decrement | Swipe up/down to change value |
