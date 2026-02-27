# Button

An interactive control that triggers an action when activated. Buttons come in multiple visual variants (filled, outlined, text-only, destructive) and sizes to convey hierarchy and emphasis.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIButton | Documented |
| macOS | NSButton | Documented |
| Android | Button (Material Design 3) | Documented |
| Windows | Button / ToggleButton / HyperlinkButton | Documented |
| Linux | GtkButton | Documented |

## iOS

Source: UIButton (iOS 15+ button configuration system)

### Variants

| Style | Background (Light) | Background (Dark) | Text Color | Border |
|-------|-------------------|-------------------|------------|--------|
| Plain | transparent | transparent | tintColor | none |
| Gray | tintColor @ 0.12 | tintColor @ 0.24 | tintColor | none |
| Tinted | tintColor @ 0.15 | tintColor @ 0.25 | tintColor | none |
| Filled | tintColor | tintColor | white | none |
| Bordered (prominent) | transparent | transparent | tintColor | 1pt tintColor |
| Bordered (tinted) | transparent | transparent | tintColor | 1pt tintColor @ 0.3 |

### Sizes

| Size | Height | Horizontal Padding | Font Size | Corner Radius |
|------|--------|-------------------|-----------|---------------|
| Mini | 28pt | 10pt | 15pt | 7pt |
| Small | 32pt | 12pt | 15pt | 8pt |
| Medium | 36pt | 14pt | 17pt | 10pt |
| Large | 50pt | 20pt | 17pt | 12pt |

Note: All sizes maintain a minimum hit target of 44x44pt. Smaller visual sizes have expanded touch areas.

### Metrics

| Property | Value |
|----------|-------|
| Corner radius (default) | 10pt (continuous/squircle) |
| Corner curve | `.continuous` (superellipse) |
| Font | SF Pro Semibold (title), SF Pro Regular (subtitle) |
| Default font size | 17pt |
| Image-to-title padding | 8pt |
| Content insets (default) | 7pt vertical, 14pt horizontal |
| Shadow | None |
| Icon size (symbol) | Matches font size (point-size based) |

### Button with Subtitle

iOS 15+ supports a subtitle below the title.

| Property | Value |
|----------|-------|
| Title font | SF Pro Semibold, 17pt |
| Subtitle font | SF Pro Regular, 12pt |
| Subtitle color | secondaryLabel |
| Vertical spacing | 2pt between title and subtitle |
| Layout | Center-aligned (default), leading, trailing |

### States

| State | Effect (Plain) | Effect (Filled) | Effect (Gray/Tinted) |
|-------|---------------|-----------------|---------------------|
| Normal | tintColor text | tintColor bg, white text | tinted bg, tintColor text |
| Highlighted (pressed) | alpha 0.3 on text | darken bg ~20% | darken bg ~15% |
| Disabled | alpha 0.3 | alpha 0.3 (entire button) | alpha 0.3 |
| Focused (tvOS/keyboard) | slight scale 1.05 | slight scale 1.05 | slight scale 1.05 |
| Selected | same as normal (no toggle visual by default) | -- | -- |

#### Press Animation

| Property | Value |
|----------|-------|
| Highlight transition | immediate (no animation) |
| Release transition | 0.15s fade back |
| Scale (if used) | 0.97 on press, spring back 0.3s |

### Menu Button

Buttons can host a pull-down menu (iOS 14+) or pop-up menu.

| Property | Value |
|----------|-------|
| Menu indicator | Downward chevron (SF Symbol: `chevron.down`) |
| Indicator size | ~8pt, slightly below center |
| Indicator color | Same as title color, reduced opacity |
| Long-press to show | ~0.3s hold |
| Instant tap shows menu | When `showsMenuAsPrimaryAction = true` |

### Activity Indicator Button

| Property | Value |
|----------|-------|
| Indicator style | `.medium` UIActivityIndicatorView |
| Indicator replaces | Image or title (configurable) |
| Indicator color | Same as text color |

### Destructive Style

| Property | Value |
|----------|-------|
| Filled destructive bg | systemRed |
| Tinted destructive bg | systemRed @ 0.15 |
| Text color | systemRed (plain/tinted), white (filled) |

## macOS

Reference: NSButton, NSButton.BezelStyle, NSButton.ButtonType, Apple HIG (macOS 14+).

### Overview

macOS buttons come in many bezel styles and types. The primary push button is the most common. All buttons support four control sizes (mini, small, regular, large) since macOS 11.

### Bezel Styles

#### NSButton.BezelStyle Enum

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

#### Deprecated Bezel Styles

| Style                  | Raw | Replacement                   |
|------------------------|-----|-------------------------------|
| `.rounded`             | 1   | Use `.push`                   |
| `.regularSquare`       | 2   | Use `.flexiblePush`           |
| `.texturedSquare`      | 8   | Use `.toolbar`                |
| `.texturedRounded`     | 11  | Use `.toolbar`                |
| `.recessed`            | 13  | Use `.accessoryBarAction`     |
| `.roundRect`           | 14  | Use `.accessoryBar`           |
| `.inline`              | 15  | Use `.accessoryBar`           |

### Button Types

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

### Metrics

#### Push Button (`.push`)

| Control Size | Height (pt) | Min Width (pt) | Corner Radius (pt) | Font Size (pt) | Font Weight  |
|-------------|-------------|----------------|---------------------|----------------|-------------|
| Mini        | 16          | 26             | 3                   | 9              | Regular     |
| Small       | 19          | 32             | 4                   | 11             | Regular     |
| Regular     | 22          | 48             | 6                   | 13             | Regular     |
| Large       | 28          | 48             | 8                   | 15             | Regular     |

#### Horizontal Padding (text to edge)

| Control Size | Horizontal Padding (pt) |
|-------------|------------------------|
| Mini        | 6                      |
| Small       | 8                      |
| Regular     | 12                     |
| Large       | 16                     |

#### Icon Button (`.circular`)

| Control Size | Diameter (pt) | Icon Size (pt) |
|-------------|---------------|----------------|
| Mini        | 16            | 10             |
| Small       | 20            | 13             |
| Regular     | 26            | 16             |
| Large       | 32            | 20             |

#### Toolbar Button (`.toolbar`)

| Control Size | Height (pt) | Corner Radius (pt) | Notes                          |
|-------------|-------------|---------------------|--------------------------------|
| Regular     | 24          | 6                   | Default for toolbars           |
| Small       | 20          | 4                   | Compact toolbars               |

### Colors

#### Push Button (Default)

| State      | Background Light           | Background Dark             | Text Light    | Text Dark     |
|------------|----------------------------|-----------------------------|---------------|---------------|
| Normal     | White gradient (#FFFFFF to #F5F5F5) | `rgba(255,255,255,0.10)` | `#262626`     | `#E5E5E5`    |
| Hover      | White gradient (#FFFFFF to #F0F0F0) | `rgba(255,255,255,0.14)` | `#262626`     | `#E5E5E5`    |
| Pressed    | `#DCDCDC`                  | `rgba(255,255,255,0.06)`   | `#262626`     | `#E5E5E5`    |
| Disabled   | `rgba(0,0,0,0.04)`        | `rgba(255,255,255,0.04)`   | `rgba(0,0,0,0.25)` | `rgba(255,255,255,0.25)` |

#### Push Button (Default / Primary / Accent)

The window's default button uses the accent color fill:

| State      | Background Light       | Background Dark        | Text Light | Text Dark  |
|------------|------------------------|------------------------|------------|------------|
| Normal     | `#007AFF`              | `#0A84FF`              | `#FFFFFF`  | `#FFFFFF`  |
| Hover      | `#0071EB`              | `#0C7AEF`              | `#FFFFFF`  | `#FFFFFF`  |
| Pressed    | `#0062CC`              | `#0068C4`              | `#FFFFFF`  | `#FFFFFF`  |
| Disabled   | `rgba(0,122,255,0.40)` | `rgba(10,132,255,0.40)`| `rgba(255,255,255,0.50)` | `rgba(255,255,255,0.50)` |

#### Destructive Button

| State      | Background Light       | Background Dark        | Text Light | Text Dark  |
|------------|------------------------|------------------------|------------|------------|
| Normal     | `#FF3B30`              | `#FF453A`              | `#FFFFFF`  | `#FFFFFF`  |
| Hover      | `#E6352B`              | `#E63F35`              | `#FFFFFF`  | `#FFFFFF`  |
| Pressed    | `#CC2F26`              | `#CC3830`              | `#FFFFFF`  | `#FFFFFF`  |

#### Toolbar Button (`.toolbar`)

| State      | Background Light         | Background Dark            |
|------------|--------------------------|----------------------------|
| Normal     | Transparent              | Transparent                |
| Hover      | `rgba(0,0,0,0.06)`      | `rgba(255,255,255,0.08)`   |
| Pressed    | `rgba(0,0,0,0.10)`      | `rgba(255,255,255,0.12)`   |
| Selected   | `rgba(0,0,0,0.08)`      | `rgba(255,255,255,0.10)`   |

### Border

Standard push buttons have a 0.5 pt border:

| State      | Border Light              | Border Dark                  |
|------------|---------------------------|------------------------------|
| Normal     | `rgba(0,0,0,0.12)`       | `rgba(255,255,255,0.12)`     |
| Focused    | `rgba(0,122,255,0.50)` (focus ring) | `rgba(10,132,255,0.50)` |
| Disabled   | `rgba(0,0,0,0.06)`       | `rgba(255,255,255,0.06)`     |

### Shadow

Normal push button shadow:

```
Color:   rgba(0, 0, 0, 0.06)
Offset:  (0, 0.5)
Blur:    1.5 pt
```

Pressed state removes the shadow.

### States

| State        | Visual Changes                                         |
|--------------|--------------------------------------------------------|
| Normal       | Default appearance with subtle shadow                  |
| Hover        | Slightly brighter/darker background                    |
| Pressed      | Inset appearance, no shadow, darker fill               |
| Focused      | Focus ring (3 pt accent-colored ring, 2 pt offset)     |
| Disabled     | 40% opacity on fill, 25% opacity on text               |
| Default      | Blue/accent fill, pulsing animation (legacy, now static)|
| On (toggle)  | Accent color tint for selected state                   |

### Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Hover in            | 50            | Ease Out      |
| Hover out           | 150           | Ease In Out   |
| Press               | 30            | Ease Out      |
| Release             | 100           | Ease Out      |
| Disable/Enable      | 200           | Ease In Out   |

### Checkbox (`.switch` type)

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

### Radio Button (`.radio` type)

| Control Size | Outer Diameter (pt) | Inner Dot Diameter (pt) |
|-------------|---------------------|------------------------|
| Mini        | 10                  | 4                      |
| Small       | 12                  | 5                      |
| Regular     | 16                  | 6                      |
| Large       | 20                  | 8                      |

### Keyboard Shortcuts

| Action          | Key                        |
|-----------------|----------------------------|
| Activate button | Space / Return (if default)|
| Cancel          | Escape (Cancel button)     |
| Toggle checkbox | Space                      |
| Tab to next     | Tab                        |
| Tab to previous | Shift+Tab                  |

### Dija Skin Mapping

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

## Android

Source: m3.material.io/components/buttons/specs

### Variants

| Variant | Container | Border | Elevation | Usage |
|---------|-----------|--------|-----------|-------|
| Filled | primary | none | Level 0 (0dp) | Highest emphasis, final actions (Save, Confirm) |
| Filled tonal | secondaryContainer | none | Level 0 (0dp) | Medium-high emphasis (Next, Open) |
| Elevated | surfaceContainerLow | none | Level 1 (1dp) | Medium emphasis on patterned backgrounds |
| Outlined | transparent | outline 1dp | Level 0 (0dp) | Medium emphasis (Back, Cancel) |
| Text | transparent | none | Level 0 (0dp) | Lowest emphasis (Learn more, Skip) |

### Metrics

| Property | Value |
|----------|-------|
| Height | 40dp |
| Min width | 48dp |
| Corner radius | 20dp (full pill) |
| Horizontal padding | 24dp |
| Horizontal padding (with icon) | 16dp (start), 24dp (end) |
| Icon size | 18dp |
| Icon-label gap | 8dp |
| Label font | Label Large (Roboto Medium 500, 14sp) |

### Colors

#### Filled Button

| Element | Light | Dark |
|---------|-------|------|
| Container | `#6750A4` (primary) | `#D0BCFF` (primary) |
| Label | `#FFFFFF` (onPrimary) | `#381E72` (onPrimary) |

#### Filled Tonal Button

| Element | Light | Dark |
|---------|-------|------|
| Container | `#E8DEF8` (secondaryContainer) | `#4A4458` (secondaryContainer) |
| Label | `#1D192B` (onSecondaryContainer) | `#E8DEF8` (onSecondaryContainer) |

#### Elevated Button

| Element | Light | Dark |
|---------|-------|------|
| Container | `#F7F2FA` (surfaceContainerLow) | `#1D1B20` (surfaceContainerLow) |
| Label | `#6750A4` (primary) | `#D0BCFF` (primary) |
| Shadow | Level 1 (1dp) | Level 1 (1dp) |

#### Outlined Button

| Element | Light | Dark |
|---------|-------|------|
| Container | transparent | transparent |
| Border | `#79747E` (outline) | `#938F99` (outline) |
| Label | `#6750A4` (primary) | `#D0BCFF` (primary) |

#### Text Button

| Element | Light | Dark |
|---------|-------|------|
| Container | transparent | transparent |
| Label | `#6750A4` (primary) | `#D0BCFF` (primary) |

### States

State layer uses the label/content color at varying opacity:

| State | Container effect | Label effect |
|-------|-----------------|-------------|
| Enabled | Default | Default |
| Hovered | + state layer 8% | Default |
| Focused | + state layer 10% | Default |
| Pressed | + state layer 10% + ripple | Default |
| Disabled | onSurface @ 12% | onSurface @ 38% |

#### Elevated button states

| State | Elevation |
|-------|-----------|
| Enabled | Level 1 (1dp) |
| Hovered | Level 2 (3dp) |
| Focused | Level 1 (1dp) |
| Pressed | Level 1 (1dp) |
| Disabled | Level 0 (0dp) |

### Icon Buttons

Separate from common buttons. Four variants: standard, filled, filled tonal, outlined.

| Property | Value |
|----------|-------|
| Container size | 40dp x 40dp |
| Icon size | 24dp |
| Corner radius | 20dp (full) |
| Touch target | 48dp x 48dp |

## Windows

Source: WinUI 3 Button, ToggleButton, HyperlinkButton

### Variants

| Style | Background (rest) | Foreground | Border |
|-------|-------------------|-----------|--------|
| Standard (Default) | ControlFillColorDefault (`#B3FFFFFF` / `#0FFFFFFF`) | TextFillColorPrimary | ControlStrokeColorDefault (1px) + bottom ControlStrokeColorSecondary |
| Accent | AccentFillColorDefault (SystemAccentColor) | TextOnAccentFillColorPrimary (white/black) | ControlStrokeColorOnAccentDefault (1px) + bottom ControlStrokeColorOnAccentSecondary |
| Subtle | Transparent | TextFillColorPrimary | None |
| Toggle (off) | Same as Standard | TextFillColorPrimary | Same as Standard |
| Toggle (on) | Same as Accent | TextOnAccentFillColorPrimary | Same as Accent |
| Hyperlink | Transparent | AccentTextFillColorPrimary | None, underline on hover |

### Metrics

| Property | Value |
|----------|-------|
| Min height | 32px |
| Min width | 120px (for dialog buttons), no global min |
| Padding | 11px left, 5px top, 11px right, 6px bottom |
| Corner radius | 4px (controlCornerRadius) |
| Font | Segoe UI Variable, 14px, SemiBold (600) |
| Icon size (when present) | 16x16px |
| Icon-to-text gap | 8px |
| Border | 1px top/sides + subtle bottom gradient stroke |

The asymmetric vertical padding (5px top, 6px bottom) accounts for optical centering of text with the bottom border accent.

### States

#### Standard Button

| State | Background | Border | Text |
|-------|-----------|--------|------|
| Rest | ControlFillColorDefault | ControlStrokeColorDefault | TextFillColorPrimary |
| Hover | ControlFillColorSecondary | ControlStrokeColorDefault | TextFillColorPrimary |
| Pressed | ControlFillColorTertiary | ControlStrokeColorDefault | TextFillColorSecondary |
| Disabled | ControlFillColorDisabled | ControlStrokeColorDefault (reduced) | TextFillColorDisabled |
| Focused | Rest appearance + dual focus ring | FocusStrokeColorOuter (2px) + FocusStrokeColorInner (1px) | -- |

#### Accent Button

| State | Background | Border | Text |
|-------|-----------|--------|------|
| Rest | AccentFillColorDefault | ControlStrokeColorOnAccentDefault | TextOnAccentFillColorPrimary |
| Hover | AccentFillColorSecondary | ControlStrokeColorOnAccentDefault | TextOnAccentFillColorPrimary |
| Pressed | AccentFillColorTertiary | ControlStrokeColorOnAccentTertiary | TextOnAccentFillColorSecondary |
| Disabled | AccentFillColorDisabled | transparent | TextOnAccentFillColorDisabled |

#### Subtle Button

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |
| Disabled | Transparent | TextFillColorDisabled |

#### Hyperlink Button

| State | Text | Decoration |
|-------|------|-----------|
| Rest | AccentTextFillColorPrimary | None |
| Hover | AccentTextFillColorSecondary | Underline |
| Pressed | AccentTextFillColorTertiary | None |
| Disabled | AccentTextFillColorDisabled | None |

### Bottom Border Effect

Standard and Accent buttons have a subtle gradient border effect: the bottom edge of the border is slightly darker than the top/sides. This creates a subtle 3D "shelf" appearance.

- Top/sides border: `ControlStrokeColorDefault` (light: `#0F000000`, dark: `#12FFFFFF`)
- Bottom border: `ControlStrokeColorSecondary` (light: `#29000000`, dark: `#18FFFFFF`)

For Accent buttons, the bottom border uses `ControlStrokeColorOnAccentSecondary`.

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Rest -> Hover (fill) | 100ms | Control fast |
| Hover -> Pressed (fill) | 50ms | Linear |
| Pressed -> Rest (fill) | 200ms | Decelerate |
| Focus ring appear | 100ms | Control fast |

### Compact Mode

When `Compact` density is applied:
- Height: 24px
- Padding: 11px horizontal, 1px vertical
- Font size remains 14px

## Linux

### Variants

| Style Class | Background (Light) | Background (Dark) | Border | Shadow |
|-------------|-------------------|-------------------|--------|--------|
| Default (raised) | `#FFFFFF` | `#404040` | 1px, `rgba(0,0,0,0.15)` | (0,1) blur 2, black @ 0.07 |
| `.flat` | transparent | transparent | none | none |
| `.suggested-action` | `#3584E4` (accent) | `#3584E4` | none | (0,1) blur 2, black @ 0.07 |
| `.destructive-action` | `#E01B24` (red_3) | `#C01C28` (red_4) | none | (0,1) blur 2, black @ 0.07 |
| `.opaque` | custom (user-defined) | custom | none | (0,1) blur 2, black @ 0.07 |
| `.circular` | same as raised | same as raised | same | same |
| `.pill` | same as raised | same as raised | same | same |

### Shapes

| Style Class | Corner Radius | Aspect Ratio |
|-------------|--------------|--------------|
| Default | 6px | Rectangle, width follows content |
| `.circular` | 9999px (fully round) | Square (1:1), for icons or 1-2 chars |
| `.pill` | 9999px (fully round) | Rectangle, width follows content |

### Metrics

| Property | Value |
|----------|-------|
| Min height | 34px |
| Horizontal padding | 16px |
| Vertical padding | 8px |
| Corner radius | 6px |
| Font | Adwaita Sans Regular, 15px |
| Icon size | 16x16px |
| Icon + label gap | 6px |
| Border width | 1px |
| Circular min size | 34x34px |

### States

#### Default (Raised) Button

| State | Background (Light) | Background (Dark) | Shadow |
|-------|-------------------|-------------------|--------|
| Rest | `#FFFFFF` | `#404040` | (0,1) blur 2, black @ 0.07 |
| Hover | `#F5F5F5` | `#4A4A4A` | (0,1) blur 3, black @ 0.09 |
| Active (pressed) | `#DEDDDA` | `#353535` | inset (0,1) blur 2, black @ 0.07 |
| Focused | rest + 2px accent outline | rest + 2px accent outline | -- |
| Disabled | rest, opacity 0.5 | rest, opacity 0.5 | -- |

#### Flat Button

| State | Background (Light) | Background (Dark) |
|-------|-------------------|-------------------|
| Rest | transparent | transparent |
| Hover | `rgba(0,0,0, 0.07)` | `rgba(255,255,255, 0.07)` |
| Active | `rgba(0,0,0, 0.12)` | `rgba(255,255,255, 0.12)` |
| Focused | transparent + 2px accent outline | transparent + 2px accent outline |
| Disabled | transparent, content opacity 0.5 | transparent, content opacity 0.5 |

#### Suggested Action Button

| State | Background | Text Color |
|-------|-----------|------------|
| Rest | `#3584E4` | `#FFFFFF` |
| Hover | `#4A95EB` (lighter) | `#FFFFFF` |
| Active | `#2B6CBF` (darker) | `#FFFFFF` |
| Focused | rest + 2px accent outline, 2px offset | `#FFFFFF` |
| Disabled | `#3584E4`, opacity 0.5 | `#FFFFFF` |

#### Destructive Action Button

| State | Background | Text Color |
|-------|-----------|------------|
| Rest | `#E01B24` | `#FFFFFF` |
| Hover | `#E84049` (lighter) | `#FFFFFF` |
| Active | `#BF1720` (darker) | `#FFFFFF` |
| Focused | rest + 2px outline | `#FFFFFF` |
| Disabled | rest, opacity 0.5 | `#FFFFFF` |

### Linked Groups

When buttons are placed in a linked group (e.g., segmented controls, toggle groups),
they share borders and lose inner corner radii:

| Property | Value |
|----------|-------|
| Group corner radius | 6px (outer corners only) |
| Inner corners | 0px |
| Gap between buttons | 0px (borders collapse) |
| Inner border | 1px separator |

### Icon Buttons

| Property | Value |
|----------|-------|
| Size (square) | 34x34px |
| Icon size | 16x16px |
| Padding | 9px all sides |
| Common usage | Header bar actions, toolbar buttons |

### Keyboard Support

| Key | Action |
|-----|--------|
| Space / Enter | Activate button |
| Tab | Move focus to next |
| Shift+Tab | Move focus to previous |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Background color change | 200ms | ease-in-out |
| Shadow transition | 200ms | ease-in-out |
| Active (press) | immediate (no delay) | -- |

### Dija Skin Mapping

```
skin! {
    ButtonSkin {
        field main
        field label

        platform linux {
            light {
                main: {
                    min_height: 34,
                    padding: 8 16,
                    border_radius: 6,
                    background: #FFFFFF,
                    border: 1 rgba(0,0,0,0.15),
                    shadow: 0 1 2 0 rgba(0,0,0,0.07),
                }
                label: {
                    font_size: 15,
                    color: #2E3436,
                }
            }
            dark {
                main: {
                    background: #404040,
                    border: 1 rgba(255,255,255,0.15),
                }
                label: {
                    color: #FFFFFF,
                }
            }
        }
    }
}
```
