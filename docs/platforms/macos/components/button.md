# macOS Button (NSButton)

Reference: NSButton, NSButton.BezelStyle, NSButton.ButtonType, Apple HIG (macOS 14+).

## Overview

macOS buttons come in many bezel styles and types. The primary push button is the most common. All buttons support four control sizes (mini, small, regular, large) since macOS 11.

## Bezel Styles

### NSButton.BezelStyle Enum

| Style                  | Raw | Description                                         | Usage Context          |
|------------------------|-----|-----------------------------------------------------|------------------------|
| `.automatic`           | 0   | System picks appropriate style for context           | Default                |
| `.push`                | 1   | Standard rounded push button                         | Window body            |
| `.flexiblePush`        | 2   | Push button that can grow vertically                 | Multiline labels       |
| `.disclosure`          | 5   | Disclosure triangle                                  | Expandable sections    |
| `.roundedDisclosure`   | 14  | Round button with disclosure arrow                   | Less common            |
| `.circular`            | 7   | Circular button for icons                            | Toolbars, palettes     |
| `.helpButton`          | 9   | Round question mark button                           | Help links             |
| `.smallSquare`         | 10  | Small square borderless button                       | Compact toolbar items  |
| `.toolbar`             | 12  | Toolbar-appropriate button                           | Toolbar items          |
| `.accessoryBarAction`  | 13  | Touch Bar / accessory bar style                      | Accessory bars         |
| `.accessoryBar`        | 15  | Accessory bar standard item                          | Accessory bars         |
| `.pushDisclosure`      | 16  | Push button with disclosure indicator                | Dropdown actions       |

### Deprecated Bezel Styles

| Style                  | Raw | Replacement                   |
|------------------------|-----|-------------------------------|
| `.rounded`             | 1   | Use `.push`                   |
| `.regularSquare`       | 2   | Use `.flexiblePush`           |
| `.texturedSquare`      | 8   | Use `.toolbar`                |
| `.texturedRounded`     | 11  | Use `.toolbar`                |
| `.recessed`            | 13  | Use `.accessoryBarAction`     |
| `.roundRect`           | 14  | Use `.accessoryBar`           |
| `.inline`              | 15  | Use `.accessoryBar`           |

## Button Types

| Type                     | Description                                   |
|--------------------------|-----------------------------------------------|
| `.momentaryLight`        | Highlights on press, returns to normal         |
| `.momentaryPushIn`       | Appears pushed in on press                     |
| `.momentaryChange`       | Shows alternate image/title on press           |
| `.pushOnPushOff`         | Toggles between pressed and normal             |
| `.toggle`                | Toggles alternate image/title on each click    |
| `.switch`                | Checkbox style                                 |
| `.radio`                 | Radio button style                             |
| `.onOff`                 | Stays highlighted when on                      |
| `.accelerator`           | Pressure-sensitive (Force Touch)               |
| `.multiLevelAccelerator` | Multi-level pressure-sensitive                 |

## Metrics

### Push Button (`.push`)

| Control Size | Height (pt) | Min Width (pt) | Corner Radius (pt) | Font Size (pt) | Font Weight  |
|-------------|-------------|----------------|---------------------|----------------|-------------|
| Mini        | 16          | 26             | 3                   | 9              | Regular     |
| Small       | 19          | 32             | 4                   | 11             | Regular     |
| Regular     | 22          | 48             | 6                   | 13             | Regular     |
| Large       | 28          | 48             | 8                   | 15             | Regular     |

### Horizontal Padding (text to edge)

| Control Size | Horizontal Padding (pt) |
|-------------|------------------------|
| Mini        | 6                      |
| Small       | 8                      |
| Regular     | 12                     |
| Large       | 16                     |

### Icon Button (`.circular`)

| Control Size | Diameter (pt) | Icon Size (pt) |
|-------------|---------------|----------------|
| Mini        | 16            | 10             |
| Small       | 20            | 13             |
| Regular     | 26            | 16             |
| Large       | 32            | 20             |

### Toolbar Button (`.toolbar`)

| Control Size | Height (pt) | Corner Radius (pt) | Notes                          |
|-------------|-------------|---------------------|--------------------------------|
| Regular     | 24          | 6                   | Default for toolbars           |
| Small       | 20          | 4                   | Compact toolbars               |

## Colors

### Push Button (Default)

| State      | Background Light           | Background Dark             | Text Light    | Text Dark     |
|------------|----------------------------|-----------------------------|---------------|---------------|
| Normal     | White gradient (#FFFFFF to #F5F5F5) | `rgba(255,255,255,0.10)` | `#262626`     | `#E5E5E5`    |
| Hover      | White gradient (#FFFFFF to #F0F0F0) | `rgba(255,255,255,0.14)` | `#262626`     | `#E5E5E5`    |
| Pressed    | `#DCDCDC`                  | `rgba(255,255,255,0.06)`   | `#262626`     | `#E5E5E5`    |
| Disabled   | `rgba(0,0,0,0.04)`        | `rgba(255,255,255,0.04)`   | `rgba(0,0,0,0.25)` | `rgba(255,255,255,0.25)` |

### Push Button (Default / Primary / Accent)

The window's default button uses the accent color fill:

| State      | Background Light       | Background Dark        | Text Light | Text Dark  |
|------------|------------------------|------------------------|------------|------------|
| Normal     | `#007AFF`              | `#0A84FF`              | `#FFFFFF`  | `#FFFFFF`  |
| Hover      | `#0071EB`              | `#0C7AEF`              | `#FFFFFF`  | `#FFFFFF`  |
| Pressed    | `#0062CC`              | `#0068C4`              | `#FFFFFF`  | `#FFFFFF`  |
| Disabled   | `rgba(0,122,255,0.40)` | `rgba(10,132,255,0.40)`| `rgba(255,255,255,0.50)` | `rgba(255,255,255,0.50)` |

### Destructive Button

| State      | Background Light       | Background Dark        | Text Light | Text Dark  |
|------------|------------------------|------------------------|------------|------------|
| Normal     | `#FF3B30`              | `#FF453A`              | `#FFFFFF`  | `#FFFFFF`  |
| Hover      | `#E6352B`              | `#E63F35`              | `#FFFFFF`  | `#FFFFFF`  |
| Pressed    | `#CC2F26`              | `#CC3830`              | `#FFFFFF`  | `#FFFFFF`  |

### Toolbar Button (`.toolbar`)

| State      | Background Light         | Background Dark            |
|------------|--------------------------|----------------------------|
| Normal     | Transparent              | Transparent                |
| Hover      | `rgba(0,0,0,0.06)`      | `rgba(255,255,255,0.08)`   |
| Pressed    | `rgba(0,0,0,0.10)`      | `rgba(255,255,255,0.12)`   |
| Selected   | `rgba(0,0,0,0.08)`      | `rgba(255,255,255,0.10)`   |

## Border

Standard push buttons have a 0.5 pt border:

| State      | Border Light              | Border Dark                  |
|------------|---------------------------|------------------------------|
| Normal     | `rgba(0,0,0,0.12)`       | `rgba(255,255,255,0.12)`     |
| Focused    | `rgba(0,122,255,0.50)` (focus ring) | `rgba(10,132,255,0.50)` |
| Disabled   | `rgba(0,0,0,0.06)`       | `rgba(255,255,255,0.06)`     |

## Shadow

Normal push button shadow:

```
Color:   rgba(0, 0, 0, 0.06)
Offset:  (0, 0.5)
Blur:    1.5 pt
```

Pressed state removes the shadow.

## States

| State        | Visual Changes                                         |
|--------------|--------------------------------------------------------|
| Normal       | Default appearance with subtle shadow                  |
| Hover        | Slightly brighter/darker background                    |
| Pressed      | Inset appearance, no shadow, darker fill               |
| Focused      | Focus ring (3 pt accent-colored ring, 2 pt offset)     |
| Disabled     | 40% opacity on fill, 25% opacity on text               |
| Default      | Blue/accent fill, pulsing animation (legacy, now static)|
| On (toggle)  | Accent color tint for selected state                   |

## Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Hover in            | 50            | Ease Out      |
| Hover out           | 150           | Ease In Out   |
| Press               | 30            | Ease Out      |
| Release             | 100           | Ease Out      |
| Disable/Enable      | 200           | Ease In Out   |

## Checkbox (`.switch` type)

| Control Size | Box Size (pt) | Corner Radius (pt) | Checkmark Stroke (pt) |
|-------------|---------------|--------------------|-----------------------|
| Mini        | 10            | 2                  | 1.0                   |
| Small       | 12            | 2.5                | 1.0                   |
| Regular     | 14            | 3                  | 1.5                   |
| Large       | 18            | 4                  | 2.0                   |

Checkbox colors:
- Unchecked: white fill with 0.5 pt border (`rgba(0,0,0,0.20)`)
- Checked: accent color fill, white checkmark
- Mixed (indeterminate): accent color fill, white dash

## Radio Button (`.radio` type)

| Control Size | Outer Diameter (pt) | Inner Dot Diameter (pt) |
|-------------|---------------------|------------------------|
| Mini        | 10                  | 4                      |
| Small       | 12                  | 5                      |
| Regular     | 16                  | 6                      |
| Large       | 20                  | 8                      |

## Keyboard Shortcuts

| Action          | Key                        |
|-----------------|----------------------------|
| Activate button | Space / Return (if default)|
| Cancel          | Escape (Cancel button)     |
| Toggle checkbox | Space                      |
| Tab to next     | Tab                        |
| Tab to previous | Shift+Tab                  |

## Dija Skin Mapping

```
comp! Button {
    attr variant, ButtonVariant, default: ButtonVariant::Solid
    attr size, Size, default: Size::MD
    attr disabled, bool, default: false

    // macOS skin should map:
    // Size::XS  -> controlSize .mini
    // Size::SM  -> controlSize .small
    // Size::MD  -> controlSize .regular
    // Size::LG  -> controlSize .large
    // ButtonVariant::Solid   -> accent-filled push button (Push accent)
    // ButtonVariant::Outline -> standard push button (Push default)
    // ButtonVariant::Soft    -> (no direct macOS equivalent)
    // ButtonVariant::Ghost   -> toolbar-style borderless (Toolbar)
    // ButtonVariant::White   -> standard push button (Push default)
}
```
