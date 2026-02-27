# Segmented Control

A horizontal group of mutually exclusive (or independently selectable) segments used for switching views, filtering content, or toggling between related options.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UISegmentedControl | Documented |
| macOS | NSSegmentedControl | Documented |
| Android | Segmented Button (Material Design 3) | Documented |
| Windows | RadioButtons / SegmentedControl (ToggleButtons) | Documented |
| Linux | GtkToggleButton Linked Group | Documented |

## iOS

Source: UISegmentedControl

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | systemGray6 (`#F2F2F7`) | `#1C1C1E` (elevated: `#2C2C2E`) |
| Corner radius (outer) | 9pt | 9pt |
| Corner curve | `.continuous` (superellipse) | |
| Height | 32pt | 32pt |
| Border | None (flat fill) | None |

### Segments

| Property | Value |
|----------|-------|
| Font | SF Pro Medium, 13pt |
| Text color (unselected) | label (`#000000` / `#FFFFFF`) |
| Text color (selected) | label (`#000000` / `#FFFFFF`) |
| Separator | 1pt wide, systemGray4 between unselected segments |
| Separator height | ~20pt (centered vertically, shorter than full height) |
| Horizontal padding | 12pt per segment (minimum) |
| Segment width | Equal distribution or intrinsic content size |

### Selected Segment Indicator

The selected segment floats as a rounded rect "pill" above the background.

| Property | Light | Dark |
|----------|-------|------|
| Fill | white (`#FFFFFF`) | systemGray3 (`#48484A`) |
| Corner radius | 7pt | 7pt |
| Corner curve | `.continuous` (superellipse) | |
| Inset from outer edge | 2pt (each side) | 2pt |
| Shadow 1 | offset(0, 3) blur 8, black @ 0.12 | offset(0, 3) blur 8, black @ 0.24 |
| Shadow 2 | offset(0, 3) blur 1, black @ 0.04 | offset(0, 3) blur 1, black @ 0.08 |

### States

| State | Effect |
|-------|--------|
| Normal (unselected) | Standard text on background |
| Selected | Floating pill indicator, shadows |
| Pressed (unselected) | Darken segment background ~10% |
| Pressed (selected) | Slightly darker pill |
| Disabled | Alpha 0.3 on entire control |
| Disabled (selected) | Selected pill visible but at reduced contrast |

### Animation

| Property | Value |
|----------|-------|
| Selection change | 0.3s spring animation |
| Spring damping | 0.75 |
| Pill slides | Horizontally to new position |
| Text crossfade | None (text stays in place, pill moves behind) |
| Separator fade | Adjacent separators fade out as pill approaches |

#### Animation Sequence (Segment A -> Segment B)

1. User taps segment B
2. Selected pill begins sliding from A to B (spring, 0.3s)
3. Separators adjacent to A fade in, separators adjacent to B fade out
4. Pill arrives at B position

### Metrics (Summary)

```
+---------------------------------------------+  <- outer: 9pt radius
| +---------+ | +---------+ | +---------+    |
| | Segment | | | SELECTED| | | Segment |    |  <- 32pt height
| |   One   | | |   Two   | | |  Three  |    |
| +---------+ | +---------+ | +---------+    |  <- inner: 7pt radius
+---------------------------------------------+
              ^ separators (1pt, gray4)
  <-- 2pt -->   <- pill inset from edges
```

### Accessibility

| Property | Value |
|----------|-------|
| Role | Segmented control (tab-like) |
| Each segment | Button with "selected" trait when active |
| VoiceOver | "[Label], button, [N] of [total]" |

## macOS

Reference: NSSegmentedControl, NSSegmentedControl.Style, Apple HIG (macOS 14+).

### Overview

`NSSegmentedControl` displays a horizontal group of mutually exclusive (or independently selectable) segments. It is used for switching views, filtering content, or grouping related actions.

### Styles

#### NSSegmentedControl.Style

| Style                | Description                                               | Usage                       |
|----------------------|-----------------------------------------------------------|-----------------------------|
| `.automatic`         | System picks based on context                              | Default                     |
| `.rounded`           | Rounded rect segments with visible borders                 | Window body, toolbars       |
| `.texturedRounded`   | Flatter, toolbar-appropriate appearance (deprecated name)  | Toolbars                    |
| `.capsule`           | Pill-shaped with a sliding selection indicator              | Tab-like switching          |
| `.smallSquare`       | Compact square segments                                    | Tight spaces, palettes      |
| `.separated`         | Individual rounded-rect buttons with gaps between them     | Discrete actions            |

#### Tracking Modes

| Mode                  | Description                                          |
|-----------------------|------------------------------------------------------|
| `.selectOne`          | Only one segment selected at a time (radio behavior) |
| `.selectAny`          | Any combination can be selected (checkbox behavior)  |
| `.momentary`          | Segments act as momentary push buttons               |

### Metrics

#### Rounded Style (`.rounded`)

| Control Size | Height (pt) | Segment Min Width (pt) | Corner Radius (pt) | Divider Width (pt) | Font Size (pt) |
|-------------|-------------|------------------------|---------------------|---------------------|----------------|
| Mini        | 16          | 20                     | 3                   | 1                   | 9              |
| Small       | 19          | 24                     | 4                   | 1                   | 11             |
| Regular     | 22          | 28                     | 5                   | 1                   | 13             |
| Large       | 28          | 34                     | 7                   | 1                   | 15             |

#### Capsule Style (`.capsule`)

| Control Size | Height (pt) | Segment Min Width (pt) | Corner Radius (pt) | Font Size (pt) |
|-------------|-------------|------------------------|---------------------|----------------|
| Mini        | 16          | 20                     | 8 (capsule)         | 9              |
| Small       | 19          | 24                     | 9.5 (capsule)       | 11             |
| Regular     | 22          | 28                     | 11 (capsule)        | 13             |
| Large       | 28          | 34                     | 14 (capsule)        | 15             |

The capsule style has a sliding pill indicator behind the selected segment.

#### Separated Style (`.separated`)

| Control Size | Height (pt) | Segment Min Width (pt) | Corner Radius (pt) | Gap Between (pt) | Font Size (pt) |
|-------------|-------------|------------------------|---------------------|-------------------|----------------|
| Mini        | 16          | 20                     | 3                   | 2                 | 9              |
| Small       | 19          | 24                     | 4                   | 2                 | 11             |
| Regular     | 22          | 28                     | 6                   | 4                 | 13             |
| Large       | 28          | 34                     | 8                   | 4                 | 15             |

#### Padding

| Control Size | Horizontal Padding per Segment (pt) | Icon-to-Label Gap (pt) |
|-------------|--------------------------------------|------------------------|
| Mini        | 4                                    | 2                      |
| Small       | 6                                    | 3                      |
| Regular     | 8                                    | 4                      |
| Large       | 12                                   | 5                      |

### Colors

#### Rounded Style

| Element                  | Light Mode                    | Dark Mode                      |
|--------------------------|-------------------------------|--------------------------------|
| Background               | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Selected segment bg      | `#FFFFFF`                     | `rgba(255,255,255,0.18)`       |
| Selected segment shadow   | `rgba(0,0,0,0.06)` offset 0,0.5 blur 1 | `rgba(0,0,0,0.20)` offset 0,0.5 blur 1 |
| Divider                  | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.10)`       |
| Text (normal)            | labelColor                    | labelColor                     |
| Text (selected)          | labelColor                    | labelColor                     |
| Text (disabled)          | disabledControlTextColor      | disabledControlTextColor       |

#### Capsule Style

| Element                  | Light Mode                    | Dark Mode                      |
|--------------------------|-------------------------------|--------------------------------|
| Track background         | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Selected pill bg         | `#FFFFFF`                     | `rgba(255,255,255,0.20)`       |
| Selected pill shadow      | `rgba(0,0,0,0.08)` offset 0,1 blur 2 | `rgba(0,0,0,0.25)` offset 0,1 blur 2 |
| Text (normal)            | secondaryLabelColor           | secondaryLabelColor            |
| Text (selected)          | labelColor                    | labelColor                     |

#### Separated Style

| Element                  | Light Mode                    | Dark Mode                      |
|--------------------------|-------------------------------|--------------------------------|
| Segment background       | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Segment hover            | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.12)`       |
| Segment selected         | controlAccentColor            | controlAccentColor             |
| Segment selected text    | `#FFFFFF`                     | `#FFFFFF`                      |
| Segment pressed          | `rgba(0,0,0,0.14)`           | `rgba(255,255,255,0.16)`       |

#### Border

| Style      | Border Light              | Border Dark                  |
|------------|---------------------------|------------------------------|
| Rounded    | `rgba(0,0,0,0.12)`       | `rgba(255,255,255,0.10)`     |
| Capsule    | `rgba(0,0,0,0.08)`       | `rgba(255,255,255,0.08)`     |
| Separated  | `rgba(0,0,0,0.12)`       | `rgba(255,255,255,0.10)`     |

Border width: 0.5 pt.

### States

| State        | Visual Changes                                          |
|--------------|--------------------------------------------------------|
| Normal       | Default appearance                                      |
| Hover        | Segment background slightly highlighted                  |
| Pressed      | Darker/lighter fill on pressed segment                   |
| Selected     | Filled background (pill in capsule, white bg in rounded) |
| Disabled     | 50% opacity, no interaction                              |
| Focused      | Focus ring around entire control                         |

### Animation

#### Capsule Style Selection Animation

The sliding pill uses a spring animation:

| Transition                   | Duration (ms) | Curve            |
|------------------------------|---------------|------------------|
| Selection slide (capsule)    | 250           | Spring (snappy)  |
| Selection change (rounded)   | 100           | Ease Out         |
| Hover highlight              | 80            | Ease Out         |
| Press feedback               | 30            | Ease Out         |
| Disable/Enable               | 200           | Ease In Out      |

### Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from control bounds
Radius:   control corner radius + 3 pt
```

Arrow keys navigate between segments when focused.

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Space / Return  | Activate/select current segment            |
| Left Arrow      | Move to previous segment                   |
| Right Arrow     | Move to next segment                       |
| Tab             | Move focus to next control                 |
| Shift+Tab       | Move focus to previous control             |

### Segment Content

Each segment can contain:
- Text label only
- Icon only (NSImage, typically SF Symbols)
- Icon + text label
- Menu attached to a segment

Segment width can be:
- Automatic (fits content)
- Fixed (set per segment via `setWidth(_:forSegment:)`)

### Dija Skin Mapping

```
comp! SegmentedControl {
    attr variant, SegmentedVariant, default: SegmentedVariant::Rounded
    attr size, Size, default: Size::MD

    // macOS skin maps:
    // SegmentedVariant::Rounded   -> .rounded style
    // SegmentedVariant::Capsule   -> .capsule style (sliding pill)
    // SegmentedVariant::Separated -> .separated style
    //
    // Size::XS  -> Mini
    // Size::SM  -> Small
    // Size::MD  -> Regular
    // Size::LG  -> Large
    //
    // Capsule: animate pill position with spring
    // Rounded: swap selected segment fill instantly
    // Separated: accent-fill selected, gray-fill unselected
}
```

## Android

Source: m3.material.io/components/segmented-buttons/specs

M3 equivalent of iOS segmented control. Two density modes: single-select
and multi-select.

### Variants

| Variant | Behavior | Usage |
|---------|----------|-------|
| Single-select | Radio-like, one active at a time | View switcher, sort order |
| Multi-select | Checkbox-like, multiple active | Filter tags |

### Metrics

| Property | Value |
|----------|-------|
| Height | 40dp |
| Min segment width | 48dp |
| Corner radius (outer) | 20dp (full pill) |
| Corner radius (inner dividers) | 0dp |
| Border width | 1dp |
| Icon size | 18dp |
| Icon-label gap | 8dp |
| Horizontal padding | 12dp |
| Label font | Label Large (Roboto Medium 500, 14sp) |
| Touch target | 48dp min height |

Segments are equal width, dividing the total width evenly. The outer shape
is a continuous pill (20dp radius on first and last segment).

### Colors

#### Selected Segment

| Element | Light | Dark |
|---------|-------|------|
| Container | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Label/icon | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |
| Check icon | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |

#### Unselected Segment

| Element | Light | Dark |
|---------|-------|------|
| Container | transparent | transparent |
| Border | `#79747E` (outline) | `#938F99` |
| Label/icon | `#1D1B20` (onSurface) | `#E6E0E9` |

#### Disabled

| Element | Value |
|---------|-------|
| Container | transparent |
| Border | onSurface @ 12% |
| Label/icon | onSurface @ 38% |

### States

| State | Effect |
|-------|--------|
| Hovered | State layer 8% (onSecondaryContainer if selected, onSurface if not) |
| Focused | State layer 10% |
| Pressed | State layer 10% + ripple |
| Disabled | Reduced opacity (container 12%, content 38%) |

### Selection Animation

When a segment is selected:
1. Check icon (18dp) fades in and slides from left (Short 4, 200ms)
2. Container fills with secondaryContainer color
3. If a label-only segment, check icon appears before the label, pushing it right

### Layout

```
+--[Segment A]--+--[Segment B]--+--[Segment C]--+
|  [x] Label A  |    Label B    |    Label C    |
+----------------+----------------+----------------+
     selected         unselected      unselected
```

Dividers between segments: 1dp, outline color. Dividers adjacent to
a selected segment are hidden (the selected container fills the space).

## Windows

Source: WinUI 3 RadioButtons (grouped), SegmentedControl (WinUI 3 Gallery)

Windows does not have a native 1:1 equivalent to iOS UISegmentedControl. The closest patterns are:

1. **RadioButtons** (grouped, pill-shaped) -- standard WinUI control for mutually exclusive choices
2. **SegmentedControl** -- community/gallery pattern using styled ToggleButtons in a horizontal strip

### RadioButtons (Standard Approach)

RadioButtons displays a grouped set of radio button options. Each item is a selectable option.

#### Radio Button Metrics

| Property | Value |
|----------|-------|
| Circle diameter (outer) | 20px |
| Circle diameter (inner dot, selected) | 8px |
| Hit area | 32px height |
| Text offset from circle | 8px |
| Font | 14px, Regular |
| Vertical spacing between items | 4px |
| Indicator color (selected) | AccentFillColorDefault |
| Indicator color (unselected) | ControlStrongStrokeColorDefault (1px ring) |

#### Radio Button States

| State | Circle | Text |
|-------|--------|------|
| Rest (unselected) | 1px ring, ControlStrongStrokeColorDefault | TextFillColorPrimary |
| Hover (unselected) | 1px ring, ControlStrongStrokeColorDefault | TextFillColorPrimary |
| Selected | AccentColor fill + 8px white inner dot | TextFillColorPrimary |
| Hover (selected) | AccentFillColorSecondary + inner dot | TextFillColorPrimary |
| Disabled | ControlStrongStrokeColorDisabled | TextFillColorDisabled |

### Segmented / Pill Toggle (Gallery Pattern)

Used when a compact, horizontal switch between 2-5 options is needed. Built from grouped ToggleButtons.

#### Container Metrics

| Property | Value |
|----------|-------|
| Background | ControlFillColorDefault |
| Corner radius | 4px |
| Border | 1px ControlStrokeColorDefault |
| Padding (inner) | 2px |
| Height | 32px |

#### Segment Metrics

| Property | Value |
|----------|-------|
| Min width per segment | 48px |
| Padding | 8px horizontal, 4px vertical |
| Corner radius | 3px (inner segments) |
| Font | 14px, Regular |

#### Segment States

| State | Background | Text |
|-------|-----------|------|
| Rest (unselected) | Transparent | TextFillColorSecondary |
| Hover (unselected) | SubtleFillColorSecondary | TextFillColorPrimary |
| Selected | ControlFillColorDefault (elevated via slight fill) or LayerFillColorDefault | TextFillColorPrimary |
| Disabled | Transparent | TextFillColorDisabled |

The selected segment has a **subtle elevation** (slightly brighter fill) and optionally a thin border or shadow to appear raised above the container.

#### Selection Indicator Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Selection slide (background pill) | 200ms | Decelerate |
| Hover fill change | 100ms | Control fast |

### Dija Mapping

For Windows skin, the segmented control should render as:
- **2-3 options**: Segmented pill toggle (horizontal ToggleButton strip)
- **4+ options or vertical layout**: RadioButtons (standard grouped radio)

Both patterns use the same underlying `dija-ui` SegmentedControl component, just with different skin rendering.

## Linux

### Overview

GNOME does not have a dedicated segmented control widget like iOS. Instead, it uses
a **linked group of GtkToggleButton** widgets, where buttons share borders and only
outer corners are rounded.

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Group background | transparent (buttons provide own bg) | transparent |
| Button background (unselected) | `#FFFFFF` | `#404040` |
| Button background (selected) | `#FFFFFF` (same, but pressed look) | `#404040` |
| Button background (selected, checked) | `rgba(0,0,0, 0.07)` | `rgba(255,255,255, 0.07)` |
| Border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Inner separator | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Text color (unselected) | `#2E3436` | `#FFFFFF` |
| Text color (selected) | `#2E3436` | `#FFFFFF` |

### Metrics

| Property | Value |
|----------|-------|
| Button min-height | 34px |
| Button horizontal padding | 16px |
| Button vertical padding | 8px |
| Outer corner radius | 6px |
| Inner corner radius | 0px |
| Font | Adwaita Sans Regular, 15px |
| Gap between buttons | 0px (touching) |
| Icon size | 16x16px |

### Corner Radius Pattern

For a group of N linked buttons:

```
[First] [Middle...] [Last]
  6|0     0|0        0|6    (left|right radius)
```

| Position | Border Radius |
|----------|--------------|
| First (leftmost) | top-left: 6px, bottom-left: 6px, right: 0px |
| Middle | all 0px |
| Last (rightmost) | top-right: 6px, bottom-right: 6px, left: 0px |
| Single (only one) | all 6px |

### States

| State | Background | Border |
|-------|-----------|--------|
| Unselected (rest) | button bg | 1px border |
| Unselected (hover) | slightly darker/lighter | 1px border |
| Unselected (active) | pressed bg | inset shadow |
| Selected (checked) | `rgba(0,0,0, 0.07)` / `rgba(255,255,255, 0.07)` | 1px border |
| Selected (hover) | `rgba(0,0,0, 0.12)` / `rgba(255,255,255, 0.12)` | 1px border |
| Disabled | rest, opacity 0.5 | 1px border |

### Selection Behavior

| Property | Value |
|----------|-------|
| Selection mode | Single (radio-like, one active at a time) |
| Allow none selected | Depends on app (usually no) |
| Click behavior | Click selects, deselects others |

Unlike iOS segmented controls, there is **no sliding indicator animation**. Selection
change is immediate with a simple background color transition.

### Keyboard Support

| Key | Action |
|-----|--------|
| Space / Enter | Toggle current button |
| Tab | Move focus to next button in group |
| Arrow Left/Right | Move focus within linked group |

### Vertical Linked Groups

Linked buttons can also be grouped vertically:

```
[ Top    ]  radius: 6 6 0 0
[ Middle ]  radius: 0 0 0 0
[ Bottom ]  radius: 0 0 6 6
```

### Alternative: AdwViewSwitcher

For tab-like navigation (not toggle selection), GNOME uses `AdwViewSwitcher`:

| Property | Value |
|----------|-------|
| Style | Flat buttons with icon + label |
| Selected indicator | Accent-colored bottom line (2px) |
| Layout | Horizontal in header bar, vertical in bottom bar |
| Adaptive | Switches between wide (icon+label) and narrow (icon only) |

The view switcher is preferred over segmented controls for page/view switching.

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Background color | 200ms | ease-in-out |
| Check state change | immediate | -- |
