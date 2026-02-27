# Search Bar

A text input field optimized for search queries, typically featuring a magnifying glass icon, placeholder text, a clear button, and optional features like search suggestions, cancel actions, and scope filtering.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UISearchBar / UISearchController | Documented |
| macOS | NSSearchField | Documented |
| Android | Search Bar (Material Design 3) | Documented |
| Windows | AutoSuggestBox | Documented |
| Linux | GtkSearchBar / GtkSearchEntry | Documented |

## iOS

Source: UISearchBar, UISearchController, SwiftUI `.searchable`

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | tertiarySystemFill (`#767680` @ 0.12) | tertiarySystemFill (`#767680` @ 0.24) |
| Corner radius | 10pt | 10pt |
| Corner curve | `.continuous` (superellipse) | |
| Height | 36pt (search field), 56pt (with bar chrome) | |
| Border | None (flat fill) | |

### Search Field Metrics

| Property | Value |
|----------|-------|
| Left padding | 8pt (from left edge to search icon) |
| Search icon to text | 6pt |
| Text right padding | 28pt (space for clear button) |
| Font | SF Pro Regular, 17pt |
| Text color | label |
| Placeholder text | "Search" (localized) |
| Placeholder color | secondaryLabel |
| Cursor color | tintColor |

### Icons

| Icon | Symbol | Size | Color |
|------|--------|------|-------|
| Search (magnifying glass) | `magnifyingglass` | 14pt | secondaryLabel |
| Clear (x circle) | `xmark.circle.fill` | 17pt | tertiaryLabel |
| Bookmark (optional) | `book` | 14pt | secondaryLabel |
| Dictation (microphone) | `mic.fill` | 14pt | secondaryLabel |

### Cancel Button

| Property | Value |
|----------|-------|
| Text | "Cancel" |
| Font | SF Pro Regular, 17pt |
| Color | tintColor |
| Position | Right of search field |
| Spacing | 8pt from search field |
| Visibility | Hidden by default, slides in on focus |
| Animation | Slide in from right, 0.25s ease-in-out |

### States

| State | Search Field | Cancel |
|-------|-------------|--------|
| Inactive | Rounded rect, placeholder shown | Hidden |
| Focused (empty) | Cursor visible, cancel slides in | Visible |
| Focused (text) | Text shown, clear button visible | Visible |
| Results | Search field may stay focused or blur | May hide |

### Search Bar Styles

| Style | Description |
|-------|-------------|
| Prominent (default) | Translucent background bar with search field |
| Minimal | Only the search field, no background bar |

### Navigation Bar Integration

When embedded in a navigation bar via UISearchController:

| Property | Value |
|----------|-------|
| Position | Below large title, above content |
| Default visibility | Hidden (revealed on pull-down scroll) |
| Always visible | Optional (`hidesSearchBarWhenScrolling = false`) |
| Focus behavior | Navigation bar collapses, search bar pins to top |
| Scope bar | Optional segment control below search field |

#### Scope Bar

| Property | Value |
|----------|-------|
| Style | Segmented control |
| Height | 32pt |
| Position | Below search bar |
| Background | Same as search bar background |
| Visibility | Shown when search is focused (configurable) |
| Animation | Slides down, 0.25s |

### Search Suggestions

iOS 16+ supports search suggestions displayed below the search bar:

| Property | Value |
|----------|-------|
| Suggestion row height | 44pt |
| Icon | SF Symbol, 22pt, tintColor |
| Text font | SF Pro Regular, 17pt |
| Text color | label |
| Background | systemBackground |
| Separator | Standard (0.33pt, 20pt inset) |

### Search Tokens

iOS 13+ supports search tokens (structured filter chips):

| Property | Value |
|----------|-------|
| Token height | ~24pt |
| Background | tintColor @ 0.15 |
| Corner radius | 6pt |
| Text font | SF Pro Regular, 15pt |
| Text color | tintColor |
| Icon size | 16pt |
| Padding | 4pt vertical, 8pt horizontal |
| Removable | Backspace deletes token |

### Animation

| Transition | Duration | Curve |
|-----------|----------|-------|
| Focus (cancel slides in) | 0.25s | ease-in-out |
| Blur (cancel slides out) | 0.2s | ease-in-out |
| Navigation collapse on focus | 0.25s | ease-in-out |
| Scope bar appear | 0.25s | ease-in-out |
| Clear button appear | 0.15s | fade |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Search field |
| VoiceOver | "Search field, [placeholder or text]" |
| Cancel | "Cancel, button" |
| Clear | "Clear text, button" |
| Scope | "Scope bar, [selected], [N] of [total]" |

## macOS

Reference: NSSearchField, NSSearchFieldCell, Apple HIG (macOS 14+).

### Overview

`NSSearchField` is a specialized text field for search input. It features a magnifying glass icon, clear button, optional search menu, and cancel button. It uses a rounded bezel (capsule shape) by default and integrates with macOS search patterns.

### Metrics

#### Dimensions

| Control Size | Height (pt) | Corner Radius (pt) | Font Size (pt) | Icon Size (pt) |
|-------------|-------------|---------------------|----------------|----------------|
| Mini        | 16          | 8 (capsule)         | 9              | 9              |
| Small       | 19          | 9.5 (capsule)       | 11             | 11             |
| Regular     | 22          | 11 (capsule)        | 13             | 13             |
| Large       | 28          | 14 (capsule)        | 15             | 15             |

#### Internal Layout

```
+-----------------------------------------------+
| [mag] [placeholder / input text]    [x] [menu] |
+-----------------------------------------------+
```

| Element                    | Value (pt)  | Notes                               |
|----------------------------|------------|---------------------------------------|
| Magnifying glass left pad  | 6          | From left edge to icon                |
| Magnifying glass size      | 13         | Regular control size                  |
| Icon to text gap           | 4          | Gap between icon and input area       |
| Clear button size          | 14         | Circular X button                     |
| Clear button right pad     | 6          | From right edge to button             |
| Text to clear button gap   | 4          | Minimum gap                           |
| Menu chevron width         | 8          | When search menu is attached          |
| Menu chevron gap           | 2          | Gap between mag glass and chevron     |

#### Toolbar Search Field

In a toolbar, the search field has additional behavior:

| Property                  | Value              |
|---------------------------|--------------------|
| Collapsed width            | 28 pt (icon only) |
| Expanded width             | 180-240 pt        |
| Expand animation           | 250 ms Ease In Out |
| Collapse animation         | 200 ms Ease In Out |

When collapsed, only the magnifying glass icon is visible. Clicking expands to the full search field.

### Colors

#### Background

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Hover        | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.10)`       |
| Focused      | `#FFFFFF`                     | `#1E1E1E`                      |
| Disabled     | `rgba(0,0,0,0.03)`           | `rgba(255,255,255,0.04)`       |

Note: The search field background is semi-transparent gray when unfocused, switching to opaque white/dark when focused. This is a distinct behavior from `NSTextField`.

#### Border

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.08)`       |
| Hover        | `rgba(0,0,0,0.12)`           | `rgba(255,255,255,0.12)`       |
| Focused      | controlAccentColor (focus ring) | controlAccentColor (focus ring) |
| Disabled     | `rgba(0,0,0,0.04)`           | `rgba(255,255,255,0.04)`       |

Border width: 0.5 pt.

#### Icons and Text

| Element              | Light Mode              | Dark Mode               |
|---------------------|-------------------------|-------------------------|
| Magnifying glass     | `rgba(0,0,0,0.40)`     | `rgba(255,255,255,0.40)`|
| Clear button X       | `rgba(0,0,0,0.30)`     | `rgba(255,255,255,0.30)`|
| Clear button hover   | `rgba(0,0,0,0.50)`     | `rgba(255,255,255,0.50)`|
| Clear button bg hover| `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.10)`|
| Placeholder text     | placeholderTextColor    | placeholderTextColor    |
| Input text           | textColor               | textColor               |
| Menu chevron         | `rgba(0,0,0,0.40)`     | `rgba(255,255,255,0.40)`|

### Clear Button

The clear button (X) appears only when there is text in the field:

| Property                  | Value              |
|---------------------------|--------------------|
| Shape                      | Circle with X glyph |
| Diameter                   | 14 pt (regular)   |
| X glyph size               | 8 pt              |
| Appear animation           | 100 ms fade in    |
| Disappear animation        | 80 ms fade out    |
| Hover: background circle   | Yes, subtle gray   |

### Search Menu

An optional menu attached to the magnifying glass icon:

| Property                  | Value                      |
|---------------------------|----------------------------|
| Trigger                    | Click on magnifying glass  |
| Menu appearance            | Standard NSMenu            |
| Chevron indicator          | Small down arrow next to mag glass |
| Common items               | Recent Searches, Clear Recent |
| Recent searches limit      | 10 items (configurable)    |

### States

| State           | Visual Changes                                       |
|-----------------|------------------------------------------------------|
| Normal          | Gray translucent background, magnifying glass icon   |
| Hover           | Slightly darker background                            |
| Focused (empty) | White/dark opaque background, focus ring, placeholder |
| Focused (text)  | White/dark bg, focus ring, text, clear button visible |
| Has text        | Input text visible, clear button visible              |
| Disabled        | Dimmed, no interaction                                |

### Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from field bounds
Radius:   field corner radius + 3 pt (capsule + 3)
```

### Token / Tag Display

Some search fields support search tokens (macOS 11+):

| Property                  | Value              |
|---------------------------|--------------------|
| Token height               | 18 pt             |
| Token corner radius        | 4 pt              |
| Token horizontal padding   | 6 pt              |
| Token background           | controlAccentColor at 15% opacity |
| Token text color           | controlAccentColor |
| Token selected background  | controlAccentColor |
| Token selected text        | `#FFFFFF`          |
| Token spacing              | 4 pt              |

### Animation

| Transition                    | Duration (ms) | Curve          |
|-------------------------------|---------------|----------------|
| Focus (gray -> white bg)      | 150           | Ease Out       |
| Unfocus (white -> gray bg)    | 200           | Ease In        |
| Clear button appear           | 100           | Fade in        |
| Clear button disappear        | 80            | Fade out       |
| Focus ring appear             | 150           | Ease Out       |
| Focus ring disappear          | 200           | Ease In        |
| Toolbar expand                | 250           | Ease In Out    |
| Toolbar collapse              | 200           | Ease In Out    |

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Escape          | Clear text, or cancel/dismiss if empty     |
| Return          | Perform search                             |
| Cmd+A           | Select all text                            |
| Option+Delete   | Delete word                                |
| Cmd+Delete      | Delete to beginning of line                |

Standard text editing shortcuts apply (see text-field.md).

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.searchField`                            |
| Subrole      | `.searchField`                            |
| Description  | "Search" or custom label                   |
| Value        | Current search text                        |
| Children     | Clear button, search menu button           |

### Dija Skin Mapping

```
comp! SearchField {
    attr placeholder, &str, default: "Search"
    attr size, Size, default: Size::MD
    attr disabled, bool, default: false
    attr search_menu, bool, default: false
    attr tokens, bool, default: false

    // macOS skin maps:
    // Capsule shape (corner radius = height/2)
    // Unfocused: translucent gray bg
    // Focused: opaque white/dark bg + focus ring
    // Magnifying glass icon: left side
    // Clear button: right side, appears on text input
    // Toolbar mode: collapsible to icon-only
}
```

## Android

Source: m3.material.io/components/search/specs

### Variants

| Variant | State | Description |
|---------|-------|------------|
| Search bar (docked) | Resting | Persistent bar in the layout |
| Search view (expanded) | Active | Full-width/full-screen search with suggestions |

### Search Bar (Docked) Metrics

| Property | Value |
|----------|-------|
| Height | 56dp |
| Corner radius | 28dp (full pill) |
| Surface | surfaceContainerHigh |
| Elevation | Level 2 (3dp) |
| Horizontal padding | 16dp |
| Leading icon size | 24dp |
| Trailing icon size | 24dp |
| Leading icon to text gap | 16dp |
| Text to trailing icon gap | 16dp |
| Placeholder font | Body Large (Roboto Regular, 16sp) |
| Input font | Body Large (Roboto Regular, 16sp) |

### Search View (Expanded) Metrics

| Property | Value |
|----------|-------|
| Height (header) | 72dp |
| Corner radius | 0dp (full width) or 28dp (overlay) |
| Surface | surfaceContainerHigh |
| Elevation | Level 2 (3dp) |
| Back icon size | 24dp |
| Clear icon size | 24dp |
| Input font | Body Large (Roboto Regular, 16sp) |
| Suggestion item height | 56dp |
| Suggestion icon size | 24dp |
| Suggestion font | Body Large (Roboto Regular, 16sp) |
| Divider | 1dp, outlineVariant |

### Colors

#### Search Bar

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainerHigh) | `#2B2930` |
| Leading icon | `#49454F` (onSurface) | `#E6E0E9` |
| Placeholder text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Input text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Trailing icon (avatar/action) | `#49454F` (onSurfaceVariant) | `#CAC4D0` |

#### Search View

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainerHigh) | `#2B2930` |
| Back icon | `#1D1B20` (onSurface) | `#E6E0E9` |
| Input text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Clear icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Suggestion text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Suggestion icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Divider | `#CAC4D0` (outlineVariant) | `#49454F` |

### States

#### Search Bar States

| State | Effect |
|-------|--------|
| Resting | Default styling |
| Hovered | State layer 8% (onSurface) |
| Focused | Transitions to search view (expanded) |
| Pressed | Transitions to search view |

#### Search View States

| State | Effect |
|-------|--------|
| Active | Input focused, keyboard visible |
| With results | Suggestion list below input |
| Empty | No suggestions, optional empty state |

### Transition Animation

Search bar to search view:

| Property | Duration | Easing |
|----------|----------|--------|
| Container morph | Medium 3 (350ms) | Emphasized decelerate |
| Corner radius (28dp -> 0dp) | Medium 2 (300ms) | Standard |
| Content cross-fade | Short 4 (200ms) | Standard |
| Suggestion list enter | Medium 1 (250ms) | Emphasized decelerate |

Search view to search bar (dismiss):

| Property | Duration | Easing |
|----------|----------|--------|
| Container morph | Medium 2 (300ms) | Standard accelerate |
| Corner radius (0dp -> 28dp) | Medium 2 (300ms) | Standard |
| Content cross-fade | Short 3 (150ms) | Standard |

### Layout

#### Search Bar (Resting)

```
+-----------------------------------------------------------+
|  16dp  [Search icon]  16dp  "Search..."   [Avatar]  16dp  |
+-----------------------------------------------------------+
                        56dp height
                      28dp corner radius
```

#### Search View (Expanded)

```
+-----------------------------------------------------------+
|  [<- Back]  16dp  "query text..."  [X Clear]              |
+-----------------------------------------------------------+  72dp header
|  -------divider (1dp)-------                              |
|  [Clock icon]  16dp  Recent search 1                      |  56dp
|  [Clock icon]  16dp  Recent search 2                      |  56dp
|  [Search icon] 16dp  Suggestion 1                         |  56dp
|  [Search icon] 16dp  Suggestion 2                         |  56dp
+-----------------------------------------------------------+
```

### Comparison with iOS

| Property | iOS Search Bar | M3 Search Bar |
|----------|---------------|--------------|
| Corner radius | 10dp (squircle) | 28dp (pill) |
| Background | systemGray6 | surfaceContainerHigh |
| Height | 36dp | 56dp |
| Cancel button | Text, right side | Back arrow, left side |
| Clear button | Circle X in field | X icon, right side |
| Scope bar | Segmented control below | Not standard |

## Windows

Source: WinUI 3 AutoSuggestBox control

### Appearance

An input field with a query icon and a dropdown suggestion list. Looks like a TextBox with search functionality.

#### Input Field

Same visual treatment as TextBox, with additional query icon.

| Property | Value |
|----------|-------|
| Height | 32px |
| Background | ControlFillColorDefault |
| Border | 1px ControlStrokeColorDefault + darker bottom stroke |
| Corner radius | 4px (controlCornerRadius) |
| Padding | 11px left, 5px top, 36px right (space for icons), 6px bottom |
| Font | 14px, Regular (400) |
| Placeholder | TextFillColorTertiary |
| Placeholder text | "Search" (localizable) |

#### Query Icon

| Property | Value |
|----------|-------|
| Icon | `&#xE721;` (Search / magnifying glass) |
| Size | 12x12px glyph |
| Hit area | 32x32px |
| Position | Right side of input |
| Color | TextFillColorSecondary |
| Background | Transparent (subtle on hover) |

#### Clear Button

| Property | Value |
|----------|-------|
| Icon | `&#xE10A;` (X / Cancel) |
| Size | 12x12px glyph |
| Visibility | Shown when text is present |
| Position | Right side, left of query icon |
| Hit area | 30x32px |

### Input States

| State | Background | Border | Bottom stroke |
|-------|-----------|--------|---------------|
| Rest | ControlFillColorDefault | ControlStrokeColorDefault | ControlStrokeColorSecondary |
| Hover | ControlFillColorSecondary | ControlStrokeColorDefault | ControlStrokeColorSecondary |
| Focused | ControlFillColorInputActive | ControlStrokeColorDefault | AccentColor (2px) |
| Disabled | ControlFillColorDisabled | ControlStrokeColorDefault (reduced) | None |

Same bottom accent stroke animation as TextBox on focus.

### Suggestion Dropdown

#### Container

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Border | 1px SurfaceStrokeColorFlyout |
| Shadow | Shadow 8 |
| Padding | 4px vertical |
| Gap from input | 4px |
| Max height | 384px (scrollable) |
| Min width | Same as input field width |

#### Suggestion Item

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px horizontal |
| Corner radius | 4px (with 2px horizontal margin) |
| Font | 14px, Regular |
| Icon size | 16x16px (optional leading icon) |
| Icon-to-text gap | 12px |

#### Suggestion Item States

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Selected (keyboard) | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |

#### No Results

| Property | Value |
|----------|-------|
| Message | "No results found" or custom |
| Font | 14px, Regular |
| Color | TextFillColorSecondary |
| Padding | 12px |
| Alignment | Center |

### Structure

```
+----------------------------------+
| [search text]          [X] [mag] |  <- Input field
+----------------------------------+
  +------------------------------+
  | Suggestion item 1            |  <- Dropdown
  | Suggestion item 2            |
  | Suggestion item 3 (selected) |
  | ...                          |
  +------------------------------+
```

### Events / API

| Event | When |
|-------|------|
| TextChanged | User types or clears text |
| SuggestionChosen | User selects a suggestion (tap or keyboard enter) |
| QuerySubmitted | User presses Enter or taps the query icon |

### Keyboard Navigation

| Key | Action |
|-----|--------|
| Down arrow | Move to first/next suggestion |
| Up arrow | Move to previous suggestion |
| Enter | Submit query or select highlighted suggestion |
| Escape | Close dropdown, clear selection |
| Tab | Move focus to next control (closes dropdown) |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Dropdown open | 200ms | Decelerate |
| Dropdown close | 150ms | Accelerate |
| Suggestion hover fill | 100ms | Control fast |
| Bottom accent stroke (focus) | 200ms | Decelerate |
| Input background transition | 100ms | Control fast |

## Linux

### Overview

GNOME provides two search-related widgets:

| Widget | Role |
|--------|------|
| `GtkSearchBar` | Container that reveals/hides a search entry in the toolbar area |
| `GtkSearchEntry` | The actual text input with search icon and clear button |

### GtkSearchBar

#### Appearance

The search bar is a toolbar-height container that slides down below the header bar
when search mode is activated.

| Property | Light | Dark |
|----------|-------|------|
| Background | Same as header bar (`#EBEBEB`) | `#303030` |
| Bottom border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Style | `.toolbar` (inherits toolbar appearance) | -- |

#### Metrics

| Property | Value |
|----------|-------|
| Height | 47px (same as header bar) |
| Padding | 6px horizontal, 6px vertical |
| Entry max-width | 400px (centered in bar) |

#### Reveal Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Reveal (slide down) | 250ms | ease-out-cubic |
| Hide (slide up) | 200ms | ease-in-cubic |

### GtkSearchEntry

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FFFFFF` (view_bg_color) | `#1E1E1E` |
| Text color | `#2E3436` | `#FFFFFF` |
| Placeholder color | `rgba(46,52,54, 0.50)` | `rgba(255,255,255, 0.50)` |
| Border (rest) | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Border (focused) | 2px `--accent-color` | 2px `--accent-color` |
| Corner radius | 6px | 6px |
| Shadow | none | none |

#### Metrics

| Property | Value |
|----------|-------|
| Min height | 34px |
| Horizontal padding | 12px |
| Vertical padding | 8px |
| Corner radius | 6px |
| Font | Adwaita Sans Regular, 15px |

#### Icons

| Position | Icon | Size | Behavior |
|----------|------|------|----------|
| Prefix (left) | Search (magnifying glass) | 16x16px | Static, always visible |
| Suffix (right) | Clear (X circle) | 16x16px | Visible only when text present |

#### Clear Button

| Property | Value |
|----------|-------|
| Icon | `edit-clear-symbolic` (X in circle) |
| Size | 16x16px |
| Hit area | 24x24px |
| Style | Flat, transparent until hover |
| Hover bg | `rgba(0,0,0, 0.07)` |
| Active bg | `rgba(0,0,0, 0.12)` |
| Corner radius | 50% (circular) |

### States

| State | Border | Background | Notes |
|-------|--------|------------|-------|
| Rest | 1px, `rgba(0,0,0,0.15)` | view_bg_color | -- |
| Hover | 1px, `rgba(0,0,0,0.25)` | view_bg_color | Stronger border |
| Focused | 2px, accent_color | view_bg_color | Accent highlight |
| Has text | same as rest/focused | view_bg_color | Clear button visible |
| Empty + unfocused | 1px border | view_bg_color | Placeholder visible |
| Disabled | 1px, `rgba(0,0,0,0.10)` | `rgba(0,0,0,0.04)` | Opacity 0.5 |

### Inline Search (within header bar)

The search entry can be placed directly in the header bar as the title widget:

| Property | Value |
|----------|-------|
| Position | Center of header bar (replaces title) |
| Max width | Expands to available space |
| Entry style | Same as standalone |
| Toggle | Search icon button activates/deactivates |

### Search Behavior

| Feature | Detail |
|---------|--------|
| Auto-search | Typing starts after a delay (150ms debounce) |
| search-changed signal | Fires on each keystroke (after debounce) |
| Stop search signal | Fires on Escape |
| Activate signal | Fires on Enter (select first result) |
| Min characters | Typically 1 (app configurable) |
| Capture | `GtkSearchBar` captures key events from its key-capture-widget |

#### Key Capture

`GtkSearchBar` has a `key-capture-widget` property (typically the window). When set,
typing anywhere in the window activates the search bar and forwards keystrokes:

| Behavior | Detail |
|----------|--------|
| Typing starts search | First printable character opens search bar |
| Escape closes search | Hides search bar, clears entry |
| Focus returns | Focus returns to previous widget after closing |

### Keyboard Support

| Key | Action |
|-----|--------|
| Ctrl+F | Toggle search bar (convention) |
| Escape | Close search bar, clear entry |
| Enter | Activate / select first result |
| Type any character | Auto-open search bar (with key capture) |
| Ctrl+A | Select all text in entry |
| Backspace (empty) | Close search bar |

### Search Suggestions / Results

GNOME does not have a built-in search suggestions dropdown. Apps implement their
own results display, typically:

| Pattern | Description |
|---------|-------------|
| Filtered list | `GtkListBox` below search bar, rows filter in real time |
| Column view | `GtkColumnView` filters, showing matching rows |
| Status page | `AdwStatusPage` shown when no results |

#### No Results State

| Property | Value |
|----------|-------|
| Icon | `system-search-symbolic`, 48px |
| Title | "No Results Found" |
| Subtitle | "Try a different search term" |
| Widget | `AdwStatusPage` |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Search bar reveal | 250ms | ease-out-cubic |
| Search bar hide | 200ms | ease-in-cubic |
| Clear button appear | 150ms | ease-out |
| Clear button disappear | 100ms | ease-in |
| Border focus transition | 200ms | ease-in-out |
| Placeholder fade | 150ms | ease-in-out |
