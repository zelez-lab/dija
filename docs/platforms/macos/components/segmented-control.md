# macOS Segmented Control (NSSegmentedControl)

Reference: NSSegmentedControl, NSSegmentedControl.Style, Apple HIG (macOS 14+).

## Overview

`NSSegmentedControl` displays a horizontal group of mutually exclusive (or independently selectable) segments. It is used for switching views, filtering content, or grouping related actions.

## Styles

### NSSegmentedControl.Style

| Style                | Description                                               | Usage                       |
|----------------------|-----------------------------------------------------------|-----------------------------|
| `.automatic`         | System picks based on context                              | Default                     |
| `.rounded`           | Rounded rect segments with visible borders                 | Window body, toolbars       |
| `.texturedRounded`   | Flatter, toolbar-appropriate appearance (deprecated name)  | Toolbars                    |
| `.capsule`           | Pill-shaped with a sliding selection indicator              | Tab-like switching          |
| `.smallSquare`       | Compact square segments                                    | Tight spaces, palettes      |
| `.separated`         | Individual rounded-rect buttons with gaps between them     | Discrete actions            |

### Tracking Modes

| Mode                  | Description                                          |
|-----------------------|------------------------------------------------------|
| `.selectOne`          | Only one segment selected at a time (radio behavior) |
| `.selectAny`          | Any combination can be selected (checkbox behavior)  |
| `.momentary`          | Segments act as momentary push buttons               |

## Metrics

### Rounded Style (`.rounded`)

| Control Size | Height (pt) | Segment Min Width (pt) | Corner Radius (pt) | Divider Width (pt) | Font Size (pt) |
|-------------|-------------|------------------------|---------------------|---------------------|----------------|
| Mini        | 16          | 20                     | 3                   | 1                   | 9              |
| Small       | 19          | 24                     | 4                   | 1                   | 11             |
| Regular     | 22          | 28                     | 5                   | 1                   | 13             |
| Large       | 28          | 34                     | 7                   | 1                   | 15             |

### Capsule Style (`.capsule`)

| Control Size | Height (pt) | Segment Min Width (pt) | Corner Radius (pt) | Font Size (pt) |
|-------------|-------------|------------------------|---------------------|----------------|
| Mini        | 16          | 20                     | 8 (capsule)         | 9              |
| Small       | 19          | 24                     | 9.5 (capsule)       | 11             |
| Regular     | 22          | 28                     | 11 (capsule)        | 13             |
| Large       | 28          | 34                     | 14 (capsule)        | 15             |

The capsule style has a sliding pill indicator behind the selected segment.

### Separated Style (`.separated`)

| Control Size | Height (pt) | Segment Min Width (pt) | Corner Radius (pt) | Gap Between (pt) | Font Size (pt) |
|-------------|-------------|------------------------|---------------------|-------------------|----------------|
| Mini        | 16          | 20                     | 3                   | 2                 | 9              |
| Small       | 19          | 24                     | 4                   | 2                 | 11             |
| Regular     | 22          | 28                     | 6                   | 4                 | 13             |
| Large       | 28          | 34                     | 8                   | 4                 | 15             |

### Padding

| Control Size | Horizontal Padding per Segment (pt) | Icon-to-Label Gap (pt) |
|-------------|--------------------------------------|------------------------|
| Mini        | 4                                    | 2                      |
| Small       | 6                                    | 3                      |
| Regular     | 8                                    | 4                      |
| Large       | 12                                   | 5                      |

## Colors

### Rounded Style

| Element                  | Light Mode                    | Dark Mode                      |
|--------------------------|-------------------------------|--------------------------------|
| Background               | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Selected segment bg      | `#FFFFFF`                     | `rgba(255,255,255,0.18)`       |
| Selected segment shadow   | `rgba(0,0,0,0.06)` offset 0,0.5 blur 1 | `rgba(0,0,0,0.20)` offset 0,0.5 blur 1 |
| Divider                  | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.10)`       |
| Text (normal)            | labelColor                    | labelColor                     |
| Text (selected)          | labelColor                    | labelColor                     |
| Text (disabled)          | disabledControlTextColor      | disabledControlTextColor       |

### Capsule Style

| Element                  | Light Mode                    | Dark Mode                      |
|--------------------------|-------------------------------|--------------------------------|
| Track background         | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Selected pill bg         | `#FFFFFF`                     | `rgba(255,255,255,0.20)`       |
| Selected pill shadow      | `rgba(0,0,0,0.08)` offset 0,1 blur 2 | `rgba(0,0,0,0.25)` offset 0,1 blur 2 |
| Text (normal)            | secondaryLabelColor           | secondaryLabelColor            |
| Text (selected)          | labelColor                    | labelColor                     |

### Separated Style

| Element                  | Light Mode                    | Dark Mode                      |
|--------------------------|-------------------------------|--------------------------------|
| Segment background       | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`       |
| Segment hover            | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.12)`       |
| Segment selected         | controlAccentColor            | controlAccentColor             |
| Segment selected text    | `#FFFFFF`                     | `#FFFFFF`                      |
| Segment pressed          | `rgba(0,0,0,0.14)`           | `rgba(255,255,255,0.16)`       |

### Border

| Style      | Border Light              | Border Dark                  |
|------------|---------------------------|------------------------------|
| Rounded    | `rgba(0,0,0,0.12)`       | `rgba(255,255,255,0.10)`     |
| Capsule    | `rgba(0,0,0,0.08)`       | `rgba(255,255,255,0.08)`     |
| Separated  | `rgba(0,0,0,0.12)`       | `rgba(255,255,255,0.10)`     |

Border width: 0.5 pt.

## States

| State        | Visual Changes                                          |
|--------------|--------------------------------------------------------|
| Normal       | Default appearance                                      |
| Hover        | Segment background slightly highlighted                  |
| Pressed      | Darker/lighter fill on pressed segment                   |
| Selected     | Filled background (pill in capsule, white bg in rounded) |
| Disabled     | 50% opacity, no interaction                              |
| Focused      | Focus ring around entire control                         |

## Animation

### Capsule Style Selection Animation

The sliding pill uses a spring animation:

| Transition                   | Duration (ms) | Curve            |
|------------------------------|---------------|------------------|
| Selection slide (capsule)    | 250           | Spring (snappy)  |
| Selection change (rounded)   | 100           | Ease Out         |
| Hover highlight              | 80            | Ease Out         |
| Press feedback               | 30            | Ease Out         |
| Disable/Enable               | 200           | Ease In Out      |

## Focus Ring

```
Color:    controlAccentColor at 50% opacity
Width:    3 pt stroke
Offset:   2 pt outset from control bounds
Radius:   control corner radius + 3 pt
```

Arrow keys navigate between segments when focused.

## Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Space / Return  | Activate/select current segment            |
| Left Arrow      | Move to previous segment                   |
| Right Arrow     | Move to next segment                       |
| Tab             | Move focus to next control                 |
| Shift+Tab       | Move focus to previous control             |

## Segment Content

Each segment can contain:
- Text label only
- Icon only (NSImage, typically SF Symbols)
- Icon + text label
- Menu attached to a segment

Segment width can be:
- Automatic (fits content)
- Fixed (set per segment via `setWidth(_:forSegment:)`)

## Dija Skin Mapping

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
