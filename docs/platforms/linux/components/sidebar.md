# Linux (GNOME/Adwaita) — Sidebar (AdwNavigationSplitView)

## Overview

libadwaita provides multiple sidebar/split-view patterns:

| Widget | Behavior |
|--------|----------|
| `AdwNavigationSplitView` | Sidebar + content, collapses to navigation stack |
| `AdwOverlaySplitView` | Sidebar overlays content on narrow windows |
| `AdwNavigationView` | Stack-based navigation (push/pop pages) |

## AdwNavigationSplitView

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Sidebar background | `#EBEBEB` (sidebar_bg_color) | `#303030` |
| Sidebar backdrop | `#F2F2F2` (sidebar_backdrop_color) | `#2A2A2A` |
| Content background | `#FAFAFA` (window_bg_color) | `#242424` |
| Separator (between panes) | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |

### Metrics

| Property | Value |
|----------|-------|
| Sidebar width (fraction) | 25% of total window width |
| Sidebar min-width | 180px |
| Sidebar max-width | 280px |
| Width unit | `sp` (scale-independent pixels) |
| Sidebar padding | 0px (content fills edge-to-edge) |
| Content padding | 0px (up to content widgets) |

### Adaptive Behavior

| Window Width | Layout |
|-------------|--------|
| >= sidebar min + content min (~460px) | Side-by-side (split view) |
| < breakpoint | Collapsed (navigation stack) |

When collapsed:
- Sidebar becomes a full-width page
- Selecting an item pushes the content page
- Back button appears in content header bar
- Transition: slide from right (400ms, ease-in-out-cubic)

## Sidebar Content

The sidebar typically contains a `GtkListBox` with `.navigation-sidebar` style:

### Navigation Sidebar Row

| Property | Light | Dark |
|----------|-------|------|
| Background (rest) | transparent | transparent |
| Background (hover) | `rgba(0,0,0, 0.04)` | `rgba(255,255,255, 0.04)` |
| Background (selected) | `--accent-bg-color` @ 0.12 | `--accent-bg-color` @ 0.12 |
| Background (selected + hover) | `--accent-bg-color` @ 0.18 | `--accent-bg-color` @ 0.18 |
| Text color (rest) | window_fg_color | window_fg_color |
| Text color (selected) | `--accent-color` | `--accent-color` |
| Corner radius | 6px | 6px |
| Margin (horizontal) | 6px | 6px |
| Padding | 8px 12px | 8px 12px |
| Min-height | 34px | 34px |

### Row Layout

```
+---+------+---+------------------------------------+---+-----+
| M | Icon | G |           Title                    | G | Badge|
+---+------+---+------------------------------------+---+-----+
 ^    16px  8px              15px                     8px
 6px margin
```

| Element | Size | Notes |
|---------|------|-------|
| Icon (prefix) | 16x16px | Optional |
| Icon-to-title gap | 8px | — |
| Title font | 15px, Regular | — |
| Badge/count (suffix) | `.caption` size, accent bg | Optional |

## AdwOverlaySplitView

### Differences from NavigationSplitView

| Property | NavigationSplitView | OverlaySplitView |
|----------|-------------------|-----------------|
| Collapsed mode | Stack navigation | Sidebar overlays content |
| Animation | Page push/pop | Slide from edge |
| Content visibility | Replaced by sidebar | Dimmed under sidebar |
| Use case | Primary navigation | Secondary/optional panel |

### Overlay Metrics

| Property | Value |
|----------|-------|
| Sidebar shadow (when overlay) | (4, 0) blur 12, black @ 0.15 |
| Content dim (when overlay) | black @ 0.20 |
| Sidebar slide direction | From left (LTR) or right (RTL) |
| Transition duration | 400ms |
| Transition easing | ease-in-out-cubic |

## Sidebar Header Bar

The sidebar pane has its own header bar:

| Property | Value |
|----------|-------|
| Height | Same as main header bar (47px) |
| Background | Same as sidebar_bg_color |
| Title | App name or section name |
| Window controls | Start side only (or none if right side) |
| Bottom border | 1px separator (same as main header bar) |

When collapsed, the sidebar header bar becomes the main header bar with a
hamburger menu or back navigation.

## Common Sidebar Patterns

### Settings Sidebar

```
Navigation Sidebar:
  +-- General
  +-- Appearance
  +-- Notifications
  +-- Privacy
  +-- ...
```

### Mail/Chat Sidebar

```
Navigation Sidebar:
  +-- Inbox        [42]
  +-- Starred
  +-- Sent
  +-- Drafts       [3]
  +-- Trash
```

### File Manager Sidebar

```
Navigation Sidebar:
  +-- Home
  +-- Documents
  +-- Downloads
  +-- Pictures
  +-- ---separator---
  +-- Trash
  +-- Other Locations
```

## Keyboard Support

| Key | Action |
|-----|--------|
| Up / Down | Navigate sidebar items |
| Enter | Select item, show content |
| Alt+Left | Go back (when collapsed) |
| F9 | Toggle sidebar visibility |
| Ctrl+F | Search (if sidebar has search) |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Sidebar collapse | 400ms | ease-in-out-cubic |
| Sidebar expand | 400ms | ease-in-out-cubic |
| Page push (collapsed) | 400ms | ease-in-out-cubic |
| Page pop (collapsed) | 400ms | ease-in-out-cubic |
| Overlay show | 400ms | ease-in-out-cubic |
| Overlay dismiss | 400ms | ease-in-out-cubic |
| Overlay dim fade | 400ms | ease-in-out |
| Sidebar row select | immediate | — |
