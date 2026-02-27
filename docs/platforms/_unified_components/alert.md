# Alert

A modal dialog that interrupts the user to deliver critical information, request confirmation, or present a decision. Alerts block interaction with the underlying content until dismissed.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIAlertController (style: .alert) | Documented |
| macOS | NSAlert | Documented |
| Android | Dialog (Material Design 3) | Documented |
| Windows | ContentDialog | Documented |
| Linux | AdwAlertDialog | Documented |

## iOS

Source: UIAlertController, SwiftUI Alert

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | Ultra-thick material | Ultra-thick material |
| Corner radius | 14pt | 14pt |
| Corner curve | `.continuous` (superellipse) | |
| Width | 270pt (fixed on iPhone) | 270pt |
| Width (iPad) | 270pt (centered in screen) | 270pt |
| Shadow | offset(0, 10) blur 40, black @ 0.3 | offset(0, 10) blur 40, black @ 0.4 |

### Dimming Backdrop

| Property | Value |
|----------|-------|
| Overlay | black @ 0.4 |
| Animation | Fade in 0.2s, fade out 0.15s |
| Background interaction | Blocked (modal) |

### Layout

| Region | Value |
|--------|-------|
| Content padding (top) | 20pt |
| Content padding (horizontal) | 16pt |
| Title-to-message spacing | 3pt |
| Message-to-buttons spacing | 20pt |
| Content-to-text-field spacing | 8pt |
| Text field height | 26pt |
| Text field corner radius | 5pt |
| Text field border | 0.5pt separator color |

### Typography

| Element | Font | Size | Weight | Color | Alignment |
|---------|------|------|--------|-------|-----------|
| Title | SF Pro | 17pt | Semibold | label | Centered |
| Message | SF Pro | 13pt | Regular | secondaryLabel | Centered |
| Default action | SF Pro | 17pt | Semibold | tintColor | Centered |
| Cancel action | SF Pro | 17pt | Semibold | tintColor | Centered |
| Regular action | SF Pro | 17pt | Regular | tintColor | Centered |
| Destructive action | SF Pro | 17pt | Regular | systemRed | Centered |
| Preferred action | SF Pro | 17pt | Semibold | tintColor | Centered (bold emphasis) |

### Button Layout

#### 2 Buttons (Side by Side)

```
+---------------------------------+
|         Alert Title              |
|     This is the message          |
+----------------+----------------+
|    Cancel      |     OK         |  <- 44pt height each
+----------------+----------------+
```

| Property | Value |
|----------|-------|
| Button height | 44pt |
| Separator (horizontal) | 0.33pt, separator color |
| Separator (vertical) | 0.33pt, separator color |
| Layout | Left: cancel, Right: default/preferred |

#### 3+ Buttons (Stacked)

```
+---------------------------------+
|         Alert Title              |
|     This is the message          |
+---------------------------------+
|          Action 1                |
+---------------------------------+
|          Action 2                |
+---------------------------------+
|          Cancel                  |  <- always last
+---------------------------------+
```

| Property | Value |
|----------|-------|
| Each button | 44pt height, full width |
| Separator | 0.33pt horizontal between each |
| Cancel | Always last (bottom) |

### Button States

| State | Effect |
|-------|--------|
| Pressed | Background darkens slightly (gray highlight fill) |
| Disabled | Text alpha 0.3 |

### Text Fields in Alert

Alerts can contain 1-2 text fields (e.g., login prompt).

| Property | Value |
|----------|-------|
| Max text fields | 2 (username + password) |
| Position | Between message and buttons |
| Background | white (light) / `#1C1C1E` (dark) |
| Border | 0.5pt separator color |
| Corner radius | 5pt |
| Height | 26pt |
| Font | SF Pro Regular, 13pt |
| Horizontal padding | 8pt |

### Animation

#### Present

| Property | Value |
|----------|-------|
| Duration | 0.25s |
| Scale | Start at 1.2, spring to 1.0 |
| Opacity | Fade in from 0 to 1 |
| Backdrop | Fade in black @ 0.4 |
| Spring damping | ~0.75 |

#### Dismiss

| Property | Value |
|----------|-------|
| Duration | 0.2s |
| Scale | From 1.0 to 0.9 |
| Opacity | Fade out from 1 to 0 |
| Backdrop | Fade out |
| Curve | ease-in |

### Accessibility

| Property | Value |
|----------|-------|
| VoiceOver | "Alert, [title], [message]" |
| Focus | First action button (or preferred action) |
| Escape gesture | Triggers cancel action |

## macOS

Reference: NSAlert, NSPanel, Apple HIG (macOS 14+).

### Overview

`NSAlert` presents a modal dialog for critical information, error conditions, or confirmation requests. Alerts can be displayed as standalone modal dialogs or as sheets attached to a window.

### Alert Styles

#### NSAlert.Style

| Style              | Icon                                  | Usage                          |
|--------------------|---------------------------------------|--------------------------------|
| `.informational`   | App icon                              | General information            |
| `.warning`         | App icon with caution triangle        | Potentially destructive action |
| `.critical`        | App icon with red stop sign overlay   | Data loss, errors              |

### Layout

#### Dialog Structure

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

#### Dimensions

| Property                  | Value (pt)   | Notes                         |
|---------------------------|-------------|-------------------------------|
| Minimum width              | 260         |                               |
| Maximum width              | 460         | Expands for long text          |
| Standard width             | 340         | Most common alert width        |
| Corner radius              | 10          | Matches window radius          |
| Content padding (top)      | 20          |                               |
| Content padding (sides)    | 20          |                               |
| Content padding (bottom)   | 20          |                               |

#### Icon

| Property                  | Value          |
|---------------------------|----------------|
| Icon size                  | 64x64 pt      |
| Icon to text gap           | 16 pt         |
| Icon position              | Top-left       |
| Icon vertical alignment    | Top-aligned with message text |

#### Text Area

| Property                  | Value          |
|---------------------------|----------------|
| Text area width            | Alert width - 64 (icon) - 16 (gap) - 40 (padding) |
| Message to informative gap | 6 pt          |
| Informative to accessory gap | 16 pt       |
| Accessory to buttons gap   | 20 pt         |

#### Button Area

| Property                  | Value          |
|---------------------------|----------------|
| Button height              | 22 pt (regular control size) |
| Button min width           | 68 pt         |
| Button spacing             | 8 pt          |
| Button area padding right  | 20 pt         |
| Button area padding bottom | 20 pt         |

### Button Layout

#### Two Buttons (Side by Side)

When there are exactly two buttons and both labels are short, they appear side by side:

```
                    [Cancel] [Default]
```

- Buttons are right-aligned
- Default button is rightmost
- Cancel button is left of default

#### Three or More Buttons (Stacked or Side by Side)

```
          [Other]  [Cancel]  [Default]
```

If the combined button width exceeds the alert width, buttons stack vertically:

```
          [Default (full width)]
          [Cancel (full width)]
          [Other (full width)]
```

#### Button Order

| Position          | Button Type                              |
|-------------------|------------------------------------------|
| Rightmost         | Default / primary action                 |
| Left of default   | Cancel / secondary action                |
| Leftmost          | Tertiary / alternative action            |
| Far left (bottom) | Help button (circular question mark)     |

### Typography

| Element              | Font Size (pt) | Weight     | Color                       |
|----------------------|----------------|------------|------------------------------|
| Message text         | 13             | Bold       | labelColor                   |
| Informative text     | 11             | Regular    | secondaryLabelColor          |
| Button text          | 13             | Regular    | Per button style             |
| Suppression checkbox | 11             | Regular    | labelColor                   |

### Colors

#### Background

| Mode      | Color                          |
|-----------|--------------------------------|
| Light     | `#ECECEC` (window background)  |
| Dark      | `#323232` (window background)  |

When presented as a sheet, the alert background may use vibrancy from the parent window.

#### Buttons

The default button uses accent color fill (see button.md):

| Button Type     | Background Light       | Background Dark        | Text Light | Text Dark  |
|-----------------|------------------------|------------------------|------------|------------|
| Default         | `#007AFF`              | `#0A84FF`              | `#FFFFFF`  | `#FFFFFF`  |
| Cancel          | Standard button fill   | Standard button fill   | labelColor | labelColor |
| Destructive     | `#FF3B30`              | `#FF453A`              | `#FFFFFF`  | `#FFFFFF`  |
| Other           | Standard button fill   | Standard button fill   | labelColor | labelColor |

### Shadow (Modal Dialog)

When displayed as a standalone modal (not sheet):

```
Color:   rgba(0, 0, 0, 0.30)
Offset:  (0, 8) pt
Blur:    40 pt
```

Plus a background dimming overlay on the window behind.

### Sheet Presentation

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

### Suppression Checkbox

Optional checkbox at the bottom of the alert:

| Property                  | Value               |
|---------------------------|---------------------|
| Text                       | "Do not show this message again" (or custom) |
| Font size                  | 11 pt              |
| Position                   | Below informative text, above buttons |
| Gap above                  | 12 pt              |
| Gap below (to buttons)     | 16 pt              |

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Return / Enter  | Activate default button                    |
| Escape          | Activate cancel button (or close alert)    |
| Space           | Activate focused button                    |
| Tab             | Move focus between buttons                 |
| Cmd+.           | Cancel (equivalent to Escape)              |

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.dialog`                                 |
| Announced    | Message text + informative text            |
| Focus        | Default button on presentation             |

### Animation

| Transition                    | Duration (ms) | Curve          |
|-------------------------------|---------------|----------------|
| Modal dialog appear           | 200           | Ease Out       |
| Modal dialog dismiss          | 150           | Ease In        |
| Sheet slide down              | 250           | Ease In Out    |
| Sheet slide up (dismiss)      | 200           | Ease In Out    |
| Background dimming            | 200           | Ease In Out    |

### Dija Skin Mapping

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

## Android

Source: m3.material.io/components/dialogs/specs

M3 equivalent of iOS alert. Two types: basic dialog and full-screen dialog.

### Variants

| Variant | Usage | Dismissible |
|---------|-------|------------|
| Basic dialog | Confirmations, simple choices | Tap outside or cancel button |
| Full-screen dialog | Complex tasks (compose, edit) | Close/X button only |

### Basic Dialog Metrics

| Property | Value |
|----------|-------|
| Min width | 280dp |
| Max width | 560dp |
| Corner radius | 28dp (extra-large) |
| Surface | surfaceContainerHigh |
| Elevation | Level 3 (6dp) |
| Padding (all sides) | 24dp |
| Icon size (optional) | 24dp |
| Icon-to-headline gap | 16dp |
| Headline-to-body gap | 16dp |
| Body-to-actions gap | 24dp |
| Action button gap | 8dp |
| Headline font | Headline Small (Roboto Regular, 24sp) |
| Body font | Body Medium (Roboto Regular, 14sp) |
| Action font | Label Large (Roboto Medium, 14sp) |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainerHigh) | `#2B2930` |
| Icon | `#6750A4` (secondary) | `#D0BCFF` |
| Headline | `#1D1B20` (onSurface) | `#E6E0E9` |
| Body | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Action buttons | `#6750A4` (primary) | `#D0BCFF` |
| Scrim | `#000000` @ 32% | `#000000` @ 32% |

### Action Buttons

- Right-aligned, horizontally laid out
- Text buttons (no container)
- Confirming action on the right, dismissive on the left
- Max 2 action buttons for basic dialog

| Action | Example | Color |
|--------|---------|-------|
| Confirming | "Accept", "Save", "OK" | primary |
| Dismissive | "Cancel", "Dismiss" | primary |

### Full-Screen Dialog

| Property | Value |
|----------|-------|
| Corner radius | 0dp (fills screen) |
| Surface | surface |
| Top bar height | 56dp |
| Close icon | 24dp, onSurface |
| Title font | Title Large (Roboto Regular, 22sp) |
| Content padding | 24dp |
| Action button | Text button in top bar, right side |

### States

| State | Effect |
|-------|--------|
| Entering | Fade in + scale up from 85%, Medium 2 (300ms), Emphasized decelerate |
| Exiting | Fade out, Short 4 (200ms), Standard accelerate |
| Scrim | Fades in/out with dialog |

### Layout

#### Basic Dialog

```
+------------------------------------+
|  24dp padding                      |
|  [Icon] (optional, centered)       |
|  16dp gap                          |
|  Headline (centered if icon)       |
|  16dp gap                          |
|  Body text                         |
|  24dp gap                          |
|           [Cancel]  [Confirm]      |
|  24dp padding                      |
+------------------------------------+
        280-560dp width
        corner radius 28dp
```

#### With Divider

For dialogs with scrollable content, a 1dp divider (outlineVariant)
separates the header and footer from the scrollable body.

## Windows

Source: WinUI 3 ContentDialog control

### Appearance

- Background: SolidBackgroundFillColorQuarternary (`#FFFFFF` / `#2C2C2C`)
- Corner radius: 8px (layerCornerRadius)
- Border: 1px SurfaceStrokeColorDefault
- Shadow: Shadow 28
- Overlay: SmokeFillColorDefault (black @ 30% light, black @ 40% dark)

### Metrics

| Property | Value |
|----------|-------|
| Max width | 548px |
| Min width | 320px |
| Padding (content area) | 24px |
| Title padding | 24px left/right, 18px top |
| Button area padding | 24px horizontal, 20px bottom, 8px top |
| Button gap | 8px |
| Corner radius | 8px |

### Structure

```
+-------------------------------------+
| Title                               |  <- 20px Subtitle, SemiBold
|                                     |
| Content area                        |  <- 14px Body, Regular
| (text, custom content, inputs)      |
|                                     |
+-------------------------------------+
| [Close]  [Secondary]  [Primary]    |  <- Button row
+-------------------------------------+
```

### Title

| Property | Value |
|----------|-------|
| Font | 20px Subtitle, SemiBold (600) |
| Color | TextFillColorPrimary |
| Max lines | 2 (truncated with ellipsis) |
| Bottom margin | 12px (to content) |

### Content

| Property | Value |
|----------|-------|
| Font | 14px Body, Regular (400) |
| Color | TextFillColorSecondary |
| Scrollable | Yes, if content exceeds max height |
| Max height | Adapts to window height minus title and button areas |

### Buttons

ContentDialog supports up to 3 buttons: Primary, Secondary, and Close.

| Property | Primary | Secondary | Close |
|----------|---------|-----------|-------|
| Style | AccentButtonStyle (filled accent) | DefaultButtonStyle (standard) | DefaultButtonStyle (standard) |
| Min width | 130px each | 130px each | 130px each |
| Height | 32px | 32px | 32px |
| Corner radius | 4px | 4px | 4px |
| Position | Right-most | Center | Left-most |

Buttons are laid out right-to-left: Primary on the right, then Secondary, then Close on the left. They are equally distributed across the full width.

When `DefaultButton` is set to `Primary`, the primary button receives AccentButtonStyle.

#### Full-Width Buttons (Single Button)

When only one button is present, it spans the full width of the dialog.

#### Stacked Layout

If the combined button width exceeds available space, buttons stack vertically with Primary on top.

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Dialog open (scale + fade) | 300ms | Decelerate |
| Dialog close (scale + fade) | 200ms | Accelerate |
| Smoke overlay fade in | 300ms | Decelerate |
| Smoke overlay fade out | 200ms | Accelerate |

Open animation: starts at ~95% scale with 0 opacity, animates to 100% scale and full opacity.
Close animation: reverse, fading to 0 opacity with slight scale down.

### Position

- Always centered in the window, both horizontally and vertically.
- Cannot be moved or dragged.
- Uses `XamlRoot` as the placement anchor (renders within the app's XAML island).

### Behavior

| Behavior | Default |
|----------|---------|
| Light dismiss | No (modal, blocks interaction) |
| Escape key | Invokes CloseButton action |
| Enter key | Invokes DefaultButton action |
| Background interaction | Blocked (smoke overlay intercepts) |
| Multiple dialogs | Only one can be shown at a time |

## Linux

### Overview

`AdwAlertDialog` is a modal dialog for warnings, confirmations, and user decisions.
It replaces the deprecated `GtkMessageDialog` in modern GNOME apps.

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FAFAFA` (dialog_bg_color) | `#383838` |
| Text color | `#2E3436` | `#FFFFFF` |
| Corner radius | 12px | 12px |
| Shadow | (0, 12) blur 36, black @ 0.25 | (0, 12) blur 36, black @ 0.25 |
| Scrim (backdrop) | black @ 0.32 | black @ 0.32 |

### Layout

```
+----------------------------------+
|          [optional icon]         |
|                                  |
|        Title (centered)          |
|                                  |
|     Body text (centered,         |
|     multi-line wrapping)         |
|                                  |
|   [Extra child widget area]      |
|                                  |
+----------------------------------+
|  [Cancel]   |   [Destructive]    |
+----------------------------------+
```

### Metrics

| Property | Value |
|----------|-------|
| Max width | 480px |
| Min width | 300px |
| Content padding | 24px |
| Title-to-body gap | 8px |
| Body-to-buttons gap | 24px |
| Button area padding | 0px (buttons fill width) |
| Button separator | 1px `rgba(0,0,0, 0.15)` |
| Button height | 42px |

### Typography

| Element | Font | Weight | Size | Alignment |
|---------|------|--------|------|-----------|
| Title | Adwaita Sans | Bold | 18px (.title-3) | Center |
| Body | Adwaita Sans | Regular | 15px (.body) | Center |
| Button label | Adwaita Sans | Regular | 15px | Center |
| Suggested button label | Adwaita Sans | Bold | 15px | Center |

### Button Layout

Buttons are placed in a horizontal row at the bottom, separated by 1px borders.
For 2 buttons, they split 50/50 width. For 3+, they stack vertically.

#### Horizontal Layout (2 buttons)

```
+------------------+---+------------------+
|     Cancel       | | | Suggested/Action |
+------------------+---+------------------+
```

#### Vertical Layout (3+ buttons)

```
+------------------------------------+
|          Primary Action            |
+------------------------------------+
|          Secondary Action          |
+------------------------------------+
|            Cancel                  |
+------------------------------------+
```

### Button Styles

| Style | Background | Text Color | Usage |
|-------|-----------|------------|-------|
| Default | transparent | `--window-fg-color` | Cancel, dismiss |
| Suggested | transparent | `--accent-color` | Confirm, save |
| Destructive | transparent | `--destructive-color` | Delete, discard |

Note: Unlike standalone buttons, dialog buttons are **flat** (no background fill).
The accent/destructive color is applied to the text only.

#### Button States (within dialog)

| State | Effect |
|-------|--------|
| Rest | Flat, text color only |
| Hover | `rgba(0,0,0, 0.04)` background |
| Active | `rgba(0,0,0, 0.08)` background |
| Focused | 2px accent outline (inset) |

### Response Types

| Response | Appearance | Keyboard |
|----------|-----------|----------|
| Default | Regular text | -- |
| Suggested | Accent-colored text, bold | Enter activates |
| Destructive | Red text | -- |
| Close | Hidden (dialog close) | Escape activates |

### Focus Behavior

| Property | Value |
|----------|-------|
| Initial focus | Suggested action button (if set) |
| Tab order | Buttons left-to-right, then content |
| Escape | Closes dialog (fires close response) |
| Enter | Activates default/suggested response |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Appear (scale + fade) | 250ms | ease-out-cubic |
| Dismiss (fade) | 200ms | ease-in-cubic |
| Scrim fade in | 250ms | ease-out |
| Scrim fade out | 200ms | ease-in |

#### Appear Animation

```
Start:  scale(0.95), opacity(0)
End:    scale(1.0),  opacity(1.0)
```

#### Dismiss Animation

```
Start:  scale(1.0),  opacity(1.0)
End:    scale(0.95), opacity(0)
```
