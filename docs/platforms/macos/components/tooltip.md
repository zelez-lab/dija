# macOS Tooltip (NSToolTipManager)

Reference: NSView tooltip support, NSToolTipManager (private), Apple HIG (macOS 14+).

## Overview

Tooltips in macOS are small, transient text labels that appear when the user hovers over a UI element. They are managed by the system through `NSView.toolTip` and the internal `NSToolTipManager`. Tooltips have a distinct yellow-ish appearance in light mode and a gray appearance in dark mode.

## Timing

| Property                  | Value              |
|---------------------------|--------------------|
| Hover delay before show    | ~1000 ms          |
| Display duration           | ~10000 ms (10 sec)|
| Fade-in duration           | ~200 ms           |
| Fade-out duration          | ~200 ms           |
| Re-hover delay (same)      | ~100 ms           |
| Re-hover delay (different) | ~500 ms           |

The hover delay is measured from when the cursor enters the tooltip rect. If the user moves the mouse away and back quickly, the tooltip reappears faster (re-hover delay).

## Metrics

### Sizing

| Property                  | Value              |
|---------------------------|--------------------|
| Maximum width              | 300 pt            |
| Padding (horizontal)       | 8 pt              |
| Padding (vertical)         | 4 pt              |
| Corner radius              | 4 pt              |
| Offset from cursor         | (0, 18) pt approx |

The tooltip is positioned below and slightly to the right of the cursor. If the tooltip would extend beyond the screen edge, it flips to appear above or to the left.

### Position Rules

| Screen Edge          | Tooltip Position                          |
|---------------------|-------------------------------------------|
| Bottom too close     | Appears above cursor                      |
| Right too close      | Shifts left to fit on screen              |
| Top too close        | Appears below cursor (default behavior)   |
| Left too close       | Shifts right                              |

## Typography

| Property              | Value              |
|-----------------------|--------------------|
| Font                   | SF Pro (system)    |
| Font size              | 11 pt             |
| Font weight            | Regular            |
| Line height            | 14 pt             |
| Max lines              | ~10 (wraps at max width) |
| Text alignment         | Left               |

## Colors

### Background

| Mode      | Value                                  |
|-----------|----------------------------------------|
| Light     | `#FFFFCC` (pale yellow, tooltip classic) |
| Dark      | `#3C3C3C` (dark gray)                  |

With vibrancy enabled (macOS 10.14+), tooltips use the `.toolTip` material:

| Mode      | Vibrancy Material                      |
|-----------|----------------------------------------|
| Light     | `.toolTip` material (slightly warm tint)|
| Dark      | `.toolTip` material (neutral gray)      |

Fallback when vibrancy is disabled:

| Mode      | Fallback                               |
|-----------|----------------------------------------|
| Light     | `#FFFFCC`                              |
| Dark      | `#3C3C3C`                              |

### Text

| Mode      | Color                                  |
|-----------|----------------------------------------|
| Light     | `#000000`                              |
| Dark      | `#FFFFFF`                              |

### Border

| Mode      | Color                                  |
|-----------|----------------------------------------|
| Light     | `rgba(0,0,0,0.15)`                    |
| Dark      | `rgba(255,255,255,0.10)`              |

Border width: 0.5 pt.

### Shadow

```
Color:   rgba(0, 0, 0, 0.12)
Offset:  (0, 2) pt
Blur:    8 pt
```

## Animation

| Transition           | Duration (ms) | Curve         |
|---------------------|---------------|---------------|
| Appear (fade in)     | 200           | Ease Out      |
| Disappear (fade out) | 200           | Ease In       |
| Reposition           | 0             | Immediate     |

## Interaction

| Event                    | Behavior                                |
|--------------------------|------------------------------------------|
| Mouse enters tooltip rect | Start hover delay timer                 |
| Mouse exits tooltip rect  | Dismiss tooltip (with fade)             |
| Mouse button click        | Dismiss tooltip immediately              |
| Mouse moves within rect   | Tooltip stays visible                    |
| Keyboard event            | Dismiss tooltip immediately              |
| Scroll event              | Dismiss tooltip immediately              |
| Window becomes inactive   | Dismiss tooltip immediately              |

## Rich Tooltips

macOS 14+ introduced richer tooltip content through accessibility descriptions, but the visual tooltip itself remains text-only. For rich content, apps typically use custom popover views, not the tooltip system.

## Custom Tooltip Rects

`NSView.addToolTipRect(_:owner:userData:)` allows defining rectangular regions with distinct tooltips:

| Property              | Description                            |
|-----------------------|----------------------------------------|
| Tracking rect          | NSRect defining the hover area        |
| Owner                  | Object providing tooltip string        |
| User data              | Optional context pointer               |

Multiple tooltip rects can exist on a single view.

## System Tooltips in Standard Controls

Standard AppKit controls provide built-in tooltips:

| Control              | Default Tooltip Content                |
|---------------------|----------------------------------------|
| NSToolbarItem        | Item label (when icon-only display)   |
| NSButton (toolbar)   | Button title or accessibility label    |
| NSSegmentedControl   | Per-segment via `setToolTip(_:forSegment:)` |
| Truncated text       | Full text (automatic for NSTextField)  |
| Menu bar item        | Help tag text                          |

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.helpTag` (system tooltip)               |
| Announced    | Tooltip text read by VoiceOver             |
| Timing       | VoiceOver reads immediately (no delay)     |

## Dija Skin Mapping

```
comp! Tooltip {
    attr text, &str, default: ""
    attr delay_ms, u32, default: 1000
    attr max_width, f32, default: 300.0

    // macOS skin maps:
    // Background: #FFFFCC (light) / #3C3C3C (dark)
    // Or: .toolTip vibrancy material
    // Text: 11 pt system font, regular weight
    // Padding: 8 pt horizontal, 4 pt vertical
    // Corner radius: 4 pt
    // Border: 0.5 pt at rgba(0,0,0,0.15) / rgba(255,255,255,0.10)
    // Shadow: rgba(0,0,0,0.12) offset (0,2) blur 8
    // Show delay: 1000 ms
    // Fade: 200 ms
}
```
