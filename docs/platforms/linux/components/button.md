# Linux (GNOME/Adwaita) — Button (GtkButton)

## Variants

| Style Class | Background (Light) | Background (Dark) | Border | Shadow |
|-------------|-------------------|-------------------|--------|--------|
| Default (raised) | `#FFFFFF` | `#404040` | 1px, `rgba(0,0,0,0.15)` | (0,1) blur 2, black @ 0.07 |
| `.flat` | transparent | transparent | none | none |
| `.suggested-action` | `#3584E4` (accent) | `#3584E4` | none | (0,1) blur 2, black @ 0.07 |
| `.destructive-action` | `#E01B24` (red_3) | `#C01C28` (red_4) | none | (0,1) blur 2, black @ 0.07 |
| `.opaque` | custom (user-defined) | custom | none | (0,1) blur 2, black @ 0.07 |
| `.circular` | same as raised | same as raised | same | same |
| `.pill` | same as raised | same as raised | same | same |

## Shapes

| Style Class | Corner Radius | Aspect Ratio |
|-------------|--------------|--------------|
| Default | 6px | Rectangle, width follows content |
| `.circular` | 9999px (fully round) | Square (1:1), for icons or 1-2 chars |
| `.pill` | 9999px (fully round) | Rectangle, width follows content |

## Metrics

| Property | Value |
|----------|-------|
| Min height | 34px |
| Horizontal padding | 16px |
| Vertical padding | 8px |
| Corner radius | 6px |
| Font | Adwaita Sans Regular, 15px |
| Icon size | 16x16px |
| Icon + label gap | 6px |
| Border width | 1px |
| Circular min size | 34x34px |

## States

### Default (Raised) Button

| State | Background (Light) | Background (Dark) | Shadow |
|-------|-------------------|-------------------|--------|
| Rest | `#FFFFFF` | `#404040` | (0,1) blur 2, black @ 0.07 |
| Hover | `#F5F5F5` | `#4A4A4A` | (0,1) blur 3, black @ 0.09 |
| Active (pressed) | `#DEDDDA` | `#353535` | inset (0,1) blur 2, black @ 0.07 |
| Focused | rest + 2px accent outline | rest + 2px accent outline | — |
| Disabled | rest, opacity 0.5 | rest, opacity 0.5 | — |

### Flat Button

| State | Background (Light) | Background (Dark) |
|-------|-------------------|-------------------|
| Rest | transparent | transparent |
| Hover | `rgba(0,0,0, 0.07)` | `rgba(255,255,255, 0.07)` |
| Active | `rgba(0,0,0, 0.12)` | `rgba(255,255,255, 0.12)` |
| Focused | transparent + 2px accent outline | transparent + 2px accent outline |
| Disabled | transparent, content opacity 0.5 | transparent, content opacity 0.5 |

### Suggested Action Button

| State | Background | Text Color |
|-------|-----------|------------|
| Rest | `#3584E4` | `#FFFFFF` |
| Hover | `#4A95EB` (lighter) | `#FFFFFF` |
| Active | `#2B6CBF` (darker) | `#FFFFFF` |
| Focused | rest + 2px accent outline, 2px offset | `#FFFFFF` |
| Disabled | `#3584E4`, opacity 0.5 | `#FFFFFF` |

### Destructive Action Button

| State | Background | Text Color |
|-------|-----------|------------|
| Rest | `#E01B24` | `#FFFFFF` |
| Hover | `#E84049` (lighter) | `#FFFFFF` |
| Active | `#BF1720` (darker) | `#FFFFFF` |
| Focused | rest + 2px outline | `#FFFFFF` |
| Disabled | rest, opacity 0.5 | `#FFFFFF` |

## Linked Groups

When buttons are placed in a linked group (e.g., segmented controls, toggle groups),
they share borders and lose inner corner radii:

| Property | Value |
|----------|-------|
| Group corner radius | 6px (outer corners only) |
| Inner corners | 0px |
| Gap between buttons | 0px (borders collapse) |
| Inner border | 1px separator |

## Icon Buttons

| Property | Value |
|----------|-------|
| Size (square) | 34x34px |
| Icon size | 16x16px |
| Padding | 9px all sides |
| Common usage | Header bar actions, toolbar buttons |

## Keyboard Support

| Key | Action |
|-----|--------|
| Space / Enter | Activate button |
| Tab | Move focus to next |
| Shift+Tab | Move focus to previous |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Background color change | 200ms | ease-in-out |
| Shadow transition | 200ms | ease-in-out |
| Active (press) | immediate (no delay) | — |

## Dija Skin Mapping

```
skin! {
    ButtonSkin {
        field main
        field label

        platform linux {
            light {
                main: {
                    min_height: 34,
                    padding: 8 16,
                    border_radius: 6,
                    background: #FFFFFF,
                    border: 1 rgba(0,0,0,0.15),
                    shadow: 0 1 2 0 rgba(0,0,0,0.07),
                }
                label: {
                    font_size: 15,
                    color: #2E3436,
                }
            }
            dark {
                main: {
                    background: #404040,
                    border: 1 rgba(255,255,255,0.15),
                }
                label: {
                    color: #FFFFFF,
                }
            }
        }
    }
}
```
