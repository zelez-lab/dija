# iOS — Table View (UITableView)

Source: UITableView, UITableViewCell, SwiftUI List

## Table Styles

| Style | Background | Cell Shape | Usage |
|-------|-----------|------------|-------|
| Plain | systemBackground | Full-width cells | Contacts, music lists |
| Grouped | systemGroupedBackground | Rounded sections | Settings, forms |
| Inset Grouped | systemGroupedBackground | Rounded + inset sections | Modern settings (iOS 13+) |

## Section Background

| Style | Light | Dark |
|-------|-------|------|
| Plain | systemBackground (`#FFFFFF`) | `#000000` |
| Grouped | systemGroupedBackground (`#F2F2F7`) | `#000000` |
| Inset Grouped | systemGroupedBackground (`#F2F2F7`) | `#000000` |

## Cell

| Property | Light | Dark |
|----------|-------|------|
| Background (grouped) | secondarySystemGroupedBackground (`#FFFFFF`) | `#1C1C1E` |
| Background (plain) | systemBackground (`#FFFFFF`) | `#000000` |
| Corner radius (inset grouped) | 13pt (first/last cells rounded, middle cells square) | |
| Corner curve | `.continuous` (superellipse) | |
| Selection highlight | systemGray4 (`#D1D1D6`) fill | systemGray4 (`#3A3A3C`) fill |

## Cell Heights

| Cell Style | Default Height | Notes |
|-----------|---------------|-------|
| Default | 44pt | Single line, icon + text |
| Subtitle | 58pt (approx) | Title + subtitle |
| Value 1 (right detail) | 44pt | Title left, detail right |
| Value 2 (left detail) | 44pt | Blue label left, title right |
| Custom | Self-sizing | Auto Layout determines height |

## Cell Content Layout

| Property | Value |
|----------|-------|
| Left inset (content) | 20pt (16pt on compact width) |
| Right inset (content) | 20pt (16pt on compact width) |
| Image-to-text spacing | 15pt |
| Title font | SF Pro Regular, 17pt |
| Title color | label |
| Subtitle font | SF Pro Regular, 15pt |
| Subtitle color | secondaryLabel |
| Detail font | SF Pro Regular, 17pt |
| Detail color | secondaryLabel |

## Accessories

| Accessory | Icon | Size | Color |
|-----------|------|------|-------|
| Disclosure indicator | Chevron right (>)  | ~8 x 13pt | systemGray3 |
| Detail disclosure | Info (i) circle + chevron | ~20pt circle | tintColor |
| Checkmark | Checkmark | ~14 x 11pt | tintColor |
| Detail button | Info (i) circle | ~22pt | tintColor |
| Switch | UISwitch | 51 x 31pt | — |

Accessory right margin: 16pt from cell trailing edge.

## Separator

| Property | Value |
|----------|-------|
| Width | 0.33pt (1px on 3x retina) |
| Color | separator (`#3C3C43` @ 0.29 / `#545458` @ 0.60) |
| Left inset (default) | 20pt (aligns with text, not icon) |
| Left inset (with image) | 59pt (after image + spacing) |
| Right inset | 0pt (extends to edge) |
| Last cell | No bottom separator |

## Section Header / Footer

| Property | Value |
|----------|-------|
| Font | SF Pro Regular, 13pt |
| Color (header) | secondaryLabel |
| Color (footer) | secondaryLabel |
| Text case (grouped) | Uppercase (header), sentence case (footer) |
| Padding (header top) | 22pt |
| Padding (header bottom) | 8pt |
| Padding (footer top) | 8pt |
| Padding (footer bottom) | 22pt |
| Left inset | 20pt |
| Section-to-section gap | ~35pt (header-to-header in grouped) |

## Swipe Actions

| Property | Value |
|----------|-------|
| Leading actions | Custom (mark read, pin, etc.) |
| Trailing actions | Delete, custom |
| Action button height | Same as cell height |
| Delete button color | systemRed (`#FF3B30` / `#FF453A`) |
| Action label font | SF Pro Regular, 15pt |
| Action label color | white |
| Full swipe threshold | ~75% of cell width |
| Full swipe | Triggers first action automatically |

### Standard Swipe Action Colors

| Action | Color |
|--------|-------|
| Delete | systemRed |
| Archive | systemPurple or systemOrange |
| Flag | systemOrange |
| More | systemGray |
| Mute | systemIndigo |
| Pin | systemYellow |

## Selection

| Property | Value |
|----------|-------|
| Single selection highlight | systemGray4 fill |
| Multi-selection checkmark | tintColor circle with checkmark |
| Multi-selection circle (unselected) | 22pt, 2pt border, systemGray3 |
| Multi-selection circle (selected) | 22pt, filled tintColor, white checkmark |
| Selection animation | Fade highlight in ~0.1s, fade out ~0.3s |

## Pull to Refresh

| Property | Value |
|----------|-------|
| Spinner | UIActivityIndicatorView.medium |
| Spinner color | secondaryLabel |
| Pull distance to trigger | ~60pt |
| Spinner position | Centered, ~40pt above content |
| Animation | Spring back after release |

## Editing Mode

| Property | Value |
|----------|-------|
| Delete button (left) | Red circle with white minus |
| Reorder control (right) | Three horizontal lines (grip handle) |
| Delete button size | 22pt circle |
| Reorder handle color | systemGray2 |
| Cell indent (editing) | 38pt from left |
| Transition | 0.3s ease-in-out |

## Accessibility

| Property | Value |
|----------|-------|
| Role | Cell (static content), Button (interactive) |
| Swipe actions | VoiceOver: custom actions rotor |
| VoiceOver | "[Title], [subtitle], [accessory type]" |
