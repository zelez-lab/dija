# macOS Alert (NSAlert)

Reference: NSAlert, NSPanel, Apple HIG (macOS 14+).

## Overview

`NSAlert` presents a modal dialog for critical information, error conditions, or confirmation requests. Alerts can be displayed as standalone modal dialogs or as sheets attached to a window.

## Alert Styles

### NSAlert.Style

| Style              | Icon                                  | Usage                          |
|--------------------|---------------------------------------|--------------------------------|
| `.informational`   | App icon                              | General information            |
| `.warning`         | App icon with caution triangle        | Potentially destructive action |
| `.critical`        | App icon with red stop sign overlay   | Data loss, errors              |

## Layout

### Dialog Structure

```
+-------------------------------------------+
|  [Icon]  Message Text                     |
|          Informative Text                 |
|                                           |
|          [Accessory View (optional)]      |
|                                           |
|          [Suppression Checkbox (optional)]|
|                                           |
|  [Help]        [Other] [Cancel] [Default] |
+-------------------------------------------+
```

### Dimensions

| Property                  | Value (pt)   | Notes                         |
|---------------------------|-------------|-------------------------------|
| Minimum width              | 260         |                               |
| Maximum width              | 460         | Expands for long text          |
| Standard width             | 340         | Most common alert width        |
| Corner radius              | 10          | Matches window radius          |
| Content padding (top)      | 20          |                               |
| Content padding (sides)    | 20          |                               |
| Content padding (bottom)   | 20          |                               |

### Icon

| Property                  | Value          |
|---------------------------|----------------|
| Icon size                  | 64x64 pt      |
| Icon to text gap           | 16 pt         |
| Icon position              | Top-left       |
| Icon vertical alignment    | Top-aligned with message text |

### Text Area

| Property                  | Value          |
|---------------------------|----------------|
| Text area width            | Alert width - 64 (icon) - 16 (gap) - 40 (padding) |
| Message to informative gap | 6 pt          |
| Informative to accessory gap | 16 pt       |
| Accessory to buttons gap   | 20 pt         |

### Button Area

| Property                  | Value          |
|---------------------------|----------------|
| Button height              | 22 pt (regular control size) |
| Button min width           | 68 pt         |
| Button spacing             | 8 pt          |
| Button area padding right  | 20 pt         |
| Button area padding bottom | 20 pt         |

## Button Layout

### Two Buttons (Side by Side)

When there are exactly two buttons and both labels are short, they appear side by side:

```
                    [Cancel] [Default]
```

- Buttons are right-aligned
- Default button is rightmost
- Cancel button is left of default

### Three or More Buttons (Stacked or Side by Side)

```
          [Other]  [Cancel]  [Default]
```

If the combined button width exceeds the alert width, buttons stack vertically:

```
          [Default (full width)]
          [Cancel (full width)]
          [Other (full width)]
```

### Button Order

| Position          | Button Type                              |
|-------------------|------------------------------------------|
| Rightmost         | Default / primary action                 |
| Left of default   | Cancel / secondary action                |
| Leftmost          | Tertiary / alternative action            |
| Far left (bottom) | Help button (circular question mark)     |

## Typography

| Element              | Font Size (pt) | Weight     | Color                       |
|----------------------|----------------|------------|------------------------------|
| Message text         | 13             | Bold       | labelColor                   |
| Informative text     | 11             | Regular    | secondaryLabelColor          |
| Button text          | 13             | Regular    | Per button style             |
| Suppression checkbox | 11             | Regular    | labelColor                   |

## Colors

### Background

| Mode      | Color                          |
|-----------|--------------------------------|
| Light     | `#ECECEC` (window background)  |
| Dark      | `#323232` (window background)  |

When presented as a sheet, the alert background may use vibrancy from the parent window.

### Buttons

The default button uses accent color fill (see button.md):

| Button Type     | Background Light       | Background Dark        | Text Light | Text Dark  |
|-----------------|------------------------|------------------------|------------|------------|
| Default         | `#007AFF`              | `#0A84FF`              | `#FFFFFF`  | `#FFFFFF`  |
| Cancel          | Standard button fill   | Standard button fill   | labelColor | labelColor |
| Destructive     | `#FF3B30`              | `#FF453A`              | `#FFFFFF`  | `#FFFFFF`  |
| Other           | Standard button fill   | Standard button fill   | labelColor | labelColor |

## Shadow (Modal Dialog)

When displayed as a standalone modal (not sheet):

```
Color:   rgba(0, 0, 0, 0.30)
Offset:  (0, 8) pt
Blur:    40 pt
```

Plus a background dimming overlay on the window behind.

## Sheet Presentation

When displayed as a sheet (`beginSheetModal(for:)`):

| Property                  | Value               |
|---------------------------|---------------------|
| Animation                  | Slide down from title bar |
| Duration                   | 250 ms              |
| Curve                      | Ease In Out         |
| Parent window dimming      | Slight darkening    |
| Parent window interaction  | Blocked             |
| Dismissal animation        | Slide up            |
| Dismissal duration         | 200 ms              |

The sheet is attached to the window's title bar and drops down:

```
Window Title Bar
=================  <- attachment point
| Alert Sheet   |
| ...           |
| [Cancel] [OK] |
=================
```

## Suppression Checkbox

Optional checkbox at the bottom of the alert:

| Property                  | Value               |
|---------------------------|---------------------|
| Text                       | "Do not show this message again" (or custom) |
| Font size                  | 11 pt              |
| Position                   | Below informative text, above buttons |
| Gap above                  | 12 pt              |
| Gap below (to buttons)     | 16 pt              |

## Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Return / Enter  | Activate default button                    |
| Escape          | Activate cancel button (or close alert)    |
| Space           | Activate focused button                    |
| Tab             | Move focus between buttons                 |
| Cmd+.           | Cancel (equivalent to Escape)              |

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.dialog`                                 |
| Announced    | Message text + informative text            |
| Focus        | Default button on presentation             |

## Animation

| Transition                    | Duration (ms) | Curve          |
|-------------------------------|---------------|----------------|
| Modal dialog appear           | 200           | Ease Out       |
| Modal dialog dismiss          | 150           | Ease In        |
| Sheet slide down              | 250           | Ease In Out    |
| Sheet slide up (dismiss)      | 200           | Ease In Out    |
| Background dimming            | 200           | Ease In Out    |

## Dija Skin Mapping

```
comp! Alert {
    attr style, AlertStyle, default: AlertStyle::Informational
    attr message, &str, default: ""
    attr informative, &str, default: ""
    attr suppression, bool, default: false

    // macOS skin maps:
    // Width: 340 pt standard, up to 460 pt
    // Icon: 64x64, positioned top-left
    // Message: 13 pt bold
    // Informative: 11 pt regular, secondaryLabelColor
    // Buttons: right-aligned, default button accent-filled
    // Corner radius: 10 pt
    // Shadow: standard window shadow for modal
}
```
