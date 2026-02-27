# Select

A dropdown control that lets users choose a value from a predefined list. Displays the selected item in a collapsed state and expands to show the full list of options.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIPickerView / SwiftUI Picker | Documented |
| macOS | NSPopUpButton / NSComboBox | Documented |
| Android | ExposedDropdownMenu (M3) | Documented |
| Windows | ComboBox (WinUI 3) | Documented |
| Linux | GtkDropDown | Documented |

---

## iOS

Source: UIPickerView, SwiftUI Picker

### UIPickerView (Wheel Picker)

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | transparent (inherits from parent) | transparent |
| Selection indicator | Rounded rect, systemFill background | systemFill background |
| Selection indicator height | 32pt | 32pt |
| Selection indicator corner radius | 8pt | 8pt |
| Total height | 216pt (default) | 216pt |
| Width | Fills container | |

#### Row Metrics

| Property | Value |
|----------|-------|
| Row height (default) | 32pt |
| Row height (custom range) | 20pt-100pt |
| Font | SF Pro Regular, 23pt (center), smaller at edges |
| Text color | label |
| Text alignment | Center (per component) |
| Component spacing | 5pt between components |

#### Scrolling Physics

| Property | Value |
|----------|-------|
| Deceleration | Fast (~0.99 deceleration rate) |
| Snap to row | Spring animation, ~0.3s |
| Haptic | Light selection feedback on each row crossing |
| Visible rows | ~5 above and below selection |
| Edge fade | Text fades and scales down away from center |
| Perspective | Slight 3D wheel effect (barrel distortion) |

#### Animation

| Property | Value |
|----------|-------|
| Scroll to row | 0.3s ease-in-out (animated) |
| Momentum | Deceleration with snap at end |
| Spring snap | ~0.2s, damping 0.8 |

### SwiftUI Picker

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

#### Menu Picker

| Property | Value |
|----------|-------|
| Trigger | Label text, tintColor, with chevron indicator |
| Menu style | Standard context menu appearance |
| Selected item | Checkmark to the left |
| Item font | SF Pro Regular, 17pt |
| Corner radius | 14pt (menu container) |
| Shadow | offset(0, 10) blur 30, black @ 0.2 |

### Accessibility

| Property | Value |
|----------|-------|
| Picker role | Picker (adjustable) |
| Wheel | "Picker item, [value], adjustable" |
| Increment/decrement | Swipe up/down to change value |

---

## macOS

Reference: NSPopUpButton, NSComboBox, Apple HIG (macOS 14+).

### NSPopUpButton (Dropdown Picker)

#### Types

| Type              | Description                                      |
|-------------------|--------------------------------------------------|
| Pop-up (default)  | Displays selected item, dropdown shows all options |
| Pull-down         | Displays title, dropdown shows action list        |

#### Metrics

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

#### Colors

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

#### Menu Appearance

The dropdown menu uses the `.menu` vibrancy material:

| Element              | Light Mode                    | Dark Mode                      |
|----------------------|-------------------------------|--------------------------------|
| Menu background       | Menu material vibrancy        | Menu material vibrancy         |
| Fallback background   | `#FFFFFF`                     | `#353535`                      |
| Menu shadow           | rgba(0,0,0,0.20) offset (0,4) blur 20 | rgba(0,0,0,0.40) offset (0,4) blur 20 |
| Selected item bg      | controlAccentColor            | controlAccentColor             |
| Selected item text    | `#FFFFFF`                     | `#FFFFFF`                      |
| Separator             | separatorColor                | separatorColor                 |

#### Arrow Indicator

The popup button shows a chevron (up/down arrows):

| Property              | Value            |
|-----------------------|------------------|
| Symbol                | Up/down chevron  |
| Size                  | ~7 pt (regular)  |
| Color                 | secondaryLabelColor |
| Position              | Right edge, vertically centered |

#### Animation

| Transition              | Duration (ms) | Curve          |
|------------------------|---------------|----------------|
| Menu appear             | 150           | Ease Out       |
| Menu dismiss            | 100           | Ease In        |
| Item highlight          | 0             | Immediate      |
| Press feedback          | 30            | Ease Out       |

### NSComboBox (Editable Dropdown)

A text field with a dropdown list. The user can type a custom value or select from the list.

#### Metrics

| Control Size | Height (pt) | Font Size (pt) |
|-------------|-------------|----------------|
| Mini        | 16          | 9              |
| Small       | 19          | 11             |
| Regular     | 22          | 13             |
| Large       | 28          | 15             |

Same as NSTextField metrics, plus a dropdown button on the right side (same width as NSPopUpButton arrow area).

#### Colors

Same as NSTextField, with the dropdown arrow colored as secondaryLabelColor.

### Keyboard Interaction

#### NSPopUpButton

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Space / Return  | Open menu                                  |
| Up/Down Arrow   | Navigate menu items (when open)            |
| Return          | Select highlighted item                    |
| Escape          | Close menu without selection               |
| Type character  | Jump to matching item (type-ahead)         |

### Dija Skin Mapping

```
comp! Select {
    attr size, Size, default: Size::MD
    attr disabled, bool, default: false

    // macOS skin maps:
    // Standard dropdown: white gradient bg, chevron arrow
    // Menu: vibrancy material background, accent selection
    // Height: 22 pt (regular), per control size table
    // Corner radius: 6 pt (regular)
}
```

---

## Android

Source: Material Design 3 (m3.material.io), material-components-android

### Overview

Android's primary picker control is the **ExposedDropdownMenu**, built on `TextInputLayout` + `AutoCompleteTextView`. It renders as an M3 text field with a trailing arrow that opens a dropdown menu.

### ExposedDropdownMenu

#### Anatomy

```
+-------------------------------------------------------+
| [Label]                                                |
| +---------------------------------------------------+ |
| | Selected text                          [Arrow v]  | |
| +---------------------------------------------------+ |
|                                                       |
| +---------------------------------------------------+ |
| |  Menu item 1                                      | |
| |  Menu item 2                            [Check]   | |
| |  Menu item 3                                      | |
| +---------------------------------------------------+ |
+-------------------------------------------------------+
```

Components:
1. **Text field anchor** -- filled or outlined M3 text field
2. **Label** -- floating label above the field
3. **Selected value text** -- displays current selection
4. **Trailing icon** -- dropdown arrow (chevron), rotates on open
5. **Menu container** -- elevated surface with list items
6. **Menu items** -- one-line or two-line items with optional leading/trailing elements

#### Variants

| Variant | Anchor Style | Description |
|---------|-------------|-------------|
| Filled | FilledBox.ExposedDropdownMenu | Filled text field with bottom-line indicator |
| Outlined | OutlinedBox.ExposedDropdownMenu | Outlined text field with border stroke |

#### Anchor Type (Compose)

| Type | Behavior |
|------|----------|
| PrimaryNotEditable | Read-only field, tapping anywhere opens menu |
| PrimaryEditable | Editable field, typing filters options |
| SecondaryEditable | Trailing icon only opens menu (better a11y for editable) |

#### Metrics (Text Field Anchor)

| Property | Filled | Outlined |
|----------|--------|----------|
| Height | 56dp | 56dp |
| Horizontal padding (text) | 16dp | 16dp |
| Top padding (with label) | 8dp | 16dp |
| Bottom padding | 16dp | 16dp |
| Corner radius (top) | 4dp | 4dp (all corners) |
| Corner radius (bottom) | 0dp | 4dp (all corners) |
| Label font | Body Small (Roboto Regular, 12sp) | Body Small (Roboto Regular, 12sp) |
| Value font | Body Large (Roboto Regular, 16sp) | Body Large (Roboto Regular, 16sp) |
| Trailing icon size | 24dp | 24dp |
| Trailing icon padding (end) | 12dp | 12dp |
| Active indicator (filled) | 2dp bottom line | 2dp border stroke |

#### Menu Metrics

| Property | Value |
|----------|-------|
| Container corner radius | 4dp (extra-small) |
| Container elevation | Level 2 (3dp shadow) |
| Container max width | Same as anchor width (exposed) |
| Item height (one-line) | 48dp |
| Item height (two-line) | 64dp |
| Item horizontal padding | 12dp |
| Item label font | Label Large (Roboto Medium 500, 14sp) |
| Item supporting text font | Body Medium (Roboto Regular, 14sp) |
| Leading element size | 24dp |
| Leading element padding (start) | 12dp |
| Trailing element size | 24dp |
| Trailing element padding (end) | 12dp |
| Vertical padding (top/bottom of list) | 8dp |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Anchor background (filled) | surfaceContainerHighest | surfaceContainerHighest |
| Anchor background (outlined) | transparent | transparent |
| Anchor border (outlined, rest) | `#79747E` (outline) | `#938F99` |
| Anchor border (outlined, focused) | `#6750A4` (primary) | `#D0BCFF` |
| Active indicator (filled, rest) | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Active indicator (filled, focused) | `#6750A4` (primary) | `#D0BCFF` |
| Label (rest) | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Label (focused) | `#6750A4` (primary) | `#D0BCFF` |
| Value text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Trailing icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Menu container | surfaceContainer | surfaceContainer |
| Menu item text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Menu selected item check | `#6750A4` (primary) | `#D0BCFF` |
| Disabled anchor bg (filled) | onSurface @ 4% | onSurface @ 4% |
| Disabled value text | onSurface @ 38% | onSurface @ 38% |
| Disabled trailing icon | onSurface @ 38% | onSurface @ 38% |

#### States

| State | Effect |
|-------|--------|
| Enabled | Default appearance |
| Focused | Label + indicator color change to primary, 2dp indicator |
| Hovered | State layer 8% onSurface over anchor |
| Pressed | State layer 10% onSurface, menu opens |
| Error | Label + indicator + trailing icon color change to error |
| Disabled | Anchor bg onSurface @ 4%, content onSurface @ 38% |
| Expanded | Menu visible, trailing icon rotated 180deg |

#### Animation

| Transition | Duration | Curve |
|------------|----------|-------|
| Menu open | 120ms | Standard decelerate |
| Menu close | 100ms | Standard accelerate |
| Arrow rotation | 150ms | Standard easing |
| Item ripple | 300ms | Standard easing |
| Label float | 150ms | Standard easing |

### Accessibility (Android)

| Property | Value |
|----------|-------|
| Dropdown role | ComboBox (TYPE_COMBO_BOX) |
| Dropdown action | ACTION_CLICK to open, ACTION_DISMISS to close |
| Menu items | Each item announced with position in set |

---

## Windows

Source: WinUI 3 / Windows App SDK (Microsoft.UI.Xaml.Controls), Fluent Design System

### Overview

Windows uses **ComboBox** as the standard dropdown picker control. It displays a collapsed single-line selector that expands into a scrollable list.

### ComboBox

#### Anatomy

```
Collapsed:
+---------------------------------------------------+
| Placeholder or selected text            [Chevron] |
+---------------------------------------------------+

Expanded:
+---------------------------------------------------+
| Selected text                           [Chevron] |
+---------------------------------------------------+
| +-----------------------------------------------+ |
| |  Item 1                                       | |
| |  Item 2  (highlighted)                        | |
| |  Item 3                                       | |
| |  ...                                          | |
| +-----------------------------------------------+ |
```

Components:
1. **Header** -- optional label above the control
2. **Collapsed box** -- displays selected item or placeholder text
3. **Chevron** -- downward-pointing arrow indicator
4. **Dropdown popup** -- scrollable list of items
5. **Items** -- selectable options, wrapped in ComboBoxItem containers

#### Variants

| Variant | Description |
|---------|-------------|
| Standard | Non-editable, select from list only |
| Editable | Text input + dropdown, user can type or select (`IsEditable=true`) |

#### Metrics

| Property | Value |
|----------|-------|
| Height (collapsed) | 32px |
| Min width | 64px |
| Horizontal padding (text) | 12px |
| Vertical padding | 5px |
| Corner radius (control) | 4px (ControlCornerRadius) |
| Corner radius (dropdown) | 8px (OverlayCornerRadius) |
| Border thickness | 1px |
| Bottom border thickness (rest) | 1px (accent underline) |
| Chevron size | 12px |
| Chevron right padding | 12px |
| Font | Segoe UI Variable, 14px (body) |
| Header font | Segoe UI Variable, 14px (body, semibold) |
| Header margin (bottom) | 8px |

#### Dropdown Metrics

| Property | Value |
|----------|-------|
| Item height | 32px |
| Item horizontal padding | 12px |
| Item corner radius | 4px |
| Max visible items (default) | 15 (ComboBoxPopupMaxNumberOfItems) |
| Dropdown border thickness | 1px |
| Dropdown vertical padding | 4px |
| Dropdown shadow | ThemeShadow, depth 32 |
| Dropdown max height | Adjustable (MaxDropDownHeight property) |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Background (rest) | ControlFillColorDefault | ControlFillColorDefault |
| Background (hover) | ControlFillColorSecondary | ControlFillColorSecondary |
| Background (pressed) | ControlFillColorTertiary | ControlFillColorTertiary |
| Background (disabled) | ControlFillColorDisabled | ControlFillColorDisabled |
| Border (rest) | ControlStrokeColorDefault + ControlStrokeColorSecondary | ControlStrokeColorDefault + ControlStrokeColorSecondary |
| Border (hover) | ControlStrokeColorDefault + ControlStrokeColorSecondary | ControlStrokeColorDefault + ControlStrokeColorSecondary |
| Border (focused) | ControlStrokeColorDefault | ControlStrokeColorDefault |
| Bottom accent (rest) | ControlStrongStrokeColorDefault | ControlStrongStrokeColorDefault |
| Bottom accent (focused) | AccentFillColorDefault (2px) | AccentFillColorDefault (2px) |
| Text (rest) | TextFillColorPrimary | TextFillColorPrimary |
| Text (disabled) | TextFillColorDisabled | TextFillColorDisabled |
| Placeholder text | TextFillColorSecondary | TextFillColorSecondary |
| Chevron | TextFillColorSecondary | TextFillColorSecondary |
| Dropdown background | AcrylicBackgroundFillColorDefaultLayerBelowMica | AcrylicBackgroundFillColorDefaultLayerBelowMica |
| Dropdown border | SurfaceStrokeColorFlyout | SurfaceStrokeColorFlyout |
| Item hover bg | SubtleFillColorSecondary | SubtleFillColorSecondary |
| Item selected bg | SubtleFillColorSecondary | SubtleFillColorSecondary |
| Item selected indicator | AccentFillColorDefault, 3px left bar | AccentFillColorDefault, 3px left bar |

#### States

| State | Effect |
|-------|--------|
| Rest | Default appearance, 1px bottom accent |
| Hover | Background shifts to secondary fill, subtle brightness |
| Pressed | Background shifts to tertiary fill |
| Focused | 2px bottom accent in AccentColor, inner focus rect |
| Disabled | All content reduced opacity (TextFillColorDisabled) |
| Open | Dropdown visible, chevron rotated 180deg |
| Error | Red border + error message below (via validation) |

#### Animation

| Transition | Duration | Curve |
|------------|----------|-------|
| Dropdown open | 250ms | Decelerate (cubic-bezier 0,0,0,1) |
| Dropdown close | 150ms | Accelerate (cubic-bezier 1,0,1,1) |
| Item highlight | 83ms | Linear |
| Focus indicator | 167ms | Decelerate |
| Chevron rotation | 167ms | Decelerate |

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Space / Enter | Open dropdown |
| Up/Down Arrow | Navigate items (when open) or cycle selection (when closed) |
| Enter | Select highlighted item |
| Escape | Close dropdown without selection |
| Home / End | Jump to first/last item |
| Type character | Type-ahead: jump to matching item |
| Alt + Down | Open dropdown |
| Alt + Up | Close dropdown |

### Accessibility

| Property | Value |
|----------|-------|
| ComboBox role | ComboBox (UIA_ComboBoxControlTypeId) |
| Pattern | ExpandCollapse + Selection |
| Collapsed state | "ComboBox, [selected value], collapsed" |
| Expanded state | "ComboBox, [selected value], expanded" |
| Items | ListItem, position in set announced |
| Editable | Text pattern also supported |

---

## Linux

Source: GTK 4 (docs.gtk.org/gtk4), libadwaita

### Overview

GTK 4 uses **GtkDropDown** as the standard dropdown selection widget, replacing the deprecated GtkComboBox from GTK 3. Options are provided via a **GListModel** and rendered using **GtkListItemFactory** instances.

### GtkDropDown

#### Anatomy

```
Collapsed:
+---------------------------------------------------+
| Selected item text                        [Arrow] |
+---------------------------------------------------+

Expanded (popover):
+---------------------------------------------------+
| Selected item text                        [Arrow] |
+---------------------------------------------------+
| +-----------------------------------------------+ |
| | [Search entry]                    (optional)  | |
| +-----------------------------------------------+ |
| |  Item 1                                       | |
| |  Item 2                              [Check]  | |
| |  Item 3                                       | |
| |  ...                                          | |
| +-----------------------------------------------+ |
```

Components:
1. **Button** -- the collapsed trigger displaying the selected item
2. **Arrow indicator** -- optional downward arrow (controllable via `show-arrow`)
3. **Popover** -- the dropdown container anchored to the button
4. **Search entry** -- optional filter field (enabled via `enable-search`)
5. **List items** -- rendered by a GtkListItemFactory; default shows text + checkmark for selected
6. **Header** -- optional header widget in popup (via `header-factory`, since GTK 4.12)

#### Properties

| Property | Type | Description | Since |
|----------|------|-------------|-------|
| model | GListModel | Data model for the list items | 4.0 |
| factory | GtkListItemFactory | Factory for rendering items in the button | 4.0 |
| list-factory | GtkListItemFactory | Factory for rendering items in the popup (defaults to `factory`) | 4.0 |
| header-factory | GtkListItemFactory | Factory for section header widgets in the popup | 4.12 |
| selected | guint | Index of the selected item (GTK_INVALID_LIST_POSITION if none) | 4.0 |
| selected-item | GObject | The selected item object | 4.0 |
| expression | GtkExpression | Expression to obtain display strings from items | 4.0 |
| enable-search | gboolean | Whether to show a search entry in the popup | 4.0 |
| show-arrow | gboolean | Whether to show the dropdown arrow indicator | 4.6 |
| search-match-mode | GtkStringFilterMatchMode | How search text is matched (EXACT, PREFIX, SUBSTRING) | 4.12 |

#### Metrics (Adwaita Theme)

| Property | Value |
|----------|-------|
| Button height (min) | 34px |
| Horizontal padding | 12px |
| Vertical padding | 8px |
| Corner radius | 6px |
| Border width | 1px |
| Font | System default (typically Cantarell 11pt or Inter 11pt) |
| Arrow size | ~16px (symbolic icon) |
| Arrow padding (end) | 6px |
| Popover corner radius | 12px |
| Popover padding | 6px |
| Item height | 34px |
| Item horizontal padding | 12px |
| Item corner radius | 6px |
| Check icon size | 16px |
| Search entry height | 34px |
| Search entry margin | 6px |

#### CSS Structure

```
dropdown
+-- button.toggle
|   +-- box
|       +-- [icon or custom content]
|       +-- [arrow]
+-- popover
    +-- [search-entry]  (if enable-search)
    +-- scrolledwindow
        +-- listview
            +-- row
            +-- row
            +-- ...
```

CSS node name: `dropdown`. The button child has the `.toggle` class. The popover follows standard GtkPopover styling.

#### Colors (Adwaita)

| Element | Light | Dark |
|---------|-------|------|
| Button background | `#FAFAFA` (headerbar_bg) | `#383838` |
| Button background (hover) | `#F0F0F0` | `#434343` |
| Button background (active) | `#D5D5D5` | `#505050` |
| Button border | `rgba(0,0,0,0.15)` | `rgba(0,0,0,0.36)` |
| Button text | `#1E1E1E` (window_fg) | `#FFFFFF` |
| Arrow | `rgba(0,0,0,0.55)` | `rgba(255,255,255,0.70)` |
| Popover background | `#FFFFFF` | `#383838` |
| Popover border | `rgba(0,0,0,0.15)` | `rgba(0,0,0,0.36)` |
| Popover shadow | `rgba(0,0,0,0.08)` 0 2px 6px | `rgba(0,0,0,0.20)` 0 2px 6px |
| Item hover bg | `rgba(0,0,0,0.06)` | `rgba(255,255,255,0.08)` |
| Item selected bg | `#3584E4` (accent_bg_color) | `#3584E4` |
| Item selected text | `#FFFFFF` | `#FFFFFF` |
| Check icon (selected) | `#3584E4` (accent_color) | `#78AEED` |
| Disabled text | `rgba(0,0,0,0.50)` | `rgba(255,255,255,0.50)` |

#### States

| State | Effect |
|-------|--------|
| Normal | Default button appearance |
| Hover | Lighter/darker background shift |
| Active (pressed) | Depressed button appearance |
| Focused | Focus ring (2px outline, accent color, 2px offset) |
| Disabled | Content at 50% opacity, no interaction |
| Checked (dropdown open) | Button in active/depressed state |

#### Animation

| Transition | Duration | Curve |
|------------|----------|-------|
| Popover open | 200ms | Ease out (cubic) |
| Popover close | 150ms | Ease in |
| Hover background | 200ms | Ease out |
| Focus ring | 75ms | Ease in-out |
| Item highlight | 50ms | Linear |

### Keyboard Interaction

| Key | Action |
|-----|--------|
| Space / Enter | Open popover |
| Up/Down Arrow | Navigate items (when open) |
| Enter | Select highlighted item |
| Escape | Close popover without selection |
| Type character | Filter items (when search enabled) |
| Tab | Move focus away, closing popover |

### Accessibility

| Property | Value |
|----------|-------|
| GtkDropDown role | GTK_ACCESSIBLE_ROLE_COMBO_BOX |
| State | aria-expanded (open/closed) |
| Selected | aria-activedescendant points to selected item |
| Items | listbox > option roles |
