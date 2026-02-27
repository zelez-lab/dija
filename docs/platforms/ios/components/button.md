# iOS — Button (UIButton)

Source: UIButton (iOS 15+ button configuration system)

## Variants

| Style | Background (Light) | Background (Dark) | Text Color | Border |
|-------|-------------------|-------------------|------------|--------|
| Plain | transparent | transparent | tintColor | none |
| Gray | tintColor @ 0.12 | tintColor @ 0.24 | tintColor | none |
| Tinted | tintColor @ 0.15 | tintColor @ 0.25 | tintColor | none |
| Filled | tintColor | tintColor | white | none |
| Bordered (prominent) | transparent | transparent | tintColor | 1pt tintColor |
| Bordered (tinted) | transparent | transparent | tintColor | 1pt tintColor @ 0.3 |

## Sizes

| Size | Height | Horizontal Padding | Font Size | Corner Radius |
|------|--------|-------------------|-----------|---------------|
| Mini | 28pt | 10pt | 15pt | 7pt |
| Small | 32pt | 12pt | 15pt | 8pt |
| Medium | 36pt | 14pt | 17pt | 10pt |
| Large | 50pt | 20pt | 17pt | 12pt |

Note: All sizes maintain a minimum hit target of 44x44pt. Smaller visual sizes have expanded touch areas.

## Metrics

| Property | Value |
|----------|-------|
| Corner radius (default) | 10pt (continuous/squircle) |
| Corner curve | `.continuous` (superellipse) |
| Font | SF Pro Semibold (title), SF Pro Regular (subtitle) |
| Default font size | 17pt |
| Image-to-title padding | 8pt |
| Content insets (default) | 7pt vertical, 14pt horizontal |
| Shadow | None |
| Icon size (symbol) | Matches font size (point-size based) |

## Button with Subtitle

iOS 15+ supports a subtitle below the title.

| Property | Value |
|----------|-------|
| Title font | SF Pro Semibold, 17pt |
| Subtitle font | SF Pro Regular, 12pt |
| Subtitle color | secondaryLabel |
| Vertical spacing | 2pt between title and subtitle |
| Layout | Center-aligned (default), leading, trailing |

## States

| State | Effect (Plain) | Effect (Filled) | Effect (Gray/Tinted) |
|-------|---------------|-----------------|---------------------|
| Normal | tintColor text | tintColor bg, white text | tinted bg, tintColor text |
| Highlighted (pressed) | alpha 0.3 on text | darken bg ~20% | darken bg ~15% |
| Disabled | alpha 0.3 | alpha 0.3 (entire button) | alpha 0.3 |
| Focused (tvOS/keyboard) | slight scale 1.05 | slight scale 1.05 | slight scale 1.05 |
| Selected | same as normal (no toggle visual by default) | — | — |

### Press Animation

| Property | Value |
|----------|-------|
| Highlight transition | immediate (no animation) |
| Release transition | 0.15s fade back |
| Scale (if used) | 0.97 on press, spring back 0.3s |

## Menu Button

Buttons can host a pull-down menu (iOS 14+) or pop-up menu.

| Property | Value |
|----------|-------|
| Menu indicator | Downward chevron (SF Symbol: `chevron.down`) |
| Indicator size | ~8pt, slightly below center |
| Indicator color | Same as title color, reduced opacity |
| Long-press to show | ~0.3s hold |
| Instant tap shows menu | When `showsMenuAsPrimaryAction = true` |

## Activity Indicator Button

| Property | Value |
|----------|-------|
| Indicator style | `.medium` UIActivityIndicatorView |
| Indicator replaces | Image or title (configurable) |
| Indicator color | Same as text color |

## Destructive Style

| Property | Value |
|----------|-------|
| Filled destructive bg | systemRed |
| Tinted destructive bg | systemRed @ 0.15 |
| Text color | systemRed (plain/tinted), white (filled) |
