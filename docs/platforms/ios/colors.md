# iOS — System Colors

Source: Apple Human Interface Guidelines (iOS 17+), UIColor API

## Label Colors

Hierarchical text colors from highest to lowest contrast.

| Name | Light | Dark | Usage |
|------|-------|------|-------|
| label | `#000000` (alpha 1.0) | `#FFFFFF` (alpha 1.0) | Primary content |
| secondaryLabel | `#3C3C43` (alpha 0.60) | `#EBEBF5` (alpha 0.60) | Subheadings, subtitles |
| tertiaryLabel | `#3C3C43` (alpha 0.30) | `#EBEBF5` (alpha 0.30) | Placeholder text, tertiary info |
| quaternaryLabel | `#3C3C43` (alpha 0.18) | `#EBEBF5` (alpha 0.18) | Disabled text, watermarks |
| placeholderText | `#3C3C43` (alpha 0.30) | `#EBEBF5` (alpha 0.30) | Input placeholder (same as tertiaryLabel) |

## Fill Colors

Overlay fills for thin UI elements like switches, sliders, and progress bars.

| Name | Light | Dark | Usage |
|------|-------|------|-------|
| systemFill | `#787880` (alpha 0.20) | `#787880` (alpha 0.36) | Thin overlays (switch track, slider) |
| secondarySystemFill | `#787880` (alpha 0.16) | `#787880` (alpha 0.32) | Secondary fills |
| tertiarySystemFill | `#767680` (alpha 0.12) | `#767680` (alpha 0.24) | Tertiary fills |
| quaternarySystemFill | `#747480` (alpha 0.08) | `#747480` (alpha 0.18) | Large area fills |

## Backgrounds (Plain Style)

For views without grouped table sections.

| Name | Light | Dark | Usage |
|------|-------|------|-------|
| systemBackground | `#FFFFFF` | `#000000` | Primary background |
| secondarySystemBackground | `#F2F2F7` | `#1C1C1E` | Grouped sections, inset content |
| tertiarySystemBackground | `#FFFFFF` | `#2C2C2E` | Third-level grouping |

## Backgrounds (Grouped Style)

For grouped table views and settings screens.

| Name | Light | Dark | Usage |
|------|-------|------|-------|
| systemGroupedBackground | `#F2F2F7` | `#000000` | Behind grouped sections |
| secondarySystemGroupedBackground | `#FFFFFF` | `#1C1C1E` | Grouped cell fill |
| tertiarySystemGroupedBackground | `#F2F2F7` | `#2C2C2E` | Third-level grouped content |

## Separator Colors

| Name | Light | Dark | Usage |
|------|-------|------|-------|
| separator | `#3C3C43` (alpha 0.29) | `#545458` (alpha 0.60) | Standard separator (partially transparent) |
| opaqueSeparator | `#C6C6C8` | `#38383A` | Separator that needs to be fully opaque |

## Tint Colors (System Accent Colors)

| Name | Light | Dark | Accessible Light | Accessible Dark |
|------|-------|------|------------------|-----------------|
| systemBlue | `#007AFF` | `#0A84FF` | `#0040DD` | `#409CFF` |
| systemGreen | `#34C759` | `#30D158` | `#248A3D` | `#30DB5B` |
| systemRed | `#FF3B30` | `#FF453A` | `#D70015` | `#FF6961` |
| systemOrange | `#FF9500` | `#FF9F0A` | `#C93400` | `#FFB340` |
| systemYellow | `#FFCC00` | `#FFD60A` | `#A05A00` | `#FFD426` |
| systemPurple | `#AF52DE` | `#BF5AF2` | `#8944AB` | `#DA8FFF` |
| systemPink | `#FF2D55` | `#FF375F` | `#D30F45` | `#FF6482` |
| systemTeal | `#30B0C7` | `#40C8E0` | `#008299` | `#70D7EF` |
| systemIndigo | `#5856D6` | `#5E5CE6` | `#3634A3` | `#7D7AFF` |
| systemCyan | `#32ADE6` | `#64D2FF` | `#0071A4` | `#70D7FF` |
| systemMint | `#00C7BE` | `#63E6E2` | `#12A594` | `#66D4CF` |
| systemBrown | `#A2845E` | `#AC8E68` | `#7C6545` | `#B59469` |

Note: "Accessible" variants are the high-contrast versions for accessibility (`.accessibilityContrast(.high)`).

## Gray Scale

| Name | Light | Dark | Usage |
|------|-------|------|-------|
| systemGray | `#8E8E93` | `#8E8E93` | Default gray |
| systemGray2 | `#AEAEB2` | `#636366` | Secondary gray |
| systemGray3 | `#C7C7CC` | `#48484A` | Tertiary gray |
| systemGray4 | `#D1D1D6` | `#3A3A3C` | Quaternary gray |
| systemGray5 | `#E5E5EA` | `#2C2C2E` | Quinary gray |
| systemGray6 | `#F2F2F7` | `#1C1C1E` | Senary gray |

Note: In light mode, grays go from medium (`systemGray`) to very light (`systemGray6`). In dark mode, grays go from medium (`systemGray`) to very dark (`systemGray6`). The scale inverts.

## Link Color

| Name | Light | Dark |
|------|-------|------|
| link | `#007AFF` | `#0984FF` |

## Non-Adaptable Standard Colors

Fixed colors that do NOT change between light and dark mode.

| Name | Hex |
|------|-----|
| .black | `#000000` |
| .blue | `#0000FF` |
| .brown | `#996633` |
| .cyan | `#00FFFF` |
| .darkGray | `#555555` |
| .gray | `#7F7F7F` |
| .green | `#00FF00` |
| .lightGray | `#AAAAAA` |
| .magenta | `#FF00FF` |
| .orange | `#FF7F00` |
| .purple | `#7F007F` |
| .red | `#FF0000` |
| .white | `#FFFFFF` |
| .yellow | `#FFFF00` |

These are the classic UIColor constants, NOT the semantic system colors. Prefer the system colors above for adaptive UI.

## Color Usage Guidelines

### Semantic Color Selection

| Need | Use |
|------|-----|
| Primary text | `label` |
| Secondary text | `secondaryLabel` |
| Disabled text | `quaternaryLabel` or control alpha 0.3 |
| Input placeholder | `placeholderText` |
| Clickable text (link) | `link` or `systemBlue` |
| Destructive action | `systemRed` |
| Success / confirmation | `systemGreen` |
| Warning | `systemOrange` |
| Page background | `systemBackground` or `systemGroupedBackground` |
| Card / cell background | `secondarySystemBackground` or `secondarySystemGroupedBackground` |
| Thin separator | `separator` |
| Thick separator or border | `opaqueSeparator` |
| Switch track (off) | `systemFill` (effectively `systemGray4` in earlier iOS) |
| Progress track | `systemFill` |

### Dark Mode Notes

- Dark mode backgrounds are near-pure black (`#000000`) for OLED power savings.
- Dark mode uses *elevated* colors for surfaces above the base level (sheets, popovers get `#1C1C1E` not `#000000`).
- Tint colors shift slightly brighter in dark mode for better contrast against dark backgrounds.
- Vibrancy is used extensively in dark mode — colors are rendered semi-transparent over blurred backgrounds for depth.
