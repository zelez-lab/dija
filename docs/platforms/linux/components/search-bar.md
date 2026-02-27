# Linux (GNOME/Adwaita) — Search Bar (GtkSearchBar / GtkSearchEntry)

## Overview

GNOME provides two search-related widgets:

| Widget | Role |
|--------|------|
| `GtkSearchBar` | Container that reveals/hides a search entry in the toolbar area |
| `GtkSearchEntry` | The actual text input with search icon and clear button |

## GtkSearchBar

### Appearance

The search bar is a toolbar-height container that slides down below the header bar
when search mode is activated.

| Property | Light | Dark |
|----------|-------|------|
| Background | Same as header bar (`#EBEBEB`) | `#303030` |
| Bottom border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Style | `.toolbar` (inherits toolbar appearance) | — |

### Metrics

| Property | Value |
|----------|-------|
| Height | 47px (same as header bar) |
| Padding | 6px horizontal, 6px vertical |
| Entry max-width | 400px (centered in bar) |

### Reveal Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Reveal (slide down) | 250ms | ease-out-cubic |
| Hide (slide up) | 200ms | ease-in-cubic |

## GtkSearchEntry

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#FFFFFF` (view_bg_color) | `#1E1E1E` |
| Text color | `#2E3436` | `#FFFFFF` |
| Placeholder color | `rgba(46,52,54, 0.50)` | `rgba(255,255,255, 0.50)` |
| Border (rest) | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Border (focused) | 2px `--accent-color` | 2px `--accent-color` |
| Corner radius | 6px | 6px |
| Shadow | none | none |

### Metrics

| Property | Value |
|----------|-------|
| Min height | 34px |
| Horizontal padding | 12px |
| Vertical padding | 8px |
| Corner radius | 6px |
| Font | Adwaita Sans Regular, 15px |

### Icons

| Position | Icon | Size | Behavior |
|----------|------|------|----------|
| Prefix (left) | Search (magnifying glass) | 16x16px | Static, always visible |
| Suffix (right) | Clear (X circle) | 16x16px | Visible only when text present |

### Clear Button

| Property | Value |
|----------|-------|
| Icon | `edit-clear-symbolic` (X in circle) |
| Size | 16x16px |
| Hit area | 24x24px |
| Style | Flat, transparent until hover |
| Hover bg | `rgba(0,0,0, 0.07)` |
| Active bg | `rgba(0,0,0, 0.12)` |
| Corner radius | 50% (circular) |

## States

| State | Border | Background | Notes |
|-------|--------|------------|-------|
| Rest | 1px, `rgba(0,0,0,0.15)` | view_bg_color | — |
| Hover | 1px, `rgba(0,0,0,0.25)` | view_bg_color | Stronger border |
| Focused | 2px, accent_color | view_bg_color | Accent highlight |
| Has text | same as rest/focused | view_bg_color | Clear button visible |
| Empty + unfocused | 1px border | view_bg_color | Placeholder visible |
| Disabled | 1px, `rgba(0,0,0,0.10)` | `rgba(0,0,0,0.04)` | Opacity 0.5 |

## Inline Search (within header bar)

The search entry can be placed directly in the header bar as the title widget:

| Property | Value |
|----------|-------|
| Position | Center of header bar (replaces title) |
| Max width | Expands to available space |
| Entry style | Same as standalone |
| Toggle | Search icon button activates/deactivates |

## Search Behavior

| Feature | Detail |
|---------|--------|
| Auto-search | Typing starts after a delay (150ms debounce) |
| search-changed signal | Fires on each keystroke (after debounce) |
| Stop search signal | Fires on Escape |
| Activate signal | Fires on Enter (select first result) |
| Min characters | Typically 1 (app configurable) |
| Capture | `GtkSearchBar` captures key events from its key-capture-widget |

### Key Capture

`GtkSearchBar` has a `key-capture-widget` property (typically the window). When set,
typing anywhere in the window activates the search bar and forwards keystrokes:

| Behavior | Detail |
|----------|--------|
| Typing starts search | First printable character opens search bar |
| Escape closes search | Hides search bar, clears entry |
| Focus returns | Focus returns to previous widget after closing |

## Keyboard Support

| Key | Action |
|-----|--------|
| Ctrl+F | Toggle search bar (convention) |
| Escape | Close search bar, clear entry |
| Enter | Activate / select first result |
| Type any character | Auto-open search bar (with key capture) |
| Ctrl+A | Select all text in entry |
| Backspace (empty) | Close search bar |

## Search Suggestions / Results

GNOME does not have a built-in search suggestions dropdown. Apps implement their
own results display, typically:

| Pattern | Description |
|---------|-------------|
| Filtered list | `GtkListBox` below search bar, rows filter in real time |
| Column view | `GtkColumnView` filters, showing matching rows |
| Status page | `AdwStatusPage` shown when no results |

### No Results State

| Property | Value |
|----------|-------|
| Icon | `system-search-symbolic`, 48px |
| Title | "No Results Found" |
| Subtitle | "Try a different search term" |
| Widget | `AdwStatusPage` |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Search bar reveal | 250ms | ease-out-cubic |
| Search bar hide | 200ms | ease-in-cubic |
| Clear button appear | 150ms | ease-out |
| Clear button disappear | 100ms | ease-in |
| Border focus transition | 200ms | ease-in-out |
| Placeholder fade | 150ms | ease-in-out |
