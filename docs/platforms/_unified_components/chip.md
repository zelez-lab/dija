# Chip

A compact element representing an attribute, action, or filter, often displayed in a group.

| Platform | Native Component | Status |
|---|---|---|
| iOS | — | No native equivalent |
| macOS | — | No native equivalent |
| Android | Chip (M3) | Documented |
| Windows | — | No native equivalent |
| Linux | — | No native equivalent |

## iOS

No native equivalent. Dija renders as a rounded pill-shaped element following iOS styling conventions (system font, iOS corner radii, system colors).

## macOS

No native equivalent. Dija renders as a rounded pill-shaped element following macOS styling conventions.

## Android

Source: m3.material.io/components/chips/specs

### Variants

| Variant | Purpose | Dismissible | Selectable |
|---------|---------|------------|------------|
| Assist | Smart actions (call, navigate, share) | No | No |
| Filter | Narrow content (category, tag) | No | Yes (toggle) |
| Input | User-entered info (email recipient, tag) | Yes (trailing X) | No |
| Suggestion | Dynamically generated prompts | No | No |

### Metrics

| Property | Value |
|----------|-------|
| Height | 32dp |
| Corner radius | 8dp (small) |
| Horizontal padding | 16dp (text-only) |
| Horizontal padding (with leading icon) | 8dp (start), 16dp (end) |
| Horizontal padding (with trailing icon) | 16dp (start), 8dp (end) |
| Leading icon size | 18dp |
| Trailing icon size | 18dp |
| Icon-label gap | 8dp |
| Label font | Label Large (Roboto Medium 500, 14sp) |
| Border width (outlined variants) | 1dp |
| Touch target | 48dp min height |

### Colors

#### Assist Chip

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container (outlined) | Enabled | transparent | transparent |
| Container (elevated) | Enabled | surfaceContainerLow | surfaceContainerLow |
| Border | Enabled | `#79747E` (outline) | `#938F99` |
| Label | Enabled | `#1D1B20` (onSurface) | `#E6E0E9` |
| Leading icon | Enabled | `#6750A4` (primary) | `#D0BCFF` |

#### Filter Chip

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container | Unselected | transparent | transparent |
| Container | Selected | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Border | Unselected | `#79747E` (outline) | `#938F99` |
| Border | Selected | none | none |
| Label | Unselected | `#1D1B20` (onSurface) | `#E6E0E9` |
| Label | Selected | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |
| Check icon | Selected | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |

#### Input Chip

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container | Enabled | transparent | transparent |
| Border | Enabled | `#79747E` (outline) | `#938F99` |
| Label | Enabled | `#1D1B20` (onSurface) | `#E6E0E9` |
| Trailing icon (remove) | Enabled | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Avatar | Enabled | 24dp circle, primaryContainer bg | |
| Leading image | Enabled | 24dp, 8dp corner radius | |

#### Suggestion Chip

| Element | State | Light | Dark |
|---------|-------|-------|------|
| Container (outlined) | Enabled | transparent | transparent |
| Container (elevated) | Enabled | surfaceContainerLow | surfaceContainerLow |
| Border | Enabled | `#79747E` (outline) | `#938F99` |
| Label | Enabled | `#1D1B20` (onSurface) | `#E6E0E9` |

### States

All chip variants share the same state layer pattern:

| State | Effect |
|-------|--------|
| Hovered | State layer 8% (onSurface or onSecondaryContainer) |
| Focused | State layer 10% |
| Pressed | State layer 10% + ripple |
| Dragged | State layer 16% |
| Disabled | Container onSurface @ 12%, content onSurface @ 38% |

### Filter Chip Selection

When a filter chip toggles to selected:
1. Check icon (18dp) fades in at leading position
2. Container fills with secondaryContainer
3. Border removed
4. Existing leading icon shifts right (if present)

Animation: Short 3 (150ms), Standard easing.

### Input Chip Removal

Tapping the trailing X icon (18dp):
1. Chip scales down to 0
2. Remaining chips reflow to fill gap

Animation: Short 4 (200ms), Standard accelerate.

### Layout

#### Chip Group (Horizontal)

```
+----------+  8dp  +---------+  8dp  +------------+
| [x] Tag1 |       |  Tag2   |       | [x] Tag3   |
+----------+       +---------+       +------------+
                 32dp height, 8dp gap
```

#### Chip Group (Flow/Wrap)

Chips wrap to next line when horizontal space runs out.
Row gap: 8dp.

## Windows

No native equivalent. Dija renders as a rounded pill-shaped element following Fluent Design styling conventions.

## Linux

No native equivalent. Dija renders as a rounded pill-shaped element following Adwaita styling conventions.
