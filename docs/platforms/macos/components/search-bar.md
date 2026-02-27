# macOS Search Field (NSSearchField)

Reference: NSSearchField, NSSearchFieldCell, Apple HIG (macOS 14+).

## Overview

`NSSearchField` is a specialized text field for search input. It features a magnifying glass icon, clear button, optional search menu, and cancel button. It uses a rounded bezel (capsule shape) by default and integrates with macOS search patterns.

## Metrics

### Dimensions

| Control Size | Height (pt) | Corner Radius (pt) | Font Size (pt) | Icon Size (pt) |
|-------------|-------------|---------------------|----------------|----------------|
| Mini        | 16          | 8 (capsule)         | 9              | 9              |
| Small       | 19          | 9.5 (capsule)       | 11             | 11             |
| Regular     | 22          | 11 (capsule)        | 13             | 13             |
| Large       | 28          | 14 (capsule)        | 15             | 15             |

### Internal Layout

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

### Toolbar Search Field

In a toolbar, the search field has additional behavior:

| Property                  | Value              |
|---------------------------|--------------------|
| Collapsed width            | 28 pt (icon only) |
| Expanded width             | 180-240 pt        |
| Expand animation           | 250 ms Ease In Out |
| Collapse animation         | 200 ms Ease In Out |

When collapsed, only the magnifying glass icon is visible. Clicking expands to the full search field.

## Colors

### Background

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Hover        | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.10)`       |
| Focused      | `#FFFFFF`                     | `#1E1E1E`                      |
| Disabled     | `rgba(0,0,0,0.03)`           | `rgba(255,255,255,0.04)`       |

Note: The search field background is semi-transparent gray when unfocused, switching to opaque white/dark when focused. This is a distinct behavior from `NSTextField`.

### Border

| State        | Light Mode                    | Dark Mode                      |
|-------------|-------------------------------|--------------------------------|
| Normal       | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.08)`       |
| Hover        | `rgba(0,0,0,0.12)`           | `rgba(255,255,255,0.12)`       |
| Focused      | controlAccentColor (focus ring) | controlAccentColor (focus ring) |
| Disabled     | `rgba(0,0,0,0.04)`           | `rgba(255,255,255,0.04)`       |

Border width: 0.5 pt.

### Icons and Text

| Element              | Light Mode              | Dark Mode               |
|---------------------|-------------------------|-------------------------|
| Magnifying glass     | `rgba(0,0,0,0.40)`     | `rgba(255,255,255,0.40)`|
| Clear button X       | `rgba(0,0,0,0.30)`     | `rgba(255,255,255,0.30)`|
| Clear button hover   | `rgba(0,0,0,0.50)`     | `rgba(255,255,255,0.50)`|
| Clear button bg hover| `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.10)`|
| Placeholder text     | placeholderTextColor    | placeholderTextColor    |
| Input text           | textColor               | textColor               |
| Menu chevron         | `rgba(0,0,0,0.40)`     | `rgba(255,255,255,0.40)`|

## Clear Button

The clear button (X) appears only when there is text in the field:

| Property                  | Value              |
|---------------------------|--------------------|
| Shape                      | Circle with X glyph |
| Diameter                   | 14 pt (regular)   |
| X glyph size               | 8 pt              |
| Appear animation           | 100 ms fade in    |
| Disappear animation        | 80 ms fade out    |
| Hover: background circle   | Yes, subtle gray   |

## Search Menu

An optional menu attached to the magnifying glass icon:

| Property                  | Value                      |
|---------------------------|----------------------------|
| Trigger                    | Click on magnifying glass  |
| Menu appearance            | Standard NSMenu            |
| Chevron indicator          | Small down arrow next to mag glass |
| Common items               | Recent Searches, Clear Recent |
| Recent searches limit      | 10 items (configurable)    |

## States

| State           | Visual Changes                                       |
|-----------------|------------------------------------------------------|
| Normal          | Gray translucent background, magnifying glass icon   |
| Hover           | Slightly darker background                            |
| Focused (empty) | White/dark opaque background, focus ring, placeholder |
| Focused (text)  | White/dark bg, focus ring, text, clear button visible |
| Has text        | Input text visible, clear button visible              |
| Disabled        | Dimmed, no interaction                                |

## Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from field bounds
Radius:   field corner radius + 3 pt (capsule + 3)
```

## Token / Tag Display

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

## Animation

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

## Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Escape          | Clear text, or cancel/dismiss if empty     |
| Return          | Perform search                             |
| Cmd+A           | Select all text                            |
| Option+Delete   | Delete word                                |
| Cmd+Delete      | Delete to beginning of line                |

Standard text editing shortcuts apply (see text-field.md).

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.searchField`                            |
| Subrole      | `.searchField`                            |
| Description  | "Search" or custom label                   |
| Value        | Current search text                        |
| Children     | Clear button, search menu button           |

## Dija Skin Mapping

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
