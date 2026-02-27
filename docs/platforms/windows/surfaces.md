# Windows — Surfaces (Materials)

Source: WinUI 3 Material System, Windows 11

Windows 11 signature look: layered depth through Mica and Acrylic materials.

## Material System Overview

```
Mica (window base) → Content layer (semi-transparent) → Controls (opaque fills)
```

Windows uses a **two-layer system**: a material base layer (Mica or Acrylic) and content layers on top. The base layer provides the ambient, contextual appearance while content layers hold interactive UI.

## Mica

Mica is an **opaque** material that subtly tints the window background with the user's desktop wallpaper colors. It is NOT transparent in the traditional sense -- it samples the wallpaper once and applies a computed tint.

### Mica Base

| Property | Light | Dark |
|----------|-------|------|
| Tint color | `#F3F3F3` (243, 243, 243) | `#202020` (32, 32, 32) |
| Tint opacity | 0.50 | 0.80 |
| Luminosity opacity | 1.00 | 1.00 |
| Fallback color | `#F3F3F3` | `#202020` |

### Mica Alt

A variant with less tinting that allows more wallpaper color to show through. Used for secondary windows or background surfaces.

| Property | Light | Dark |
|----------|-------|------|
| Tint color | `#DADADA` (218, 218, 218) | `#0A0A0A` (10, 10, 10) |
| Tint opacity | 0.50 | 0.50 |
| Luminosity opacity | 1.00 | 1.00 |
| Fallback color | `#DADADA` | `#0A0A0A` |

### Mica Rendering Pipeline

```
DesktopWallpaper
  → Gaussian blur (large radius, ~120px)
  → Downsample
  → Tint overlay (tint_color @ tint_opacity)
  → Luminosity clamp (luminosity_opacity)
  → Final surface
```

### Mica Behavior

| Condition | Behavior |
|-----------|----------|
| Window active | Full Mica effect with wallpaper tint |
| Window inactive | Neutral solid fallback (no wallpaper sampling) |
| Battery saver / low power | Solid fallback color |
| High contrast mode | Solid system background color |
| Windows 10 (no Mica support) | Solid fallback color |
| Remote desktop | Solid fallback color |

### Mica Usage

| Surface | Material |
|---------|----------|
| Main window background | Mica Base |
| Settings window | Mica Base |
| Secondary/companion windows | Mica Alt |
| NavigationView background | Mica Base (applied to root) |

## Acrylic

Acrylic is a **translucent** material that shows a blurred version of content behind the surface, plus noise texture for visual richness.

### In-App Acrylic

Blurs content **within** the app window. Used for surfaces that overlay app content.

| Property | Light | Dark |
|----------|-------|------|
| Tint color | `#FCFCFC` (252, 252, 252) | `#2C2C2C` (44, 44, 44) |
| Tint opacity | 0.00 (fully transparent tint) | 0.15 |
| Luminosity opacity | 0.85 | 0.96 |
| Fallback color | `#F9F9F9` | `#2C2C2C` |
| Blur radius | 30px | 30px |
| Noise texture | 2% luminance noise | 2% luminance noise |

### Background Acrylic

Blurs content **behind** the app window (desktop, other windows). This was deprecated in Windows 11 for most uses; only transient surfaces use it.

| Property | Light | Dark |
|----------|-------|------|
| Tint color | `#FCFCFC` | `#2C2C2C` |
| Tint opacity | 0.00 | 0.15 |
| Luminosity opacity | 0.85 | 0.96 |
| Fallback color | `#F9F9F9` | `#2C2C2C` |
| Blur radius | 30px (desktop backdrop) | 30px |
| Noise texture | 2% luminance noise | 2% luminance noise |

### Acrylic Rendering Pipeline

```
Background content (behind or within window)
  → Gaussian blur (30px)
  → Exclusion blend
  → Tint overlay (tint_color @ tint_opacity)
  → Luminosity clamp (luminosity_opacity)
  → Noise texture overlay (2%, luminance)
  → Final surface
```

### Acrylic Usage

| Surface | Acrylic Type |
|---------|-------------|
| Context menus | Background Acrylic |
| MenuFlyout | Background Acrylic |
| CommandBarFlyout | Background Acrylic |
| NavigationView pane (overlay mode) | In-App Acrylic |
| Flyouts | Background Acrylic |
| AutoSuggestBox dropdown | Background Acrylic |

## Smoke Layer

A dimming overlay applied behind modal dialogs and full-screen content.

| Property | Light | Dark |
|----------|-------|------|
| Color | `#000000` @ 30% | `#000000` @ 40% |
| Resource name | SmokeFillColorDefault | SmokeFillColorDefault |

Used for: ContentDialog backdrop, popup overlays, light-dismiss backgrounds.

## Layering System

### Two-Layer Architecture

```
┌─────────────────────────────────┐
│  Layer 2: Content surface       │  ← LayerFillColorDefault (semi-transparent)
│  ┌───────────────────────────┐  │
│  │  Controls (buttons, etc.) │  │  ← Opaque control fills
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  Layer 1: Base material         │  ← Mica or solid background
└─────────────────────────────────┘
```

### Layer Fill Colors

| Layer | Light | Dark | Usage |
|-------|-------|------|-------|
| Base (Mica/Mica Alt) | See Mica section | See Mica section | Window background |
| Content (on Mica) | `#80FFFFFF` (white@50%) | `#0DFFFFFF` (white@5%) | Cards, panels, content areas |
| Content Alt | `#FFFFFF` (opaque) | `#0DFFFFFF` | Elevated content surfaces |
| On Acrylic | `#40FFFFFF` (white@25%) | `#09FFFFFF` (white@3.5%) | Content on Acrylic base |

### Layering Guidelines

| Principle | Description |
|-----------|-------------|
| Max 2 layers | Base + 1 content layer. Avoid stacking more. |
| No Acrylic on Acrylic | Never layer Acrylic materials. Use opaque fills for nested surfaces. |
| No Mica on content | Mica is base-only. Content layers use semi-transparent fills. |
| Cards on Mica | Use `LayerFillColorDefault` + `CardStrokeColorDefault` border |
| Flyouts on anything | Use Background Acrylic + Shadow 8 |
| Dialogs on anything | Use Smoke layer + opaque dialog fill + Shadow 28 |

## Material Fallback Cascade

When materials cannot render (battery saver, remote desktop, legacy OS):

```
Mica → SolidBackgroundFillColorBase (#F3F3F3 / #202020)
Mica Alt → SolidBackgroundFillColorBaseAlt (#DADADA / #0A0A0A)
Acrylic (in-app) → AcrylicFallback (#F9F9F9 / #2C2C2C)
Acrylic (background) → AcrylicFallback (#F9F9F9 / #2C2C2C)
Smoke → SmokeFillColorDefault (opaque black overlay)
```

## Title Bar Integration

Windows 11 title bars extend into Mica. The `ExtendsContentIntoTitleBar` API allows app content to render behind the title bar caption buttons, providing a seamless Mica background from the window chrome into the app.

| Region | Height |
|--------|--------|
| Standard title bar | 32px |
| Tall title bar (with back button) | 48px |
| Caption button area width | 138px (3 buttons x 46px) |
| Drag region | Full title bar minus interactive elements |
