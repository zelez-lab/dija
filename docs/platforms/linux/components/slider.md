# Linux (GNOME/Adwaita) — Slider (GtkScale)

## Appearance

A horizontal (or vertical) slider with a thin track and a circular thumb.

## Track

| Property | Light | Dark |
|----------|-------|------|
| Height | 4px | 4px |
| Corner radius | 2px (fully rounded) | 2px |
| Filled (left of thumb) | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Unfilled (right of thumb) | `rgba(0,0,0, 0.15)` | `rgba(255,255,255, 0.15)` |
| Fill level indicator | `--accent-bg-color` @ 0.5 | `--accent-bg-color` @ 0.5 |

## Thumb (Slider Handle)

| Property | Light | Dark |
|----------|-------|------|
| Diameter | 20px | 20px |
| Color | `#FFFFFF` | `#FFFFFF` |
| Border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Shadow | (0, 1) blur 2, black @ 0.10 | (0, 1) blur 2, black @ 0.10 |
| Corner radius | 10px (fully round) | 10px |
| Hit area | 34px diameter (invisible) | 34px |

## States

| State | Thumb | Track |
|-------|-------|-------|
| Rest | white, 20px | normal |
| Hover | white, slight border darken | normal |
| Active (dragging) | accent_bg_color, 20px | normal |
| Disabled | white, opacity 0.5 | opacity 0.5 |

### Hover

| Property | Value |
|----------|-------|
| Thumb border | `rgba(0,0,0, 0.25)` (slightly stronger) |

### Active (Dragging)

| Property | Value |
|----------|-------|
| Thumb color | `--accent-bg-color` (fills with accent) |
| Thumb border | none (accent fill covers) |

## Metrics

| Property | Value |
|----------|-------|
| Track height | 4px |
| Track corner radius | 2px |
| Thumb diameter | 20px |
| Hit area (thumb) | 34px |
| Min width (horizontal) | 100px |
| Total widget height | 34px (includes hit area) |
| Horizontal padding | 12px |

## Marks and Ticks

GtkScale supports marks (tick marks along the track):

| Property | Value |
|----------|-------|
| Mark height | 6px |
| Mark width | 1px |
| Mark color | `rgba(0,0,0, 0.20)` / `rgba(255,255,255, 0.20)` |
| Mark label font | `.caption` (13px) |
| Mark label color | dim-label color (secondary) |

## Value Display

| Property | Value |
|----------|-------|
| Value position | Above or below (configurable) |
| Value font | `.caption` (13px) |
| Draw value | Optional (default: off) |
| Value format | Configurable via signal |

## Orientation

| Orientation | Track Axis | Filled Direction |
|-------------|-----------|-----------------|
| Horizontal | Left to right | Left of thumb = filled |
| Vertical | Bottom to top | Below thumb = filled |
| Inverted | Reverses direction | Filled direction reverses |

## Focus

| Property | Value |
|----------|-------|
| Focus ring | 2px accent outline around thumb |
| Focus ring offset | 2px |
| Focus radius | thumb radius + 2px = 12px |

## Keyboard Support

| Key | Action |
|-----|--------|
| Left / Down | Decrease by step |
| Right / Up | Increase by step |
| Page Up / Page Down | Increase / decrease by page step |
| Home / End | Jump to min / max |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Thumb color change | 200ms | ease-in-out |
| Value change (keyboard) | immediate | — |
| Value change (scroll) | immediate | — |

## OSD Variant

When used with `.osd` style class (e.g., media player volume):

| Property | Value |
|----------|-------|
| Track height | 3px (thinner) |
| Trough visible | no |
| Background | transparent |
| Thumb | same, with OSD shadow |

## CSS Node Structure

```
scale[.horizontal/.vertical]
 +-- trough
 |    +-- slider (thumb)
 |    +-- highlight (filled portion)
 |    +-- fill (fill level, optional)
 +-- marks.top
 |    +-- mark
 |         +-- indicator
 |         +-- label
 +-- marks.bottom
      +-- mark
           +-- indicator
           +-- label
```
