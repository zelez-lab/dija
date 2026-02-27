# macOS Surfaces & Vibrancy

Reference: NSVisualEffectView, NSAppearance, Apple Human Interface Guidelines (macOS 14+).

## Overview

macOS achieves its layered, translucent look through **vibrancy** -- a system where foreground content (text, icons, fills) blends with the content behind a translucent surface. This is powered by `NSVisualEffectView`, which composites a material effect behind your content.

Vibrancy is NOT just blur. It is a compositing pipeline:
1. Background content is captured and blurred
2. A tint/saturation layer is applied (the "material")
3. Foreground content is drawn with special blend modes that pull color from behind

## NSVisualEffectView Materials

Each material is tuned for a specific UI context. Materials automatically adapt between light and dark appearances.

### Material Enum Values

| Material                | Raw Value | Introduced | Description                                           |
|-------------------------|-----------|------------|-------------------------------------------------------|
| `.titlebar`             | 3         | 10.10      | Window title bar background                           |
| `.selection`            | 4         | 10.10      | Selected row/cell in tables                           |
| `.menu`                 | 5         | 10.10      | Menu and context menu background                      |
| `.popover`              | 6         | 10.10      | Popover background                                    |
| `.sidebar`              | 7         | 10.10      | Source list / sidebar background                      |
| `.headerView`           | 10        | 10.14      | Table header view                                     |
| `.sheet`                | 11        | 10.14      | Sheet background                                      |
| `.windowBackground`     | 12        | 10.14      | General window background                             |
| `.hudWindow`            | 13        | 10.14      | HUD overlay window                                    |
| `.fullScreenUI`         | 15        | 10.14      | Full-screen presentation UI                           |
| `.toolTip`              | 17        | 10.14      | Tooltip background                                    |
| `.contentBackground`    | 18        | 10.14      | Content area background (tables, text views)          |
| `.underWindowBackground`| 21        | 10.14      | Behind the window (desktop widget style)              |
| `.underPageBackground`  | 22        | 10.14      | Behind scrolled-out content (under-page area)         |

### Deprecated Materials

| Material                | Raw Value | Status                                    |
|-------------------------|-----------|-------------------------------------------|
| `.appearanceBased`      | 0         | Deprecated 10.14. Use specific materials. |
| `.light`                | 1         | Deprecated 10.14. Use specific materials. |
| `.dark`                 | 2         | Deprecated 10.14. Use specific materials. |
| `.mediumLight`          | 8         | Deprecated 10.14. Use specific materials. |
| `.ultraDark`            | 9         | Deprecated 10.14. Use specific materials. |

## Blending Modes

`NSVisualEffectView` supports two blending modes:

| Mode              | Description                                                       |
|-------------------|-------------------------------------------------------------------|
| `.behindWindow`   | Blurs content behind the entire window (desktop, other windows)   |
| `.withinWindow`   | Blurs content within the same window (content behind this view)   |

### Usage by Material

| Material                | Typical Blending Mode |
|-------------------------|-----------------------|
| `.sidebar`              | `.behindWindow`       |
| `.titlebar`             | `.behindWindow`       |
| `.menu`                 | `.behindWindow`       |
| `.popover`              | `.behindWindow`       |
| `.toolTip`              | `.behindWindow`       |
| `.hudWindow`            | `.behindWindow`       |
| `.contentBackground`    | `.withinWindow`       |
| `.headerView`           | `.withinWindow`       |
| `.selection`            | `.withinWindow`       |
| `.sheet`                | `.behindWindow`       |
| `.windowBackground`     | `.behindWindow`       |

## Material Visual Properties

Approximate visual characteristics of each material (these are not exact CSS equivalents; macOS uses complex multi-layer compositing):

### Sidebar Material

```
Light Mode:
  Background tint: rgba(255, 255, 255, 0.70)
  Saturation: 1.8
  Blur radius: 30 pt

Dark Mode:
  Background tint: rgba(30, 30, 30, 0.72)
  Saturation: 1.6
  Blur radius: 30 pt
```

### Menu Material

```
Light Mode:
  Background tint: rgba(255, 255, 255, 0.80)
  Saturation: 1.8
  Blur radius: 50 pt

Dark Mode:
  Background tint: rgba(40, 40, 40, 0.82)
  Saturation: 1.5
  Blur radius: 50 pt
```

### Popover Material

```
Light Mode:
  Background tint: rgba(246, 246, 246, 0.85)
  Saturation: 1.6
  Blur radius: 40 pt

Dark Mode:
  Background tint: rgba(50, 50, 50, 0.85)
  Saturation: 1.4
  Blur radius: 40 pt
```

### Titlebar Material

```
Light Mode:
  Background tint: rgba(236, 236, 236, 0.80)
  Saturation: 1.4
  Blur radius: 30 pt

Dark Mode:
  Background tint: rgba(50, 50, 50, 0.78)
  Saturation: 1.2
  Blur radius: 30 pt
```

### Tooltip Material

```
Light Mode:
  Background tint: rgba(255, 255, 204, 0.95)
  Saturation: 1.0
  Blur radius: 10 pt

Dark Mode:
  Background tint: rgba(60, 60, 60, 0.95)
  Saturation: 1.0
  Blur radius: 10 pt
```

### HUD Window Material

```
Light Mode:
  Background tint: rgba(40, 40, 40, 0.90)
  Saturation: 1.0
  Blur radius: 40 pt

Dark Mode:
  Background tint: rgba(30, 30, 30, 0.92)
  Saturation: 1.0
  Blur radius: 40 pt
```

## Window Backgrounds

macOS windows come in several configurations with different translucency behaviors.

### Standard Window

```
titlebarAppearsTransparent = false
styleMask includes .titled

Light: Opaque #ECECEC with vibrancy titlebar
Dark:  Opaque #323232 with vibrancy titlebar
```

### Full-Size Content View Window

```
titlebarAppearsTransparent = true
styleMask includes .fullSizeContentView

Content extends behind titlebar.
Titlebar area gets automatic vibrancy overlay.
```

### Unified Toolbar Window (macOS 11+)

```
toolbarStyle = .unified
titleVisibility = .visible

Toolbar and titlebar share a single vibrancy band.
Height: ~52 pt (with title) / ~38 pt (without title)
```

### Compact Unified Toolbar

```
toolbarStyle = .unifiedCompact

Shorter toolbar band.
Height: ~38 pt
Used in auxiliary/utility windows.
```

### Sidebar Split View

The sidebar portion of an `NSSplitView` with a sidebar style automatically receives `.sidebar` material vibrancy when configured correctly:

```
splitViewItem.behavior = .sidebar

Sidebar width range: 180-280 pt (default ~240 pt)
Minimum recommended: 200 pt
```

## Vibrancy States

| State              | Effect                                         |
|--------------------|-------------------------------------------------|
| Active window      | Full vibrancy, live blur from desktop content   |
| Inactive window    | Reduced vibrancy, frozen snapshot of background |
| Accessibility mode | Vibrancy disabled, opaque backgrounds used      |

When "Reduce Transparency" is enabled in System Settings > Accessibility:

| Material              | Fallback Light  | Fallback Dark   |
|-----------------------|-----------------|-----------------|
| `.sidebar`            | `#F6F6F6`       | `#2D2D2D`       |
| `.menu`               | `#FFFFFF`       | `#353535`       |
| `.popover`            | `#F6F6F6`       | `#323232`       |
| `.titlebar`           | `#ECECEC`       | `#323232`       |
| `.toolTip`            | `#FFFFCC`       | `#3C3C3C`       |
| `.contentBackground`  | `#FFFFFF`       | `#1E1E1E`       |
| `.windowBackground`   | `#ECECEC`       | `#323232`       |

## Vibrancy Label Colors

When drawing on vibrant surfaces, the system automatically adjusts label colors for contrast. These are NOT the same as the standard label colors.

On a vibrant surface, use:
- `NSColor.labelColor` -- system adjusts automatically
- `NSColor.secondaryLabelColor` -- dimmer variant
- Do NOT use hardcoded colors on vibrant surfaces

The vibrant variants use different compositing (additive/subtractive blending) to maintain readability regardless of background content.

## Material Layering Order (back to front)

```
1. Desktop wallpaper / other windows
2. Window background (windowBackground material)
3. Sidebar (sidebar material, behindWindow blending)
4. Content area (contentBackground material, withinWindow blending)
5. Header / toolbar (headerView / titlebar material)
6. Selection highlight (selection material)
7. Popover / menu (behindWindow blending, floats above)
8. Tooltip (topmost vibrancy layer)
```

## Dija Implementation Notes

To replicate macOS vibrancy in Dija:

1. **GPU compositing required.** Vibrancy needs real-time blur of window content. The software backend cannot do this at interactive frame rates.
2. **Material = blur + tint + saturation.** Each material is a tuple of (blur_radius, tint_color, tint_alpha, saturation_factor).
3. **Blending modes matter.** `behindWindow` requires access to the compositor's window backing store. `withinWindow` can be done with a render-to-texture pass.
4. **Fallback for reduced transparency.** Always provide opaque fallback colors for accessibility.
5. **Metal integration.** On macOS, Dija can use `CAMetalLayer` with `NSVisualEffectView` as a parent to get native vibrancy for free. Custom rendering requires replicating the blur pipeline.
