# macOS Sidebar

Reference: NSSplitViewItem (sidebar behavior), NSOutlineView (source list style), NSVisualEffectView (sidebar material), Apple HIG (macOS 14+).

## Overview

The macOS sidebar is a standard navigation pattern for organizing content hierarchically. It is typically implemented as an `NSOutlineView` with `.sourceList` style inside an `NSSplitViewItem` with `.sidebar` behavior. The sidebar gets automatic vibrancy, selection highlighting, and standard sizing.

## Layout

### Width

| Property                  | Value (pt) |
|---------------------------|------------|
| Default width              | 240        |
| Minimum width              | 180        |
| Maximum width              | 320        |
| Recommended range          | 200-280    |
| Collapse threshold         | 100        |

### Height

The sidebar extends the full height of the window. In "full-height sidebar" mode (macOS 11+), the sidebar extends behind the toolbar into the title bar area.

| Configuration            | Sidebar Top Edge                          |
|--------------------------|-------------------------------------------|
| Standard                 | Below toolbar separator                   |
| Full-height              | Top of window (behind titlebar/toolbar)    |

Full-height sidebar requires:
```swift
splitViewItem.allowsFullHeightLayout = true
window.titlebarSeparatorStyle = .none
```

## Metrics

### Row Metrics

| Property                  | Value (pt) |
|---------------------------|------------|
| Row height                 | 24         |
| Row horizontal padding     | 10         |
| Row vertical padding       | 2          |
| Selection corner radius    | 6          |
| Selection inset (H)        | 10         |
| Selection inset (V)        | 0          |
| Indentation per level      | 16         |
| Icon size                  | 16         |
| Icon to text gap           | 6          |

### Group Header Metrics

| Property                  | Value (pt) |
|---------------------------|------------|
| Group header height        | 28         |
| Group header top padding   | 16 (first), 8 (subsequent) |
| Group header font size     | 11         |
| Group header font weight   | Bold       |
| Group header letter spacing | +0.5 pt   |
| Group header text transform| Uppercase  |

### Badge (Count Indicator)

Sidebar rows often show a count badge on the right side:

| Property                  | Value             |
|---------------------------|-------------------|
| Badge height               | 18 pt             |
| Badge min width            | 18 pt             |
| Badge horizontal padding   | 6 pt              |
| Badge corner radius        | 9 pt (capsule)    |
| Badge font size            | 10 pt             |
| Badge font weight          | Medium            |
| Badge right margin         | 6 pt              |

## Colors

### Background

| State                    | Light Mode                   | Dark Mode                    |
|--------------------------|------------------------------|------------------------------|
| Background               | sidebar material vibrancy    | sidebar material vibrancy    |
| Fallback (no vibrancy)   | `#F6F6F6`                    | `#2D2D2D`                    |

### Selection

| State                    | Light Mode                         | Dark Mode                          |
|--------------------------|------------------------------------|------------------------------------|
| Selected (focused)       | controlAccentColor with vibrancy   | controlAccentColor with vibrancy   |
| Selected (unfocused)     | `rgba(0,0,0,0.06)`                | `rgba(255,255,255,0.08)`           |
| Hover                    | `rgba(0,0,0,0.04)`                | `rgba(255,255,255,0.06)`           |
| Pressed                  | `rgba(0,0,0,0.08)`                | `rgba(255,255,255,0.10)`           |

The focused selection uses the accent color composited with vibrancy for a rich, translucent tint effect.

### Text

| Element                  | Light Mode                 | Dark Mode                  |
|--------------------------|----------------------------|----------------------------|
| Item text                | labelColor                 | labelColor                 |
| Item selected text       | `#FFFFFF`                  | `#FFFFFF`                  |
| Group header text        | secondaryLabelColor        | secondaryLabelColor        |
| Badge text (normal)      | secondaryLabelColor        | secondaryLabelColor        |
| Badge text (selected)    | `#FFFFFF`                  | `#FFFFFF`                  |
| Badge background (normal)| `rgba(0,0,0,0.08)`        | `rgba(255,255,255,0.10)`   |
| Badge background (selected)| `rgba(255,255,255,0.25)` | `rgba(255,255,255,0.25)`   |

### Icons

| State                    | Treatment                                    |
|--------------------------|----------------------------------------------|
| Normal                   | Template image, tinted with labelColor        |
| Selected (focused)       | Template image, tinted white                  |
| Selected (unfocused)     | Template image, tinted with labelColor        |
| Disabled                 | Template image at 40% opacity                 |

### Separator

A thin separator line appears between the sidebar and the content area:

| Property                  | Value                            |
|---------------------------|----------------------------------|
| Width                      | 0.5 pt (1 px on Retina)        |
| Color (light)              | `rgba(0,0,0,0.12)`             |
| Color (dark)               | `rgba(255,255,255,0.12)`       |

## Disclosure (Expandable Groups)

| Element                  | Value                            |
|--------------------------|----------------------------------|
| Disclosure triangle size | 10x10 pt                         |
| Disclosure color         | tertiaryLabelColor               |
| Disclosure animation     | 150 ms rotate, Ease In Out       |
| Collapsed state          | Triangle points right            |
| Expanded state           | Triangle points down             |

## Interaction States

| Interaction              | Behavior                                     |
|--------------------------|----------------------------------------------|
| Click                    | Select item, navigate                        |
| Double-click             | Open in new window/tab (context-dependent)   |
| Right-click              | Context menu                                 |
| Drag                     | Reorder items (if enabled)                   |
| Drop                     | Rearrange or move content                    |
| Collapse sidebar         | Click toggle button or drag divider past min |

## Sidebar Toggle

The standard sidebar toggle button in the toolbar:
- SF Symbol: `sidebar.leading`
- Size: 16 pt icon, toolbar-style button
- Keyboard shortcut: Cmd+Shift+L (or Cmd+Control+S)

## Animation

| Transition                    | Duration (ms) | Curve          |
|-------------------------------|---------------|----------------|
| Sidebar collapse              | 250           | Ease In Out    |
| Sidebar expand                | 250           | Ease In Out    |
| Selection change              | 100           | Ease Out       |
| Disclosure expand/collapse    | 150           | Ease In Out    |
| Row insert/delete             | 250           | Ease In Out    |
| Badge count update            | 200           | Ease In Out    |
| Hover highlight               | 80            | Ease Out       |

## Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Up Arrow        | Move selection up one row                  |
| Down Arrow      | Move selection down one row                |
| Right Arrow     | Expand group / enter subgroup              |
| Left Arrow      | Collapse group / go to parent              |
| Return          | Open/navigate to selected item             |
| Tab             | Move focus to content area                 |
| Space           | Toggle selection (if applicable)           |
| Cmd+Shift+L     | Toggle sidebar visibility                  |

## Dija Skin Mapping

```
comp! Sidebar {
    // macOS skin should provide:
    // Background: sidebar vibrancy material
    // Rows: 24 pt height, 10 pt horizontal padding
    // Selection: accent-tinted vibrancy rect, 6 pt radius
    // Icons: 16 pt template images
    // Group headers: 11 pt bold uppercase
    // Separator: 0.5 pt line at trailing edge
    //
    // Full-height mode extends behind toolbar
    // Width: 240 pt default, 180-320 pt range
}
```
