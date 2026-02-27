# Linux (GNOME/Adwaita) — Table View (GtkListBox / GtkColumnView)

## Overview

GNOME provides multiple list/table widgets:

| Widget | Usage |
|--------|-------|
| `GtkListBox` | Simple vertical list of rows |
| `GtkListView` | Scalable list with recycling (for large datasets) |
| `GtkColumnView` | Multi-column table with headers (data tables) |
| `GtkGridView` | Grid of items (icon grid) |

## GtkListBox (Simple List)

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | transparent (inherits parent) | transparent |
| Row background (rest) | transparent | transparent |
| Row background (hover) | `rgba(0,0,0, 0.04)` | `rgba(255,255,255, 0.04)` |
| Row background (active) | `rgba(0,0,0, 0.08)` | `rgba(255,255,255, 0.08)` |
| Row background (selected) | `rgba(0,0,0, 0.06)` | `rgba(255,255,255, 0.06)` |
| Separator | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Selection mode | Single / Multiple / None | — |

### Metrics

| Property | Value |
|----------|-------|
| Row min-height | 34px |
| Row padding | 8px 12px |
| Separator height | 1px |
| Corner radius (if boxed-list) | 12px |

### Boxed List Style

Adding `.boxed-list` to a GtkListBox wraps it in a card:

| Property | Value |
|----------|-------|
| Container border | 1px `rgba(0,0,0, 0.12)` |
| Container radius | 12px |
| Container shadow | (0,1) blur 3, black @ 0.06 |
| Container background | card_bg_color |
| Row separator | full-width, inside card |
| First/last row | radius matches card corners |

## GtkColumnView (Data Table)

### Header

| Property | Light | Dark |
|----------|-------|------|
| Background | transparent | transparent |
| Text color | dim-label (secondary) | dim-label |
| Font | Adwaita Sans Bold, 13px (.caption-heading) | — |
| Height | 32px | 32px |
| Bottom border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Sort indicator | Arrow icon, 12px | Arrow icon |
| Resizable columns | Drag handle at column edge | — |

### Column Separators

| Property | Value |
|----------|-------|
| Between columns | 1px `rgba(0,0,0, 0.08)` (optional) |
| Between rows | 1px `rgba(0,0,0, 0.15)` (when `.separators` class applied) |

### Cells

| Property | Value |
|----------|-------|
| Padding | 8px 12px |
| Font | Adwaita Sans Regular, 15px |
| Min-height | 34px |
| Alignment | Left (text), Right (numbers) |

### Selection

| Property | Light | Dark |
|----------|-------|------|
| Selected row bg | `rgba(0,0,0, 0.06)` | `rgba(255,255,255, 0.06)` |
| Selected + hover | `rgba(0,0,0, 0.10)` | `rgba(255,255,255, 0.10)` |
| Selection indicator | Accent-colored left bar (optional) | — |
| Multi-select | Click + Ctrl (toggle), Click + Shift (range) | — |
| Rubberband | Accent color @ 0.2, with 1px accent border | — |

## Row Types (for Boxed Lists)

libadwaita provides specialized row types:

### AdwActionRow

| Property | Value |
|----------|-------|
| Title | 15px, Regular |
| Subtitle | 13px, dim-label |
| Prefix | Icon or widget, 12px left margin |
| Suffix | Widget (switch, button, arrow), 12px right margin |
| Activatable | Entire row clickable |
| Min-height | 50px (with subtitle), 34px (title only) |

### AdwSwitchRow

| Property | Value |
|----------|-------|
| Layout | Title + subtitle on left, GtkSwitch on right |
| Toggle on click | Yes (entire row toggles switch) |

### AdwComboRow

| Property | Value |
|----------|-------|
| Layout | Title + subtitle on left, dropdown on right |
| Dropdown style | Shows current value + chevron icon |
| Popover | Standard popover with list of options |

### AdwExpanderRow

| Property | Value |
|----------|-------|
| Layout | Title + expander arrow |
| Arrow position | Right side |
| Animation | 250ms ease-in-out collapse/expand |
| Nested content | Indented child rows |

## Navigation Sidebar Style

Adding `.navigation-sidebar` to a GtkListBox:

| Property | Value |
|----------|-------|
| Row background (selected) | `--accent-bg-color` @ 0.12 |
| Row corner radius | 6px |
| Row margin | 6px horizontal |
| Row padding | 8px 12px |
| Row min-height | 34px |
| Row icon | 16px, 8px margin right |

## Rich List Style

Adding `.rich-list` to a GtkListBox:

| Property | Value |
|----------|-------|
| Row padding | 12px (increased from 8px) |
| Row min-height | 50px |
| Used for | Settings rows with larger touch targets |

## Focus and Keyboard

| Key | Action |
|-----|--------|
| Up / Down | Move selection |
| Space / Enter | Activate row |
| Ctrl+A | Select all (multi-select) |
| Escape | Clear selection |
| Home / End | Jump to first / last |
| Page Up / Page Down | Scroll by page |
| Type-ahead | Jump to matching row |

## Scrolling

| Property | Value |
|----------|-------|
| Scroll widget | GtkScrolledWindow wrapping the list |
| Scrollbar style | Overlay (appears on hover/scroll) |
| Scrollbar width | 8px (hover: 12px) |
| Kinetic scrolling | Enabled on touch |
| Overshoot | Elastic bounce indicator |
