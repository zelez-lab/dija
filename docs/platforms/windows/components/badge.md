# Windows — InfoBadge

Source: WinUI 3 InfoBadge control

## Variants

| Style | Shape | Size |
|-------|-------|------|
| Dot | Circle | 4px diameter |
| Icon | Circle | 16px diameter |
| Numeric | Rounded pill | 16px height, variable width |

## Dot Badge

Minimal indicator showing presence of new content or attention needed.

| Property | Value |
|----------|-------|
| Diameter | 4px |
| Corner radius | 2px (circle) |
| Background | SystemFillColorCritical (default), or SystemFillColorCaution, SystemFillColorSuccess, SystemFillColorAttention |
| Border | None |

## Icon Badge

Circle containing a small icon glyph.

| Property | Value |
|----------|-------|
| Diameter | 16px |
| Corner radius | 8px (circle) |
| Background | SystemFillColorCritical (default) |
| Icon size | 10x10px |
| Icon color | White (`#FFFFFF`) |
| Border | None |

### Built-in Icon Types

| Type | Icon |
|------|------|
| Attention | Asterisk (`*`) |
| Informational | `i` glyph |
| Success | Checkmark |
| Critical | `!` exclamation |

## Numeric Badge

Rounded pill showing a count.

| Property | Value |
|----------|-------|
| Height | 16px |
| Min width | 16px (single digit) |
| Padding | 4px horizontal |
| Corner radius | 8px (pill shape) |
| Background | SystemFillColorCritical (default) |
| Font | 11px, SemiBold (600) |
| Text color | White (`#FFFFFF`) |
| Border | None |

### Overflow

When the number exceeds display width, the pill stretches horizontally. No built-in max-count truncation (app must handle "99+" logic).

## Color Presets

| Preset | Background color (Light) | Background color (Dark) |
|--------|-------------------------|------------------------|
| Critical (default) | `#C42B1C` | `#FF99A4` |
| Attention | SystemAccentColor | SystemAccentColor |
| Informational | SystemFillColorNeutral | SystemFillColorNeutral |
| Success | `#0F7B0F` | `#6CCB5F` |
| Caution | `#9D5D00` | `#FCE100` |

## Position

InfoBadge is designed to be placed on:

| Host | Position | Offset |
|------|----------|--------|
| NavigationViewItem | Top-right of icon area | Overlaps slightly |
| IconButton | Top-right corner | Inset by 2px |
| Tab | Top-right of tab label | Inset by 2px |
| Custom placement | Absolute position via layout |

## States

InfoBadge does not have interactive states (no hover, press, or focus). It is a pure visual indicator.

| State | Behavior |
|-------|----------|
| Value = -1 or unset | Hides the badge |
| Value = 0 | Shows dot or hides (configurable) |
| Value > 0 | Shows numeric or icon badge |

## Dija Mapping

The dija-ui Badge component maps directly:

| Dija Badge | WinUI InfoBadge |
|-----------|----------------|
| `Size::XXS` (dot) | Dot variant (4px) |
| `Size::XS` | Icon variant (16px) |
| `Size::SM` | Numeric variant (16px height) |
| Color attribute | Maps to Fluent preset colors |
