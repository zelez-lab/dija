# macOS Table View (NSTableView / NSOutlineView)

Reference: NSTableView, NSOutlineView, NSTableColumn, Apple HIG (macOS 14+).

## Overview

`NSTableView` displays data in rows and columns. `NSOutlineView` is a subclass that adds hierarchical disclosure (tree structure). Since macOS 11 Big Sur, tables have adopted a more modern appearance with rounded selection highlights, increased row heights, and inset content.

## Table Styles

### NSTableView.Style

| Style             | Description                                                 | Usage                      |
|-------------------|-------------------------------------------------------------|----------------------------|
| `.automatic`      | System picks based on context                                | Default                    |
| `.fullWidth`      | Selection extends full width of table, no inset              | Dense data tables          |
| `.inset`          | Selection has rounded corners, inset from edges              | Settings, preferences      |
| `.sourceList`     | Sidebar/source list appearance with vibrancy                 | Sidebars                   |
| `.plain`          | No special styling, minimal chrome                           | Custom layouts             |

## Metrics

### Row Heights

| Configuration           | Row Height (pt) | Notes                              |
|------------------------|-----------------|-------------------------------------|
| Default                 | 24              | Standard single-line row            |
| Source list              | 24              | Sidebar row                         |
| Large row height        | 34              | Rows with subtitle or icon          |
| Custom                  | User-defined    | Via delegate `heightOfRow()`        |

### Column Metrics

| Property                    | Default Value (pt) | Notes                          |
|-----------------------------|-------------------|--------------------------------|
| Minimum column width         | 40                | `minWidth` property            |
| Default column width         | 100               | `width` property               |
| Column header height         | 24                | Standard header row            |
| Column resize handle width   | 6                 | Draggable area at edge         |
| Inter-cell spacing (H)       | 3                 | `intercellSpacing.width`       |
| Inter-cell spacing (V)       | 2                 | `intercellSpacing.height`      |

### Inset Style Margins

| Property                    | Value (pt) |
|-----------------------------|------------|
| Row inset (left/right)       | 10         |
| Selection corner radius      | 6          |
| Content padding (horizontal) | 6          |
| Content padding (vertical)   | 2          |

### Source List Style

| Property                    | Value (pt) |
|-----------------------------|------------|
| Row inset (left/right)       | 10         |
| Selection corner radius      | 6          |
| Group row height             | 28         |
| Group row top padding        | 8          |
| Indentation per level        | 16         |
| Disclosure triangle size     | 10         |
| Icon to text gap             | 6          |

## Colors

### Backgrounds

| Element                        | Light Mode            | Dark Mode             |
|--------------------------------|-----------------------|-----------------------|
| Table background               | `#FFFFFF`             | `#1E1E1E`             |
| Alternating row (even)         | `#FFFFFF`             | `#1E1E1E`             |
| Alternating row (odd)          | `#F4F5F5`             | `#232323`             |
| Source list background         | Vibrancy (sidebar material) | Vibrancy (sidebar material) |
| Source list fallback           | `#F6F6F6`             | `#2D2D2D`             |

### Selection

| State                          | Light Mode            | Dark Mode             |
|--------------------------------|-----------------------|-----------------------|
| Selected row (focused)         | `#0063E1`             | `#0058D0`             |
| Selected row (unfocused)       | `#DCDCDC`             | `#464646`             |
| Selected text (focused)        | `#FFFFFF`             | `#FFFFFF`             |
| Selected text (unfocused)      | labelColor            | labelColor            |
| Source list selected (focused) | controlAccentColor with vibrancy | controlAccentColor with vibrancy |
| Source list selected (unfocused)| `rgba(0,0,0,0.06)`  | `rgba(255,255,255,0.08)` |

### Column Header

| Element                        | Light Mode              | Dark Mode               |
|--------------------------------|-------------------------|-------------------------|
| Header background              | `rgba(0,0,0,0.04)`     | `rgba(255,255,255,0.04)`|
| Header text                    | secondaryLabelColor     | secondaryLabelColor     |
| Header separator               | separatorColor          | separatorColor          |
| Sort indicator                 | secondaryLabelColor     | secondaryLabelColor     |

### Grid Lines

| Element                        | Light Mode              | Dark Mode               |
|--------------------------------|-------------------------|-------------------------|
| Horizontal grid                | `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.08)`|
| Vertical grid                  | `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.08)`|

## States

### Row States

| State           | Visual Changes                                        |
|-----------------|------------------------------------------------------|
| Normal          | Default background (or alternating color)             |
| Hover           | Subtle highlight (iOS-like, macOS 14+)                |
| Selected        | Accent color fill (focused) or gray fill (unfocused)  |
| Dragging        | Semi-transparent row snapshot                          |
| Drop target     | Blue line indicator at insertion point                 |
| Editing         | Cell becomes editable text field                       |
| Disabled row    | Dimmed text, no selection                              |

### Group Row (NSOutlineView)

| State           | Visual Changes                                        |
|-----------------|------------------------------------------------------|
| Normal          | Bold uppercase text, no background                    |
| Collapsed       | Disclosure triangle points right                      |
| Expanded        | Disclosure triangle points down                       |

## Typography

| Element                  | Font Size (pt) | Weight      |
|--------------------------|----------------|-------------|
| Cell text                | 13 (body)      | Regular     |
| Cell secondary text      | 11             | Regular     |
| Column header text       | 11             | Semibold    |
| Source list group header  | 11             | Bold        |
| Source list item          | 13             | Regular     |
| Source list selected item | 13             | Regular     |

## Disclosure Triangle (NSOutlineView)

| Property              | Value          |
|-----------------------|----------------|
| Size                  | 10x10 pt       |
| Color                 | tertiaryLabelColor |
| Collapsed direction   | Right-pointing  |
| Expanded direction    | Down-pointing   |
| Animation duration    | 150 ms          |
| Animation curve       | Ease In Out     |

## Column Resizing

| Behavior                 | Description                                  |
|--------------------------|----------------------------------------------|
| User resize              | Drag column header edge                      |
| Auto resize all columns  | `.uniformColumnAutoresizingStyle`            |
| Resize last column       | `.lastColumnOnlyAutoresizingStyle`           |
| Resize first column      | `.firstColumnOnlyAutoresizingStyle`          |
| No auto resize           | `.noColumnAutoresizing`                      |
| Sequential auto resize   | `.sequentialColumnAutoresizingStyle`         |

## Drag and Drop

| Element                  | Description                                  |
|--------------------------|----------------------------------------------|
| Drag threshold           | 4 pt mouse movement before drag starts       |
| Drag preview             | Semi-transparent row snapshot at 70% opacity  |
| Drop indicator           | 2 pt blue line at insertion point             |
| Drop highlight (on row)  | Blue outline around target row                |
| Drop feedback (between)  | Blue line with circle at left edge            |
| Spring-loading delay     | 500 ms hover before auto-expand              |

## Scroll Behavior

| Property                | Value                                        |
|-------------------------|----------------------------------------------|
| Elastic overscroll      | Yes (rubber band)                            |
| Scroll indicators       | Overlay, auto-hide (system preference)       |
| Scroll bar width        | 6 pt collapsed, 8 pt hover                  |
| Scroll bar inset        | 2 pt from edge                               |

## Animation

| Transition                   | Duration (ms) | Curve          |
|------------------------------|---------------|----------------|
| Row insert                   | 250           | Ease In Out    |
| Row delete                   | 250           | Ease In Out    |
| Row move                     | 250           | Ease In Out    |
| Selection change             | 100           | Ease Out       |
| Disclosure expand/collapse   | 150           | Ease In Out    |
| Column resize                | 0             | Immediate      |
| Scroll deceleration          | varies        | Ease Out       |

## Keyboard Interaction

| Key                  | Action                                    |
|---------------------|-------------------------------------------|
| Up Arrow            | Move selection up one row                  |
| Down Arrow          | Move selection down one row                |
| Cmd+Up              | Select first row                           |
| Cmd+Down            | Select last row                            |
| Shift+Up/Down       | Extend selection                           |
| Cmd+Click           | Toggle row selection                       |
| Shift+Click         | Extend selection to clicked row            |
| Return              | Begin editing selected cell                |
| Delete              | Delete selected row (if supported)         |
| Right Arrow         | Expand disclosure (NSOutlineView)          |
| Left Arrow          | Collapse disclosure (NSOutlineView)        |
| Space               | Quick Look preview (if supported)          |
| Cmd+A               | Select all rows                            |
| Tab                 | Move to next column (editing mode)         |

## Dija Skin Mapping

```
comp! Table {
    attr style, TableStyle, default: TableStyle::Inset
    attr alternating, bool, default: true
    attr headers, bool, default: true
    attr grid_lines, GridLines, default: GridLines::None

    // macOS skin maps:
    // TableStyle::FullWidth  -> .fullWidth (no inset selection)
    // TableStyle::Inset      -> .inset (rounded selection, 10 pt margins)
    // TableStyle::SourceList -> .sourceList (vibrancy background)
    //
    // Row height: 24 pt default
    // Selection: accent-colored rounded rect in inset mode
    // Headers: 24 pt with secondary label color text
}
```
