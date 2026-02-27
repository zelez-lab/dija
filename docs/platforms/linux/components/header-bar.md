# Linux (GNOME/Adwaita) — Header Bar (AdwHeaderBar)

## Overview

AdwHeaderBar is the defining UI element of GNOME applications. It replaces both the
OS title bar and toolbar, providing CSD (client-side decorations) with integrated
window controls.

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#EBEBEB` (headerbar_bg_color) | `#303030` |
| Backdrop (unfocused) | `#FAFAFA` (window_bg_color) | `#242424` |
| Text color | `#2E3436` | `#FFFFFF` |
| Bottom border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Top corners | 12px (matches window CSD) | 12px |
| Top corners (maximized) | 0px | 0px |

## Metrics

| Property | Value |
|----------|-------|
| Min height | 47px |
| Horizontal padding | 6px |
| Widget spacing | 6px |
| Title area | Centered, between start/end widgets |
| Window controls size | 24px icons |
| Window controls spacing | 6px |

## Layout

```
+---+------+---+---------------------+---+------+---+
| P | [Btn] | S |       Title        | S | [Btn]| C |
+---+------+---+---------------------+---+------+---+
 ^                    ^                          ^
 6px padding     Centered title              6px padding
```

- **Start area**: Left-aligned buttons and widgets
- **Center area**: Title widget (text, view switcher, or custom)
- **End area**: Right-aligned buttons and widgets
- **Window controls**: Close, minimize, maximize (configurable position)

## Window Controls

Position determined by `org.gnome.desktop.wm.preferences button-layout`:

| Layout String | Result |
|--------------|--------|
| `close,minimize,maximize:` | Controls on left (macOS-like) |
| `:minimize,maximize,close` | Controls on right (default) |
| `close:` | Close only, on left |
| `:close` | Close only, on right |
| (empty) | No window controls |

### Button Sizes

| Button | Icon Size | Hit Area |
|--------|-----------|----------|
| Close | 16px | 24x24px |
| Minimize | 16px | 24x24px |
| Maximize | 16px | 24x24px |

### Close Button

| State | Light | Dark |
|-------|-------|------|
| Rest | transparent (flat) | transparent |
| Hover | `rgba(224,27,36, 0.15)` (red tint) | `rgba(224,27,36, 0.15)` |
| Active | `rgba(224,27,36, 0.30)` | `rgba(224,27,36, 0.30)` |

The close button has a distinctive red hover state, unlike other window controls.

## Title

### Text Title (Default)

| Property | Value |
|----------|-------|
| Font | Adwaita Sans Bold, 15px |
| Alignment | Centered in available space |
| Ellipsis | Truncate with "..." when no space |

### Title + Subtitle

| Property | Value |
|----------|-------|
| Title font | Adwaita Sans Bold, 15px |
| Subtitle font | Adwaita Sans Regular, 13px, dim-label |
| Subtitle color | secondary (dim) |
| Vertical stacking | Title above, subtitle below |

### Custom Title Widget

The title area can be replaced with any widget:

| Common replacements | Widget |
|--------------------|--------|
| View switcher | `AdwViewSwitcher` (tabs in header) |
| Search entry | `GtkSearchEntry` (search mode) |
| Custom combo | `GtkDropDown` |
| Breadcrumbs | Custom widget |

## Header Bar Variants

### Default (.toolbar Style)

All header bars automatically get the `.toolbar` appearance:

| Property | Value |
|----------|-------|
| Inner buttons | Flat style by default |
| Button padding | 8px 10px |
| Button min-size | 34px |

### Flat Header Bar

Adding `.flat` removes the bottom border and makes the header bar blend with content:

| Property | Value |
|----------|-------|
| Background | transparent (inherits window bg) |
| Bottom border | none |
| Usage | Single-view apps, content-heavy layouts |

### Development Style

Adding `.devel` adds a striped pattern for development/nightly builds:

| Property | Value |
|----------|-------|
| Background | Diagonal stripes overlay |
| Usage | Development builds, nightly apps |

## Backdrop Behavior

When the window loses focus:

| Property | Focused | Unfocused (Backdrop) |
|----------|---------|---------------------|
| Background | headerbar_bg_color | window_bg_color |
| Text opacity | 1.0 | 1.0 (text remains readable) |
| Button opacity | 1.0 | subtly reduced |
| Transition | — | 200ms ease-in-out |

## Integration with Content

The header bar is typically the first child of `AdwToolbarView`:

```
AdwToolbarView
 +-- AdwHeaderBar (top-bar)
 +-- Content (scrollable)
 +-- [Bottom bar] (optional)
```

| Property | Value |
|----------|-------|
| Top bar mode | `ADW_TOOLBAR_FLAT` or `ADW_TOOLBAR_RAISED` |
| Raised mode | Adds bottom shadow when content is scrolled |
| Raised border | Replaces static border with scroll-dependent shadow |

## Keyboard Support

| Key | Action |
|-----|--------|
| Alt+F4 | Close window |
| Super+Up | Maximize |
| Super+Down | Restore/minimize |
| Alt+Space | Window menu |
| F11 | Fullscreen toggle |

## Drag Behavior

| Action | Effect |
|--------|--------|
| Drag on empty header bar area | Move window |
| Double-click on header bar | Maximize / restore |
| Right-click on header bar | Window context menu |
| Middle-click on header bar | Lower window (configurable) |

## Fullscreen and Maximized

| State | Header Bar Changes |
|-------|--------------------|
| Normal | 12px top corners, full controls |
| Maximized | 0px top corners, full controls |
| Tiled (half screen) | 0px on tiled edge, 12px on free edge |
| Fullscreen | Header bar auto-hides, revealed on mouse hover at top |
