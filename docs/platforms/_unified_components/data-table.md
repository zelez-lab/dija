# Data Table

A multi-column table with sortable column headers, displaying structured data in rows and columns. Supports column resizing, row selection, and alternating row styles.

| Platform | Native Component | Status |
|---|---|---|
| iOS | (Use List View for single-column lists) | N/A |
| macOS | NSTableView (multi-column) / NSOutlineView | Documented |
| Android | (No built-in M3 data table; use custom or third-party) | Minimal |
| Windows | WinUI 3 DataGrid (community) | Documented |
| Linux | GtkColumnView (GNOME/Adwaita) | Documented |

---

## macOS

Reference: NSTableView (multi-column mode), NSOutlineView, Apple HIG (macOS 14+).

### Overview

`NSTableView` displays data in rows and columns. `NSOutlineView` is a subclass that adds hierarchical disclosure (tree structure). Since macOS 11 Big Sur, tables have adopted a more modern appearance with rounded selection highlights, increased row heights, and inset content.

### Table Styles

| Style             | Description                                                 | Usage                      |
|-------------------|-------------------------------------------------------------|----------------------------|
| `.automatic`      | System picks based on context                                | Default                    |
| `.fullWidth`      | Selection extends full width of table, no inset              | Dense data tables          |
| `.inset`          | Selection has rounded corners, inset from edges              | Settings, preferences      |

### Column Metrics

| Property                    | Default Value (pt) | Notes                          |
|-----------------------------|-------------------|--------------------------------|
| Minimum column width         | 40                | `minWidth` property            |
| Default column width         | 100               | `width` property               |
| Column header height         | 24                | Standard header row            |
| Column resize handle width   | 6                 | Draggable area at edge         |
| Inter-cell spacing (H)       | 3                 | `intercellSpacing.width`       |
| Inter-cell spacing (V)       | 2                 | `intercellSpacing.height`      |

### Row Heights

| Configuration           | Row Height (pt) | Notes                              |
|------------------------|-----------------|-------------------------------------|
| Default                 | 24              | Standard single-line row            |
| Large row height        | 34              | Rows with subtitle or icon          |
| Custom                  | User-defined    | Via delegate `heightOfRow()`        |

### Colors

#### Backgrounds

| Element                        | Light Mode            | Dark Mode             |
|--------------------------------|-----------------------|-----------------------|
| Table background               | `#FFFFFF`             | `#1E1E1E`             |
| Alternating row (even)         | `#FFFFFF`             | `#1E1E1E`             |
| Alternating row (odd)          | `#F4F5F5`             | `#232323`             |

#### Selection

| State                          | Light Mode            | Dark Mode             |
|--------------------------------|-----------------------|-----------------------|
| Selected row (focused)         | `#0063E1`             | `#0058D0`             |
| Selected row (unfocused)       | `#DCDCDC`             | `#464646`             |
| Selected text (focused)        | `#FFFFFF`             | `#FFFFFF`             |
| Selected text (unfocused)      | labelColor            | labelColor            |

#### Column Header

| Element                        | Light Mode              | Dark Mode               |
|--------------------------------|-------------------------|-------------------------|
| Header background              | `rgba(0,0,0,0.04)`     | `rgba(255,255,255,0.04)`|
| Header text                    | secondaryLabelColor     | secondaryLabelColor     |
| Header separator               | separatorColor          | separatorColor          |
| Sort indicator                 | secondaryLabelColor     | secondaryLabelColor     |

#### Grid Lines

| Element                        | Light Mode              | Dark Mode               |
|--------------------------------|-------------------------|-------------------------|
| Horizontal grid                | `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.08)`|
| Vertical grid                  | `rgba(0,0,0,0.08)`     | `rgba(255,255,255,0.08)`|

### States

| State           | Visual Changes                                        |
|-----------------|------------------------------------------------------|
| Normal          | Default background (or alternating color)             |
| Hover           | Subtle highlight (macOS 14+)                          |
| Selected        | Accent color fill (focused) or gray fill (unfocused)  |
| Dragging        | Semi-transparent row snapshot                          |
| Drop target     | Blue line indicator at insertion point                 |
| Editing         | Cell becomes editable text field                       |
| Disabled row    | Dimmed text, no selection                              |

### Typography

| Element                  | Font Size (pt) | Weight      |
|--------------------------|----------------|-------------|
| Cell text                | 13 (body)      | Regular     |
| Cell secondary text      | 11             | Regular     |
| Column header text       | 11             | Semibold    |

### Column Resizing

| Behavior                 | Description                                  |
|--------------------------|----------------------------------------------|
| User resize              | Drag column header edge                      |
| Auto resize all columns  | `.uniformColumnAutoresizingStyle`            |
| Resize last column       | `.lastColumnOnlyAutoresizingStyle`           |
| Resize first column      | `.firstColumnOnlyAutoresizingStyle`          |
| No auto resize           | `.noColumnAutoresizing`                      |
| Sequential auto resize   | `.sequentialColumnAutoresizingStyle`         |

### Drag and Drop

| Element                  | Description                                  |
|--------------------------|----------------------------------------------|
| Drag threshold           | 4 pt mouse movement before drag starts       |
| Drag preview             | Semi-transparent row snapshot at 70% opacity  |
| Drop indicator           | 2 pt blue line at insertion point             |
| Drop highlight (on row)  | Blue outline around target row                |
| Drop feedback (between)  | Blue line with circle at left edge            |
| Spring-loading delay     | 500 ms hover before auto-expand              |

### Animation

| Transition                   | Duration (ms) | Curve          |
|------------------------------|---------------|----------------|
| Row insert                   | 250           | Ease In Out    |
| Row delete                   | 250           | Ease In Out    |
| Row move                     | 250           | Ease In Out    |
| Selection change             | 100           | Ease Out       |
| Disclosure expand/collapse   | 150           | Ease In Out    |
| Column resize                | 0             | Immediate      |

### Keyboard Interaction

| Key                  | Action                                    |
|---------------------|-------------------------------------------|
| Up Arrow            | Move selection up one row                  |
| Down Arrow          | Move selection down one row                |
| Cmd+Up              | Select first row                           |
| Cmd+Down            | Select last row                            |
| Shift+Up/Down       | Extend selection                           |
| Return              | Begin editing selected cell                |
| Delete              | Delete selected row (if supported)         |
| Right Arrow         | Expand disclosure (NSOutlineView)          |
| Left Arrow          | Collapse disclosure (NSOutlineView)        |
| Tab                 | Move to next column (editing mode)         |
| Cmd+A               | Select all rows                            |

### Dija Skin Mapping

```
comp! DataTable {
    attr style, TableStyle, default: TableStyle::Inset
    attr alternating, bool, default: true
    attr headers, bool, default: true
    attr grid_lines, GridLines, default: GridLines::None

    // macOS skin maps:
    // TableStyle::FullWidth  -> .fullWidth (no inset selection)
    // TableStyle::Inset      -> .inset (rounded selection, 10 pt margins)
    //
    // Row height: 24 pt default
    // Selection: accent-colored rounded rect in inset mode
    // Headers: 24 pt with secondary label color text
}
```

---

## Windows

Source: WinUI 3 DataGrid (community)

WinUI 3 does not ship a built-in DataGrid. Community implementations follow these conventions:

### Column Header

| Property | Value |
|----------|-------|
| Height | 32px |
| Padding | 12px horizontal |
| Font | 12px Caption, Regular |
| Color | TextFillColorSecondary |
| Background | Transparent |
| Sort indicator | Chevron glyph, 8px |
| Separator | 1px DividerStrokeColorDefault between columns |
| Resize handle | 1px wide, full height, on hover shows resize cursor |

### Data Row

| Property | Value |
|----------|-------|
| Height | 40px (standard), 32px (compact) |
| Padding | 12px horizontal per cell |
| Font | 14px, Regular |
| Hover | SubtleFillColorSecondary (full row) |
| Selected | SubtleFillColorSecondary + left accent pill |
| Alternating rows | Optional, uses SubtleFillColorSecondary for even rows |
| Row separator | 1px DividerStrokeColorDefault |

### Scrollbar

| Property | Value |
|----------|-------|
| Width (collapsed) | 2px |
| Width (expanded, on hover) | 6px |
| Corner radius | Fully rounded |
| Thumb color | ControlStrongFillColorDefault |
| Track color | Transparent |
| Hover: thumb color | ControlStrongFillColorDefault (increased opacity) |

---

## Linux

Source: GTK 4 (docs.gtk.org/gtk4), libadwaita

### GtkColumnView (Data Table)

#### Header

| Property | Light | Dark |
|----------|-------|------|
| Background | transparent | transparent |
| Text color | dim-label (secondary) | dim-label |
| Font | Adwaita Sans Bold, 13px (.caption-heading) | -- |
| Height | 32px | 32px |
| Bottom border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Sort indicator | Arrow icon, 12px | Arrow icon |
| Resizable columns | Drag handle at column edge | -- |

#### Column Separators

| Property | Value |
|----------|-------|
| Between columns | 1px `rgba(0,0,0, 0.08)` (optional) |
| Between rows | 1px `rgba(0,0,0, 0.15)` (when `.separators` class applied) |

#### Cells

| Property | Value |
|----------|-------|
| Padding | 8px 12px |
| Font | Adwaita Sans Regular, 15px |
| Min-height | 34px |
| Alignment | Left (text), Right (numbers) |

#### Selection

| Property | Light | Dark |
|----------|-------|------|
| Selected row bg | `rgba(0,0,0, 0.06)` | `rgba(255,255,255, 0.06)` |
| Selected + hover | `rgba(0,0,0, 0.10)` | `rgba(255,255,255, 0.10)` |
| Selection indicator | Accent-colored left bar (optional) | -- |
| Multi-select | Click + Ctrl (toggle), Click + Shift (range) | -- |
| Rubberband | Accent color @ 0.2, with 1px accent border | -- |

### Focus and Keyboard

| Key | Action |
|-----|--------|
| Up / Down | Move selection |
| Space / Enter | Activate row |
| Ctrl+A | Select all (multi-select) |
| Escape | Clear selection |
| Home / End | Jump to first / last |
| Page Up / Page Down | Scroll by page |
