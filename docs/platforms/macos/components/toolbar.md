# macOS Toolbar (NSToolbar)

Reference: NSToolbar, NSToolbarItem, NSWindow.ToolbarStyle, Apple HIG (macOS 14+).

## Overview

`NSToolbar` manages the toolbar area at the top of a window. Since macOS 11, toolbars are integrated with the title bar and support several display styles. The toolbar is a system-managed container -- you provide items and the system handles layout, overflow, and customization.

## Toolbar Styles

### NSWindow.ToolbarStyle

| Style                | Height (pt) | Description                                      |
|----------------------|-------------|--------------------------------------------------|
| `.automatic`         | varies      | System picks based on window configuration       |
| `.expanded`          | ~78         | Tall toolbar with title above, items below        |
| `.preference`        | ~78         | Same as expanded, used for preferences windows    |
| `.unified`           | ~52         | Title and toolbar items on same row              |
| `.unifiedCompact`    | ~38         | Shorter unified, for utility/secondary windows    |

### Height Breakdown (`.unified`)

| Component            | Height (pt) |
|---------------------|-------------|
| Title bar area       | 28          |
| Toolbar content area | 24          |
| Total                | 52          |

### Height Breakdown (`.unifiedCompact`)

| Component            | Height (pt) |
|---------------------|-------------|
| Total                | 38          |

### Height Breakdown (`.expanded`)

| Component            | Height (pt) |
|---------------------|-------------|
| Title bar area       | 28          |
| Toolbar content area | ~50         |
| Total                | ~78         |

## Toolbar Items

### Standard Item Types

| Type                          | Description                                    |
|-------------------------------|------------------------------------------------|
| Custom item (with view)       | Any NSView embedded in toolbar                 |
| Image item                    | SF Symbol or NSImage button                    |
| Segmented item                | NSSegmentedControl in toolbar                  |
| Search item                   | NSSearchField in toolbar                       |
| Tracking separator            | Links to split view divider                     |
| Space                         | Fixed-size space (16 pt)                       |
| Flexible space                | Expanding space that fills available width       |
| Sidebar tracking separator    | Separator that tracks sidebar split view        |

### Standard Identifiers

| Identifier                       | Description                                  |
|----------------------------------|----------------------------------------------|
| `.sidebarTrackingSeparator`      | Tracks sidebar divider position              |
| `.flexibleSpace`                 | Expanding gap                                |
| `.space`                         | Fixed 16 pt gap                              |
| `.toggleSidebar`                 | Standard sidebar toggle button               |
| `.print`                         | Standard print button                        |
| `.showColors`                    | Standard color panel button                  |
| `.showFonts`                     | Standard font panel button                   |
| `.inspectorTrackingSeparator`    | Tracks inspector divider (macOS 14+)         |
| `.toggleInspector`               | Standard inspector toggle button             |

## Metrics

### Toolbar Item Sizing

| Control Size | Button Height (pt) | Icon Size (pt) | Min Width (pt) |
|-------------|-------------------|----------------|----------------|
| Regular     | 24                | 16             | 28             |
| Small       | 20                | 13             | 22             |

### Spacing

| Property                        | Value (pt) |
|---------------------------------|------------|
| Inter-item spacing              | 8          |
| Item to edge padding            | 12         |
| Icon to label gap (labeled)     | 2          |
| Section gap (around separators) | 12         |

### Toolbar Item Labels

When `displayMode` includes labels:

| Property                        | Value             |
|---------------------------------|-------------------|
| Font size                       | 10 pt             |
| Font weight                     | Regular           |
| Label position                  | Below icon        |
| Combined item height            | ~44 pt            |

## Colors

### Toolbar Background

| Configuration           | Light Mode                   | Dark Mode                    |
|------------------------|------------------------------|------------------------------|
| Standard               | titlebar material vibrancy   | titlebar material vibrancy   |
| Fallback (no vibrancy) | `#ECECEC`                    | `#323232`                    |

### Toolbar Items

| State        | Light Mode                    | Dark Mode                     |
|-------------|-------------------------------|-------------------------------|
| Normal       | Transparent                   | Transparent                   |
| Hover        | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`      |
| Pressed      | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.12)`      |
| Selected     | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.10)`      |
| Disabled     | 40% opacity icon/text         | 40% opacity icon/text         |

### Separator Line

The separator line between toolbar and content:

| Context               | Light Mode              | Dark Mode               |
|-----------------------|-------------------------|-------------------------|
| Separator             | `rgba(0,0,0,0.12)`     | `rgba(255,255,255,0.12)`|
| Width                 | full window width       | full window width       |
| Height                | 0.5 pt                 | 0.5 pt                  |

### Title Text

| Configuration      | Color Light          | Color Dark           | Font Size (pt) | Weight    |
|--------------------|----------------------|----------------------|----------------|-----------|
| Window title       | labelColor           | labelColor           | 13             | Semibold  |
| Subtitle           | secondaryLabelColor  | secondaryLabelColor  | 11             | Regular   |

## Traffic Light Positioning

The close/minimize/zoom buttons position depends on toolbar style:

| Style              | Traffic Light Position              |
|--------------------|-------------------------------------|
| `.unified`         | Vertically centered in title area   |
| `.unifiedCompact`  | Vertically centered in toolbar      |
| `.expanded`        | Top-left at standard offset (20, 20)|

Traffic light buttons:
- Diameter: 12 pt each
- Spacing: 8 pt between centers
- Left offset: 20 pt from window edge (7 pt from each button edge to next)

## Display Modes

### NSToolbar.DisplayMode

| Mode              | Description                                  |
|-------------------|----------------------------------------------|
| `.default`        | System-chosen (currently icon only)          |
| `.iconAndLabel`   | Icons with text labels below                 |
| `.iconOnly`       | Icons only (most common)                     |
| `.labelOnly`      | Text labels only                             |

## Overflow Menu

When the window is too narrow for all toolbar items:
- Overflow chevron button appears at the right edge
- Clicking opens a menu with overflowed items
- Items overflow right-to-left (rightmost items overflow first)
- Flexible space items collapse before other items

## Toolbar Customization

Users can customize the toolbar (right-click > "Customize Toolbar..."):
- Drag items in/out of the toolbar
- Rearrange item order
- Choose display mode
- Reset to defaults
- Sheet presentation with all available items

## Animation

| Transition                        | Duration (ms) | Curve         |
|-----------------------------------|---------------|---------------|
| Toolbar show/hide                 | 250           | Ease In Out   |
| Toolbar item reorder              | 200           | Ease In Out   |
| Overflow menu appear              | 150           | Ease Out      |
| Sidebar tracking separator move   | 0             | Immediate     |
| Toolbar style change              | 300           | Ease In Out   |

## Dija Skin Mapping

```
comp! Toolbar {
    attr style, ToolbarStyle, default: ToolbarStyle::Unified
    attr display_mode, ToolbarDisplayMode, default: ToolbarDisplayMode::IconOnly

    // macOS skin maps:
    // ToolbarStyle::Unified        -> .unified (52 pt)
    // ToolbarStyle::UnifiedCompact -> .unifiedCompact (38 pt)
    // ToolbarStyle::Expanded       -> .expanded (78 pt)
    //
    // Background: titlebar vibrancy material
    // Items: transparent, hover highlight, 24 pt height
    // Separator: 0.5 pt line below toolbar
    // Traffic lights: system-positioned
}
```
