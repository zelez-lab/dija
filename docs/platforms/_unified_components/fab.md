# FAB (Floating Action Button)

A prominent, elevated button that floats above the content area, representing the primary action of a screen.

| Platform | Native Component | Status |
|---|---|---|
| iOS | — | No native equivalent |
| macOS | — | No native equivalent |
| Android | FAB (M3) | Documented |
| Windows | — | No native equivalent |
| Linux | — | No native equivalent |

## iOS

No native equivalent. Dija renders as a floating circular button following iOS styling conventions (system blur, shadow, system colors).

## macOS

No native equivalent. Dija renders as a floating circular button following macOS styling conventions.

## Android

Source: m3.material.io/components/floating-action-button/specs

### Variants

| Variant | Size | Corner radius | Usage |
|---------|------|---------------|-------|
| FAB | 56dp x 56dp | 16dp (large) | Primary action |
| Small FAB | 40dp x 40dp | 12dp (medium) | Secondary action, compact layouts |
| Large FAB | 96dp x 96dp | 28dp (extra-large) | Hero action (rare) |
| Extended FAB | 56dp height, variable width | 16dp (large) | Primary action with label |

### Metrics

#### Standard FAB (56dp)

| Property | Value |
|----------|-------|
| Width | 56dp |
| Height | 56dp |
| Corner radius | 16dp |
| Icon size | 24dp |
| Elevation | Level 3 (6dp) |
| Min touch target | 48dp (already exceeded) |

#### Small FAB (40dp)

| Property | Value |
|----------|-------|
| Width | 40dp |
| Height | 40dp |
| Corner radius | 12dp |
| Icon size | 24dp |
| Elevation | Level 3 (6dp) |

#### Large FAB (96dp)

| Property | Value |
|----------|-------|
| Width | 96dp |
| Height | 96dp |
| Corner radius | 28dp |
| Icon size | 36dp |
| Elevation | Level 3 (6dp) |

#### Extended FAB

| Property | Value |
|----------|-------|
| Height | 56dp |
| Min width | 80dp |
| Corner radius | 16dp |
| Icon size | 24dp |
| Icon-label gap | 12dp |
| Horizontal padding | 16dp |
| Label font | Label Large (Roboto Medium 500, 14sp) |
| Elevation | Level 3 (6dp) |

### Colors

| Variant | Container | Icon/Label |
|---------|-----------|-----------|
| Surface (default) | surfaceContainerHigh | primary |
| Primary | primaryContainer | onPrimaryContainer |
| Secondary | secondaryContainer | onSecondaryContainer |
| Tertiary | tertiaryContainer | onTertiaryContainer |

#### Default (Surface) Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainerHigh) | `#2B2930` |
| Icon | `#6750A4` (primary) | `#D0BCFF` |

#### Primary Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#EADDFF` (primaryContainer) | `#4F378B` |
| Icon | `#21005D` (onPrimaryContainer) | `#EADDFF` |

### States

| State | Container | Elevation |
|-------|-----------|-----------|
| Enabled | Default | Level 3 (6dp) |
| Hovered | + state layer 8% | Level 4 (8dp) |
| Focused | + state layer 10% | Level 3 (6dp) |
| Pressed | + state layer 10% + ripple | Level 3 (6dp) |

State layer color matches the icon/label color.

### Positioning

| Property | Value |
|----------|-------|
| Bottom-right margin | 16dp |
| Distance from bottom nav bar | 16dp above bar |
| Distance from edge | 16dp |

FAB avoids overlapping with:
- Bottom navigation bar (floats above)
- Snackbar (snackbar slides up to clear FAB)
- Bottom sheet (FAB hides or moves)

### Extended FAB Collapse

Extended FAB can collapse to standard FAB on scroll:
- On scroll down: label fades out, width shrinks to 56dp
- On scroll up: width expands, label fades in
- Duration: Medium 2 (300ms), Standard easing

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Enter (scale) | Medium 1 (250ms) | Emphasized decelerate |
| Exit (scale) | Short 4 (200ms) | Standard accelerate |
| Collapse (extended) | Medium 2 (300ms) | Standard |
| Expand (extended) | Medium 2 (300ms) | Standard |
| Hover elevation | Short 2 (100ms) | Standard |

### Layout

#### Standard Position

```
+----------------------------------------+
|                                        |
|                  Main content          |
|                                        |
|                                        |
|                              +------+  |
|                              | FAB  |  | 16dp from edge
|                              | 56dp |  |
|                              +------+  |
|  16dp                        16dp      |
+========================================+
|  Navigation bar (80dp)                 |
+========================================+
```

## Windows

No native equivalent. Dija renders as a floating circular button following Fluent Design styling conventions.

## Linux

No native equivalent. Dija renders as a floating circular button following Adwaita styling conventions.
