# iOS — Surfaces (Materials)

Source: Apple Human Interface Guidelines (iOS 17+)

iOS signature look: layered translucency with vibrancy.

## Formula

```
Material = BackdropBlur(sigma) + Saturate(1.8) + Overlay(tint_color) + Background(base_color @ opacity)
```

On capable hardware, Apple uses a multi-pass compositing approach:
1. **Capture** the pixels behind the view
2. **Apply Gaussian blur** with the given sigma
3. **Boost saturation** (~1.8x) to keep colors vibrant through the blur
4. **Overlay** a tinted layer for the material's characteristic color cast
5. **Composite** the view's content on top

## Material Levels

| Material | Blur sigma | Tint overlay (light) | Tint overlay (dark) | Notes |
|----------|-----------|---------------------|---------------------|-------|
| Ultra thin | ~40 | white @ 0.02 | black @ 0.02 | Very transparent, maximum blur |
| Thin | ~30 | white @ 0.05 | black @ 0.05 | Subtle material |
| Regular | ~20 | white @ 0.10 | black @ 0.10 | Default for most surfaces |
| Thick | ~15 | white @ 0.20 | black @ 0.15 | More opaque |
| Ultra thick | ~10 | white @ 0.30 | black @ 0.25 | Most opaque, minimum blur |
| Chrome | ~20 | white @ 0.25 | black @ 0.15 | Navigation/tab bars (denser tint) |

All materials include a **saturation boost of ~1.8x**.

## Vibrancy

Vibrancy is a companion to materials. It renders content (text, icons, separators) semi-transparently so the blurred background shows through, maintaining legibility while feeling integrated with the surface.

### Vibrancy Levels

| Level | Effect | Usage |
|-------|--------|-------|
| Primary (label) | Brightest / most legible | Primary text, icons on materials |
| Secondary | Reduced luminance | Secondary text, subtitles |
| Tertiary | Most subtle | Tertiary info, fills |
| Separator | Thin, subtle line | Separators on material backgrounds |
| Fill | Semi-transparent fill | Interactive element fills on materials |

In light mode, vibrant content is darkened. In dark mode, vibrant content is lightened. This is achieved through blend modes (plus-lighter in dark, multiply in light).

## Component-to-Material Mapping

| Component | Material | Vibrancy | Notes |
|-----------|----------|----------|-------|
| Navigation bar (at rest) | Regular | Label (title), Secondary (buttons) | Transitions to solid on scroll |
| Navigation bar (scrolled) | Solid (opaque) | None | Falls back to system background |
| Tab bar | Thin or Regular | Label (selected icon), Secondary (labels) | |
| Toolbar | Regular | Label | |
| Sidebar (iPad) | Regular | Label | |
| Alerts | Ultra thick | Label (title, actions), Secondary (message) | |
| Action sheets | Ultra thick | Label (actions), Secondary (header) | |
| Bottom sheets | Regular | None (uses standard colors) | |
| Notification banners | Regular | Label | |
| Context menu backdrop | Thin | None (dimming overlay on rest of screen) | |
| Search bar background | Thick | None | |
| Keyboard background | Regular (light) / Thick (dark) | Label (keys) | |
| Control center | Ultra thin | Label | |
| Spotlight search | Regular | Label | |
| Widget background | Regular | Label | |

## Dimming Overlays

When modals appear, the background content is dimmed.

| Context | Overlay |
|---------|---------|
| Alert presentation | black @ 0.4 |
| Action sheet (iPad popover) | No dimming |
| Action sheet (iPhone) | black @ 0.4 |
| Sheet presentation | black @ 0.2 to 0.4 (scaled with drag) |
| Context menu | black @ 0.25 (with scale-down of background) |
| Photo viewer | black @ 1.0 (full black) |

## Elevation Model

iOS uses a flat elevation model (no Material Design-style z-axis shadows). Depth is conveyed through:

1. **Blur/material** — translucent surfaces feel "above" opaque ones
2. **Dimming** — darkened background behind modals
3. **Scale** — background content shrinks slightly during sheet presentation
4. **Shadows** — used sparingly (cards, floating elements), never as primary elevation cue

### Surface Hierarchy (bottom to top)

```
1. System background (opaque)
   2. Content (scrolling)
      3. Navigation bar (material, floating above scroll)
      3. Tab bar (material, floating above scroll)
         4. Sheet (slides up from bottom)
            5. Alert (centered, dimmed backdrop)
               6. Status bar (always on top)
```

## Fallback (No Blur Support)

On hardware without GPU blur support (or reduced transparency accessibility setting):

| Material | Fallback (light) | Fallback (dark) |
|----------|------------------|-----------------|
| Ultra thin | white @ 0.80 | `#1C1C1E` @ 0.90 |
| Thin | white @ 0.85 | `#1C1C1E` @ 0.92 |
| Regular | white @ 0.90 | `#1C1C1E` @ 0.94 |
| Thick | white @ 0.94 | `#1C1C1E` @ 0.96 |
| Ultra thick | white @ 0.97 | `#1C1C1E` @ 0.98 |

When `UIAccessibility.isReduceTransparencyEnabled` is true, all materials become fully opaque with their fallback background colors.
