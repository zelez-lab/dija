# Windows — Segmented Control (RadioButtons / Segmented)

Source: WinUI 3 RadioButtons (grouped), SegmentedControl (WinUI 3 Gallery)

Windows does not have a native 1:1 equivalent to iOS UISegmentedControl. The closest patterns are:

1. **RadioButtons** (grouped, pill-shaped) -- standard WinUI control for mutually exclusive choices
2. **SegmentedControl** -- community/gallery pattern using styled ToggleButtons in a horizontal strip

## RadioButtons (Standard Approach)

RadioButtons displays a grouped set of radio button options. Each item is a selectable option.

### Radio Button Metrics

| Property | Value |
|----------|-------|
| Circle diameter (outer) | 20px |
| Circle diameter (inner dot, selected) | 8px |
| Hit area | 32px height |
| Text offset from circle | 8px |
| Font | 14px, Regular |
| Vertical spacing between items | 4px |
| Indicator color (selected) | AccentFillColorDefault |
| Indicator color (unselected) | ControlStrongStrokeColorDefault (1px ring) |

### Radio Button States

| State | Circle | Text |
|-------|--------|------|
| Rest (unselected) | 1px ring, ControlStrongStrokeColorDefault | TextFillColorPrimary |
| Hover (unselected) | 1px ring, ControlStrongStrokeColorDefault | TextFillColorPrimary |
| Selected | AccentColor fill + 8px white inner dot | TextFillColorPrimary |
| Hover (selected) | AccentFillColorSecondary + inner dot | TextFillColorPrimary |
| Disabled | ControlStrongStrokeColorDisabled | TextFillColorDisabled |

## Segmented / Pill Toggle (Gallery Pattern)

Used when a compact, horizontal switch between 2-5 options is needed. Built from grouped ToggleButtons.

### Container Metrics

| Property | Value |
|----------|-------|
| Background | ControlFillColorDefault |
| Corner radius | 4px |
| Border | 1px ControlStrokeColorDefault |
| Padding (inner) | 2px |
| Height | 32px |

### Segment Metrics

| Property | Value |
|----------|-------|
| Min width per segment | 48px |
| Padding | 8px horizontal, 4px vertical |
| Corner radius | 3px (inner segments) |
| Font | 14px, Regular |

### Segment States

| State | Background | Text |
|-------|-----------|------|
| Rest (unselected) | Transparent | TextFillColorSecondary |
| Hover (unselected) | SubtleFillColorSecondary | TextFillColorPrimary |
| Selected | ControlFillColorDefault (elevated via slight fill) or LayerFillColorDefault | TextFillColorPrimary |
| Disabled | Transparent | TextFillColorDisabled |

The selected segment has a **subtle elevation** (slightly brighter fill) and optionally a thin border or shadow to appear raised above the container.

### Selection Indicator Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Selection slide (background pill) | 200ms | Decelerate |
| Hover fill change | 100ms | Control fast |

## Dija Mapping

For Windows skin, the segmented control should render as:
- **2-3 options**: Segmented pill toggle (horizontal ToggleButton strip)
- **4+ options or vertical layout**: RadioButtons (standard grouped radio)

Both patterns use the same underlying `dija-ui` SegmentedControl component, just with different skin rendering.
