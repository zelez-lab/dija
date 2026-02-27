# Linux (GNOME/Adwaita) — Switch (GtkSwitch)

## Appearance

Adwaita's switch is a compact pill-shaped toggle with a circular thumb.

## Track

| Property | Light | Dark |
|----------|-------|------|
| Width | 42px | 42px |
| Height | 26px | 26px |
| Corner radius | 13px (fully rounded) | 13px |
| Off background | `rgba(0,0,0, 0.15)` | `rgba(255,255,255, 0.15)` |
| On background | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Border (off) | 2px `rgba(0,0,0, 0.15)` | 2px `rgba(255,255,255, 0.15)` |
| Border (on) | none (accent fill covers) | none |

## Thumb (Slider)

| Property | Value |
|----------|-------|
| Diameter | 20px |
| Color | `#FFFFFF` |
| Shadow | (0, 1) blur 2, black @ 0.10 |
| Corner radius | 10px (fully round) |
| Horizontal margin | 3px from track edge |

## States

| State | Track | Thumb |
|-------|-------|-------|
| Off (rest) | `rgba(0,0,0, 0.15)` | Left position |
| Off (hover) | `rgba(0,0,0, 0.22)` | Left position |
| Off (active) | `rgba(0,0,0, 0.30)` | Left position |
| On (rest) | accent_bg_color | Right position |
| On (hover) | accent_bg_color, lightened ~8% | Right position |
| On (active) | accent_bg_color, darkened ~8% | Right position |
| Disabled (off) | `rgba(0,0,0, 0.08)` | Left, opacity 0.5 |
| Disabled (on) | accent @ 0.5 | Right, opacity 0.5 |

## Focus

| Property | Value |
|----------|-------|
| Focus ring | 2px `--accent-color`, 2px offset |
| Focus ring radius | track radius + 2px = 15px |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Thumb slide | 250ms | ease-in-out |
| Track color change | 250ms | ease-in-out |
| Hover color change | 200ms | ease-in-out |

## Keyboard Support

| Key | Action |
|-----|--------|
| Space | Toggle switch |
| Enter | Toggle switch |
| Tab | Move focus |

## Metrics Summary

```
Track:  42 x 26px, radius 13px
Thumb:  20 x 20px, radius 10px
Margin: 3px inset from track edge

Off:    [O          ]  thumb at x=3
On:     [          O]  thumb at x=19 (42 - 20 - 3)
```

## CSS Node Structure

```
switch
 +-- image (optional, for slider icon)
```

## Dija Skin Mapping

```
skin! {
    SwitchSkin {
        field track
        field thumb

        platform linux {
            light {
                track: {
                    width: 42, height: 26,
                    border_radius: 13,
                    background: rgba(0,0,0,0.15),
                    border: 2 rgba(0,0,0,0.15),
                }
                thumb: {
                    width: 20, height: 20,
                    border_radius: 10,
                    background: #FFFFFF,
                    shadow: 0 1 2 0 rgba(0,0,0,0.10),
                }
            }
        }
    }
}
```
