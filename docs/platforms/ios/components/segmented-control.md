# iOS — Segmented Control (UISegmentedControl)

Source: UISegmentedControl

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | systemGray6 (`#F2F2F7`) | `#1C1C1E` (elevated: `#2C2C2E`) |
| Corner radius (outer) | 9pt | 9pt |
| Corner curve | `.continuous` (superellipse) | |
| Height | 32pt | 32pt |
| Border | None (flat fill) | None |

## Segments

| Property | Value |
|----------|-------|
| Font | SF Pro Medium, 13pt |
| Text color (unselected) | label (`#000000` / `#FFFFFF`) |
| Text color (selected) | label (`#000000` / `#FFFFFF`) |
| Separator | 1pt wide, systemGray4 between unselected segments |
| Separator height | ~20pt (centered vertically, shorter than full height) |
| Horizontal padding | 12pt per segment (minimum) |
| Segment width | Equal distribution or intrinsic content size |

## Selected Segment Indicator

The selected segment floats as a rounded rect "pill" above the background.

| Property | Light | Dark |
|----------|-------|------|
| Fill | white (`#FFFFFF`) | systemGray3 (`#48484A`) |
| Corner radius | 7pt | 7pt |
| Corner curve | `.continuous` (superellipse) | |
| Inset from outer edge | 2pt (each side) | 2pt |
| Shadow 1 | offset(0, 3) blur 8, black @ 0.12 | offset(0, 3) blur 8, black @ 0.24 |
| Shadow 2 | offset(0, 3) blur 1, black @ 0.04 | offset(0, 3) blur 1, black @ 0.08 |

## States

| State | Effect |
|-------|--------|
| Normal (unselected) | Standard text on background |
| Selected | Floating pill indicator, shadows |
| Pressed (unselected) | Darken segment background ~10% |
| Pressed (selected) | Slightly darker pill |
| Disabled | Alpha 0.3 on entire control |
| Disabled (selected) | Selected pill visible but at reduced contrast |

## Animation

| Property | Value |
|----------|-------|
| Selection change | 0.3s spring animation |
| Spring damping | 0.75 |
| Pill slides | Horizontally to new position |
| Text crossfade | None (text stays in place, pill moves behind) |
| Separator fade | Adjacent separators fade out as pill approaches |

### Animation Sequence (Segment A -> Segment B)

1. User taps segment B
2. Selected pill begins sliding from A to B (spring, 0.3s)
3. Separators adjacent to A fade in, separators adjacent to B fade out
4. Pill arrives at B position

## Metrics (Summary)

```
┌─────────────────────────────────────────────┐  ← outer: 9pt radius
│ ┌─────────┐ │ ┌─────────┐ │ ┌─────────┐    │
│ │ Segment │ │ │ SELECTED│ │ │ Segment │    │  ← 32pt height
│ │   One   │ │ │   Two   │ │ │  Three  │    │
│ └─────────┘ │ └─────────┘ │ └─────────┘    │  ← inner: 7pt radius
└─────────────────────────────────────────────┘
              ↑ separators (1pt, gray4)
  ←── 2pt ──→   ← pill inset from edges
```

## Accessibility

| Property | Value |
|----------|-------|
| Role | Segmented control (tab-like) |
| Each segment | Button with "selected" trait when active |
| VoiceOver | "[Label], button, [N] of [total]" |
