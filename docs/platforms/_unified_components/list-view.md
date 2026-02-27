# List View

A vertically scrollable list of rows, optionally organized into sections with headers, supporting selection, reordering, and swipe actions.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UITableView / UITableViewCell / SwiftUI List | Documented |
| macOS | NSTableView (single-column / source list) | Documented |
| Android | Material Design 3 Lists | Documented |
| Windows | WinUI 3 ListView / GridView | Documented |
| Linux | GtkListBox / GtkListView (GNOME/Adwaita) | Documented |

---

## iOS

Source: UITableView, UITableViewCell, SwiftUI List

### Table Styles

| Style | Background | Cell Shape | Usage |
|-------|-----------|------------|-------|
| Plain | systemBackground | Full-width cells | Contacts, music lists |
| Grouped | systemGroupedBackground | Rounded sections | Settings, forms |
| Inset Grouped | systemGroupedBackground | Rounded + inset sections | Modern settings (iOS 13+) |

### Section Background

| Style | Light | Dark |
|-------|-------|------|
| Plain | systemBackground (`#FFFFFF`) | `#000000` |
| Grouped | systemGroupedBackground (`#F2F2F7`) | `#000000` |
| Inset Grouped | systemGroupedBackground (`#F2F2F7`) | `#000000` |

### Cell

| Property | Light | Dark |
|----------|-------|------|
| Background (grouped) | secondarySystemGroupedBackground (`#FFFFFF`) | `#1C1C1E` |
| Background (plain) | systemBackground (`#FFFFFF`) | `#000000` |
| Corner radius (inset grouped) | 13pt (first/last cells rounded, middle cells square) | |
| Corner curve | `.continuous` (superellipse) | |
| Selection highlight | systemGray4 (`#D1D1D6`) fill | systemGray4 (`#3A3A3C`) fill |

### Cell Heights

| Cell Style | Default Height | Notes |
|-----------|---------------|-------|
| Default | 44pt | Single line, icon + text |
| Subtitle | 58pt (approx) | Title + subtitle |
| Value 1 (right detail) | 44pt | Title left, detail right |
| Value 2 (left detail) | 44pt | Blue label left, title right |
| Custom | Self-sizing | Auto Layout determines height |

### Cell Content Layout

| Property | Value |
|----------|-------|
| Left inset (content) | 20pt (16pt on compact width) |
| Right inset (content) | 20pt (16pt on compact width) |
| Image-to-text spacing | 15pt |
| Title font | SF Pro Regular, 17pt |
| Title color | label |
| Subtitle font | SF Pro Regular, 15pt |
| Subtitle color | secondaryLabel |
| Detail font | SF Pro Regular, 17pt |
| Detail color | secondaryLabel |

### Accessories

| Accessory | Icon | Size | Color |
|-----------|------|------|-------|
| Disclosure indicator | Chevron right (>)  | ~8 x 13pt | systemGray3 |
| Detail disclosure | Info (i) circle + chevron | ~20pt circle | tintColor |
| Checkmark | Checkmark | ~14 x 11pt | tintColor |
| Detail button | Info (i) circle | ~22pt | tintColor |
| Switch | UISwitch | 51 x 31pt | -- |

Accessory right margin: 16pt from cell trailing edge.

### Separator

| Property | Value |
|----------|-------|
| Width | 0.33pt (1px on 3x retina) |
| Color | separator (`#3C3C43` @ 0.29 / `#545458` @ 0.60) |
| Left inset (default) | 20pt (aligns with text, not icon) |
| Left inset (with image) | 59pt (after image + spacing) |
| Right inset | 0pt (extends to edge) |
| Last cell | No bottom separator |

### Section Header / Footer

| Property | Value |
|----------|-------|
| Font | SF Pro Regular, 13pt |
| Color (header) | secondaryLabel |
| Color (footer) | secondaryLabel |
| Text case (grouped) | Uppercase (header), sentence case (footer) |
| Padding (header top) | 22pt |
| Padding (header bottom) | 8pt |
| Padding (footer top) | 8pt |
| Padding (footer bottom) | 22pt |
| Left inset | 20pt |
| Section-to-section gap | ~35pt (header-to-header in grouped) |

### Swipe Actions

| Property | Value |
|----------|-------|
| Leading actions | Custom (mark read, pin, etc.) |
| Trailing actions | Delete, custom |
| Action button height | Same as cell height |
| Delete button color | systemRed (`#FF3B30` / `#FF453A`) |
| Action label font | SF Pro Regular, 15pt |
| Action label color | white |
| Full swipe threshold | ~75% of cell width |
| Full swipe | Triggers first action automatically |

#### Standard Swipe Action Colors

| Action | Color |
|--------|-------|
| Delete | systemRed |
| Archive | systemPurple or systemOrange |
| Flag | systemOrange |
| More | systemGray |
| Mute | systemIndigo |
| Pin | systemYellow |

### Selection

| Property | Value |
|----------|-------|
| Single selection highlight | systemGray4 fill |
| Multi-selection checkmark | tintColor circle with checkmark |
| Multi-selection circle (unselected) | 22pt, 2pt border, systemGray3 |
| Multi-selection circle (selected) | 22pt, filled tintColor, white checkmark |
| Selection animation | Fade highlight in ~0.1s, fade out ~0.3s |

### Pull to Refresh

| Property | Value |
|----------|-------|
| Spinner | UIActivityIndicatorView.medium |
| Spinner color | secondaryLabel |
| Pull distance to trigger | ~60pt |
| Spinner position | Centered, ~40pt above content |
| Animation | Spring back after release |

### Editing Mode

| Property | Value |
|----------|-------|
| Delete button (left) | Red circle with white minus |
| Reorder control (right) | Three horizontal lines (grip handle) |
| Delete button size | 22pt circle |
| Reorder handle color | systemGray2 |
| Cell indent (editing) | 38pt from left |
| Transition | 0.3s ease-in-out |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Cell (static content), Button (interactive) |
| Swipe actions | VoiceOver: custom actions rotor |
| VoiceOver | "[Title], [subtitle], [accessory type]" |

---

## macOS

Reference: NSTableView (single-column list mode), Apple HIG (macOS 14+).

### Overview

`NSTableView` in single-column mode or with the `.sourceList` style serves as the macOS list view. For multi-column data tables, see Data Table.

### Table Styles

| Style             | Description                                                 | Usage                      |
|-------------------|-------------------------------------------------------------|----------------------------|
| `.inset`          | Selection has rounded corners, inset from edges              | Settings, preferences      |
| `.sourceList`     | Sidebar/source list appearance with vibrancy                 | Sidebars                   |
| `.plain`          | No special styling, minimal chrome                           | Custom layouts             |

### Row Heights

| Configuration           | Row Height (pt) | Notes                              |
|------------------------|-----------------|-------------------------------------|
| Default                 | 24              | Standard single-line row            |
| Source list              | 24              | Sidebar row                         |
| Large row height        | 34              | Rows with subtitle or icon          |
| Custom                  | User-defined    | Via delegate `heightOfRow()`        |

### Inset Style Margins

| Property                    | Value (pt) |
|-----------------------------|------------|
| Row inset (left/right)       | 10         |
| Selection corner radius      | 6          |
| Content padding (horizontal) | 6          |
| Content padding (vertical)   | 2          |

### Source List Style

| Property                    | Value (pt) |
|-----------------------------|------------|
| Row inset (left/right)       | 10         |
| Selection corner radius      | 6          |
| Group row height             | 28         |
| Group row top padding        | 8          |
| Indentation per level        | 16         |
| Disclosure triangle size     | 10         |
| Icon to text gap             | 6          |

### Colors

#### Backgrounds

| Element                        | Light Mode            | Dark Mode             |
|--------------------------------|-----------------------|-----------------------|
| Table background               | `#FFFFFF`             | `#1E1E1E`             |
| Alternating row (even)         | `#FFFFFF`             | `#1E1E1E`             |
| Alternating row (odd)          | `#F4F5F5`             | `#232323`             |
| Source list background         | Vibrancy (sidebar material) | Vibrancy (sidebar material) |
| Source list fallback           | `#F6F6F6`             | `#2D2D2D`             |

#### Selection

| State                          | Light Mode            | Dark Mode             |
|--------------------------------|-----------------------|-----------------------|
| Selected row (focused)         | `#0063E1`             | `#0058D0`             |
| Selected row (unfocused)       | `#DCDCDC`             | `#464646`             |
| Selected text (focused)        | `#FFFFFF`             | `#FFFFFF`             |
| Selected text (unfocused)      | labelColor            | labelColor            |
| Source list selected (focused) | controlAccentColor with vibrancy | controlAccentColor with vibrancy |
| Source list selected (unfocused)| `rgba(0,0,0,0.06)`  | `rgba(255,255,255,0.08)` |

### States

| State           | Visual Changes                                        |
|-----------------|------------------------------------------------------|
| Normal          | Default background (or alternating color)             |
| Hover           | Subtle highlight (iOS-like, macOS 14+)                |
| Selected        | Accent color fill (focused) or gray fill (unfocused)  |
| Dragging        | Semi-transparent row snapshot                          |
| Drop target     | Blue line indicator at insertion point                 |
| Disabled row    | Dimmed text, no selection                              |

### Group Row (NSOutlineView)

| State           | Visual Changes                                        |
|-----------------|------------------------------------------------------|
| Normal          | Bold uppercase text, no background                    |
| Collapsed       | Disclosure triangle points right                      |
| Expanded        | Disclosure triangle points down                       |

### Typography

| Element                  | Font Size (pt) | Weight      |
|--------------------------|----------------|-------------|
| Cell text                | 13 (body)      | Regular     |
| Cell secondary text      | 11             | Regular     |
| Source list group header  | 11             | Bold        |
| Source list item          | 13             | Regular     |

### Disclosure Triangle (NSOutlineView)

| Property              | Value          |
|-----------------------|----------------|
| Size                  | 10x10 pt       |
| Color                 | tertiaryLabelColor |
| Collapsed direction   | Right-pointing  |
| Expanded direction    | Down-pointing   |
| Animation duration    | 150 ms          |
| Animation curve       | Ease In Out     |

### Drag and Drop

| Element                  | Description                                  |
|--------------------------|----------------------------------------------|
| Drag threshold           | 4 pt mouse movement before drag starts       |
| Drag preview             | Semi-transparent row snapshot at 70% opacity  |
| Drop indicator           | 2 pt blue line at insertion point             |
| Drop highlight (on row)  | Blue outline around target row                |
| Drop feedback (between)  | Blue line with circle at left edge            |
| Spring-loading delay     | 500 ms hover before auto-expand              |

### Scroll Behavior

| Property                | Value                                        |
|-------------------------|----------------------------------------------|
| Elastic overscroll      | Yes (rubber band)                            |
| Scroll indicators       | Overlay, auto-hide (system preference)       |
| Scroll bar width        | 6 pt collapsed, 8 pt hover                  |
| Scroll bar inset        | 2 pt from edge                               |

### Animation

| Transition                   | Duration (ms) | Curve          |
|------------------------------|---------------|----------------|
| Row insert                   | 250           | Ease In Out    |
| Row delete                   | 250           | Ease In Out    |
| Row move                     | 250           | Ease In Out    |
| Selection change             | 100           | Ease Out       |
| Disclosure expand/collapse   | 150           | Ease In Out    |
| Scroll deceleration          | varies        | Ease Out       |

### Keyboard Interaction

| Key                  | Action                                    |
|---------------------|-------------------------------------------|
| Up Arrow            | Move selection up one row                  |
| Down Arrow          | Move selection down one row                |
| Cmd+Up              | Select first row                           |
| Cmd+Down            | Select last row                            |
| Shift+Up/Down       | Extend selection                           |
| Cmd+Click           | Toggle row selection                       |
| Shift+Click         | Extend selection to clicked row            |
| Delete              | Delete selected row (if supported)         |
| Right Arrow         | Expand disclosure (NSOutlineView)          |
| Left Arrow          | Collapse disclosure (NSOutlineView)        |
| Space               | Quick Look preview (if supported)          |
| Cmd+A               | Select all rows                            |

---

## Android

Source: m3.material.io/components/lists/specs

M3 equivalent of iOS table view cells. Called "Lists" in M3 vocabulary.

### Variants

| Variant | Height | Content |
|---------|--------|---------|
| One-line | 56dp | Headline only |
| Two-line | 72dp | Headline + supporting text |
| Three-line | 88dp | Headline + 2 lines supporting text |

### Metrics

| Property | Value |
|----------|-------|
| Min height (one-line) | 56dp |
| Min height (two-line) | 72dp |
| Min height (three-line) | 88dp |
| Horizontal padding (leading edge) | 16dp |
| Horizontal padding (trailing edge) | 24dp |
| Vertical padding | 8dp (top and bottom, two/three-line) |
| Leading element gap | 16dp |
| Trailing element gap | 16dp |
| Headline-supporting gap | 0dp (adjacent lines) |
| Headline font | Body Large (Roboto Regular, 16sp) |
| Supporting text font | Body Medium (Roboto Regular, 14sp) |
| Overline font | Label Small (Roboto Medium, 11sp) |
| Trailing supporting font | Label Small (Roboto Medium, 11sp) |

### Leading Element Sizes

| Element type | Size |
|-------------|------|
| Icon | 24dp x 24dp |
| Avatar (monogram) | 40dp x 40dp |
| Avatar (image) | 40dp x 40dp |
| Thumbnail | 56dp x 56dp |
| Video thumbnail | 114dp x 64dp |
| Checkbox / Radio | 18dp x 18dp |

Avatar corner radius: 20dp (full circle).
Thumbnail corner radius: 0dp (square).

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#FEF7FF` (surface) | `#141218` |
| Headline | `#1D1B20` (onSurface) | `#E6E0E9` |
| Supporting text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Leading icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Trailing icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Trailing text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Overline | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Divider | `#CAC4D0` (outlineVariant) | `#49454F` |

### States

| State | Effect |
|-------|--------|
| Enabled | Default |
| Hovered | State layer onSurface @ 8% |
| Focused | State layer onSurface @ 10% |
| Pressed | State layer onSurface @ 10% + ripple |
| Disabled | Headline onSurface @ 38%, no state layer |
| Selected | No built-in selected state (use checkbox/radio) |
| Dragged | State layer onSurface @ 16%, elevation Level 4 (8dp) |

### Layout Anatomy

```
+------------------------------------------------------------------+
| [Leading]  Headline text                        [Trailing]  16dp |
| 16dp gap   Supporting text                       element         |
+------------------------------------------------------------------+
```

#### One-line

```
+------------------------------------------------------------------+
| [Icon 24dp]  16dp  Headline                    [Switch]    24dp  |
+------------------------------------------------------------------+
                        56dp height
```

#### Two-line

```
+------------------------------------------------------------------+
|  8dp top padding                                                 |
| [Avatar 40dp] 16dp  Headline                   [Icon 24dp] 24dp |
|                      Supporting text                             |
|  8dp bottom padding                                              |
+------------------------------------------------------------------+
                        72dp height
```

#### Three-line

```
+------------------------------------------------------------------+
|  8dp top padding (content top-aligned)                           |
| [Thumb 56dp]  16dp  Headline                   [Checkbox]  24dp |
|                      Supporting line 1                           |
|                      Supporting line 2                           |
|  8dp bottom padding                                              |
+------------------------------------------------------------------+
                        88dp height
```

### Dividers

- Optional 1dp divider between list items
- Full-bleed or inset (indented past leading element)
- Color: outlineVariant
- Inset padding: 16dp + leading element width + 16dp gap

---

## Windows

Source: WinUI 3 ListView, GridView, ItemsView

### ListView (Standard List)

#### Item Metrics

| Property | Value |
|----------|-------|
| Item height (single-line) | 40px |
| Item height (two-line) | 60px |
| Item height (three-line) | 72px |
| Item padding (horizontal) | 12px |
| Item padding (vertical) | 8px |
| Item corner radius | 4px (controlCornerRadius) |
| Item margin (between items) | 2px vertical |
| Icon size (leading) | 16x16px or 20x20px |
| Icon-to-text gap | 12px |
| Font (primary text) | 14px, Regular |
| Font (secondary text) | 12px Caption, Regular |
| Secondary text color | TextFillColorSecondary |

#### Item States

| State | Background | Text | Indicator |
|-------|-----------|------|-----------|
| Rest | Transparent | TextFillColorPrimary | None |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary | None |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary | None |
| Selected | SubtleFillColorSecondary | TextFillColorPrimary | 3px accent pill (left edge) |
| Selected + Hover | SubtleFillColorTertiary | TextFillColorPrimary | 3px accent pill |
| Disabled | Transparent | TextFillColorDisabled | None |

#### Selection Indicator

When an item is selected, a **3px wide, 16px tall accent-colored pill** appears on the left edge of the item (vertically centered). This is the primary selection indicator.

| Property | Value |
|----------|-------|
| Width | 3px |
| Height | 16px |
| Corner radius | 1.5px (fully rounded) |
| Color | AccentFillColorDefault |
| Position | Left edge, vertically centered |

#### Group Header

| Property | Value |
|----------|-------|
| Font | 14px, SemiBold |
| Padding | 8px vertical, 12px horizontal |
| Separator | 1px DividerStrokeColorDefault below header |

### GridView (Grid Layout)

Same as ListView but items are arranged in a wrapping grid.

| Property | Value |
|----------|-------|
| Item size | Configurable (typical: 100x100px, 200x200px) |
| Item corner radius | 4px |
| Item gap | 4px |
| Selection check | Rounded checkbox in top-right corner |

### Swipe Actions

WinUI 3 SwipeControl can be added to list items:

| Property | Value |
|----------|-------|
| Action background | Configurable (e.g., SystemFillColorCritical for delete) |
| Action icon | 20x20px, white |
| Action text | 12px, white |
| Swipe threshold | 64px to reveal, 128px to execute |

### Empty State

| Property | Value |
|----------|-------|
| Illustration | Optional, centered |
| Message | 14px Body, TextFillColorSecondary, centered |
| Action button | Optional, Accent style |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Item hover fill | 100ms | Control fast |
| Selection indicator appear | 150ms | Decelerate |
| Selection indicator disappear | 100ms | Accelerate |
| Reorder (drag) | 200ms | Decelerate |
| Add item (entrance) | 200ms | Decelerate |
| Remove item (exit) | 150ms | Accelerate |
| Scrollbar expand | 150ms | Decelerate |
| Scrollbar collapse | 300ms | Accelerate |

---

## Linux

Source: GTK 4 (docs.gtk.org/gtk4), libadwaita

### Overview

GNOME provides multiple list widgets:

| Widget | Usage |
|--------|-------|
| `GtkListBox` | Simple vertical list of rows |
| `GtkListView` | Scalable list with recycling (for large datasets) |
| `GtkGridView` | Grid of items (icon grid) |

### GtkListBox (Simple List)

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | transparent (inherits parent) | transparent |
| Row background (rest) | transparent | transparent |
| Row background (hover) | `rgba(0,0,0, 0.04)` | `rgba(255,255,255, 0.04)` |
| Row background (active) | `rgba(0,0,0, 0.08)` | `rgba(255,255,255, 0.08)` |
| Row background (selected) | `rgba(0,0,0, 0.06)` | `rgba(255,255,255, 0.06)` |
| Separator | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Selection mode | Single / Multiple / None | -- |

#### Metrics

| Property | Value |
|----------|-------|
| Row min-height | 34px |
| Row padding | 8px 12px |
| Separator height | 1px |
| Corner radius (if boxed-list) | 12px |

#### Boxed List Style

Adding `.boxed-list` to a GtkListBox wraps it in a card:

| Property | Value |
|----------|-------|
| Container border | 1px `rgba(0,0,0, 0.12)` |
| Container radius | 12px |
| Container shadow | (0,1) blur 3, black @ 0.06 |
| Container background | card_bg_color |
| Row separator | full-width, inside card |
| First/last row | radius matches card corners |

### Row Types (for Boxed Lists)

libadwaita provides specialized row types:

#### AdwActionRow

| Property | Value |
|----------|-------|
| Title | 15px, Regular |
| Subtitle | 13px, dim-label |
| Prefix | Icon or widget, 12px left margin |
| Suffix | Widget (switch, button, arrow), 12px right margin |
| Activatable | Entire row clickable |
| Min-height | 50px (with subtitle), 34px (title only) |

#### AdwSwitchRow

| Property | Value |
|----------|-------|
| Layout | Title + subtitle on left, GtkSwitch on right |
| Toggle on click | Yes (entire row toggles switch) |

#### AdwComboRow

| Property | Value |
|----------|-------|
| Layout | Title + subtitle on left, dropdown on right |
| Dropdown style | Shows current value + chevron icon |
| Popover | Standard popover with list of options |

#### AdwExpanderRow

| Property | Value |
|----------|-------|
| Layout | Title + expander arrow |
| Arrow position | Right side |
| Animation | 250ms ease-in-out collapse/expand |
| Nested content | Indented child rows |

### Navigation Sidebar Style

Adding `.navigation-sidebar` to a GtkListBox:

| Property | Value |
|----------|-------|
| Row background (selected) | `--accent-bg-color` @ 0.12 |
| Row corner radius | 6px |
| Row margin | 6px horizontal |
| Row padding | 8px 12px |
| Row min-height | 34px |
| Row icon | 16px, 8px margin right |

### Rich List Style

Adding `.rich-list` to a GtkListBox:

| Property | Value |
|----------|-------|
| Row padding | 12px (increased from 8px) |
| Row min-height | 50px |
| Used for | Settings rows with larger touch targets |

### Focus and Keyboard

| Key | Action |
|-----|--------|
| Up / Down | Move selection |
| Space / Enter | Activate row |
| Ctrl+A | Select all (multi-select) |
| Escape | Clear selection |
| Home / End | Jump to first / last |
| Page Up / Page Down | Scroll by page |
| Type-ahead | Jump to matching row |

### Scrolling

| Property | Value |
|----------|-------|
| Scroll widget | GtkScrolledWindow wrapping the list |
| Scrollbar style | Overlay (appears on hover/scroll) |
| Scrollbar width | 8px (hover: 12px) |
| Kinetic scrolling | Enabled on touch |
| Overshoot | Elastic bounce indicator |
