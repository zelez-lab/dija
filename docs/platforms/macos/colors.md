# macOS System Colors

Reference: NSColor (AppKit), Apple Human Interface Guidelines (macOS 14+).

All values measured on macOS Sonoma 14 with default accent color (Multicolor) and standard contrast. Colors are in sRGB color space. Dynamic colors change automatically between light and dark appearances.

## Accent System Colors

These are the tinted semantic colors that adjust between light and dark mode.

| Name           | Light Mode         | Dark Mode          |
|----------------|--------------------|--------------------|
| systemRed      | `#FF3B30`          | `#FF453A`          |
| systemOrange   | `#FF9500`          | `#FF9F0A`          |
| systemYellow   | `#FFCC00`          | `#FFD60A`          |
| systemGreen    | `#34C759`          | `#30D158`          |
| systemMint     | `#00C7BE`          | `#63E6E2`          |
| systemTeal     | `#30B0C7`          | `#40CBE0`          |
| systemCyan     | `#32ADE6`          | `#64D2FF`          |
| systemBlue     | `#007AFF`          | `#0A84FF`          |
| systemIndigo   | `#5856D6`          | `#5E5CE6`          |
| systemPurple   | `#AF52DE`          | `#BF5AF2`          |
| systemPink     | `#FF2D55`          | `#FF375F`          |
| systemBrown    | `#A2845E`          | `#AC8E68`          |

### Accent Color

The user-chosen accent color (`NSColor.controlAccentColor`) defaults to `systemBlue` but can be any of these system tints, or the "Multicolor" setting which uses different accent colors per context.

| Setting     | Light Mode  | Dark Mode   |
|-------------|-------------|-------------|
| Blue        | `#007AFF`   | `#0A84FF`   |
| Purple      | `#953D96`   | `#A550A7`   |
| Pink        | `#F74F9E`   | `#F55DA0`   |
| Red         | `#E0383E`   | `#E44043`   |
| Orange      | `#D96A21`   | `#DB7529`   |
| Yellow      | `#DFA92C`   | `#E2B037`   |
| Green       | `#62BA46`   | `#6BBF4E`   |
| Graphite    | `#8C8C8C`   | `#98989D`   |

## Label Colors

Used for text and symbols at varying prominence levels. These use alpha transparency over backgrounds.

| Name                    | Light Mode            | Dark Mode             |
|-------------------------|-----------------------|-----------------------|
| labelColor              | `rgba(0,0,0,0.85)`   | `rgba(255,255,255,0.85)` |
| secondaryLabelColor     | `rgba(0,0,0,0.50)`   | `rgba(255,255,255,0.55)` |
| tertiaryLabelColor      | `rgba(0,0,0,0.26)`   | `rgba(255,255,255,0.25)` |
| quaternaryLabelColor    | `rgba(0,0,0,0.10)`   | `rgba(255,255,255,0.10)` |

Approximate opaque equivalents on white/dark backgrounds:

| Name                    | Light (on white)  | Dark (on #1E1E1E)  |
|-------------------------|-------------------|---------------------|
| labelColor              | `#262626`         | `#E5E5E5`           |
| secondaryLabelColor     | `#808080`         | `#A0A0A0`           |
| tertiaryLabelColor      | `#BDBDBD`         | `#6B6B6B`           |
| quaternaryLabelColor    | `#E6E6E6`         | `#474747`           |

## Text Colors

| Name                    | Light Mode    | Dark Mode     |
|-------------------------|---------------|---------------|
| textColor               | `#000000`     | `#FFFFFF`     |
| placeholderTextColor    | `rgba(0,0,0,0.25)` | `rgba(255,255,255,0.25)` |
| selectedTextColor       | `#000000`     | `#FFFFFF`     |
| textBackgroundColor     | `#FFFFFF`     | `#1E1E1E`    |
| selectedTextBackgroundColor | `#B3D7FF` | `#3F638B`    |

## Background Colors

| Name                        | Light Mode        | Dark Mode         |
|-----------------------------|-------------------|-------------------|
| windowBackgroundColor       | `#ECECEC`         | `#323232`         |
| underPageBackgroundColor    | `#969696`         | `#282828`         |
| controlBackgroundColor      | `#FFFFFF`         | `#1E1E1E`         |
| textBackgroundColor         | `#FFFFFF`         | `#1E1E1E`         |
| windowFrameTextColor        | `rgba(0,0,0,0.85)` | `rgba(255,255,255,0.85)` |

### Grouped Backgrounds (for grouped content areas)

| Name                                  | Light Mode  | Dark Mode   |
|---------------------------------------|-------------|-------------|
| systemGroupedBackground (primary)     | `#F2F2F7`   | `#1C1C1E`   |
| secondarySystemGroupedBackground      | `#FFFFFF`   | `#2C2C2E`   |
| tertiarySystemGroupedBackground       | `#F2F2F7`   | `#3A3A3C`   |

## Control Colors

| Name                        | Light Mode             | Dark Mode              |
|-----------------------------|------------------------|------------------------|
| controlColor                | `rgba(0,0,0,0.06)`    | `rgba(255,255,255,0.10)` |
| controlTextColor            | `rgba(0,0,0,0.85)`    | `rgba(255,255,255,0.85)` |
| disabledControlTextColor    | `rgba(0,0,0,0.25)`    | `rgba(255,255,255,0.25)` |
| selectedControlColor        | `#B3D7FF`              | `#3F638B`              |
| selectedControlTextColor    | `rgba(0,0,0,0.85)`    | `rgba(255,255,255,0.85)` |
| alternateSelectedControlTextColor | `#FFFFFF`        | `#FFFFFF`              |
| controlAccentColor          | `#007AFF`              | `#0A84FF`              |

## Fill Colors

Overlay fills applied on top of backgrounds for UI chrome. Increasing opacity for each level.

| Name                    | Light Mode            | Dark Mode                |
|-------------------------|-----------------------|--------------------------|
| systemFill              | `rgba(0,0,0,0.05)`   | `rgba(255,255,255,0.05)` |
| secondarySystemFill     | `rgba(0,0,0,0.08)`   | `rgba(255,255,255,0.08)` |
| tertiarySystemFill      | `rgba(0,0,0,0.12)`   | `rgba(255,255,255,0.12)` |
| quaternarySystemFill    | `rgba(0,0,0,0.18)`   | `rgba(255,255,255,0.18)` |

## Separator Colors

| Name                    | Light Mode            | Dark Mode                |
|-------------------------|-----------------------|--------------------------|
| separatorColor          | `rgba(0,0,0,0.10)`   | `rgba(255,255,255,0.10)` |
| gridColor               | `#DCDCDC`             | `#3A3A3A`                |

## Other UI Colors

| Name                    | Light Mode            | Dark Mode                |
|-------------------------|-----------------------|--------------------------|
| highlightColor          | `#FFFFFF`             | `#636366`                |
| shadowColor             | `#000000`             | `#000000`                |
| linkColor               | `#007AFF`             | `#0A84FF`                |
| findHighlightColor      | `#FFFF00`             | `#FFFF00`                |
| keyboardFocusIndicatorColor | `rgba(0,122,255,0.50)` | `rgba(10,132,255,0.50)` |
| unemphasizedSelectedContentBackgroundColor | `#DCDCDC` | `#464646`   |
| unemphasizedSelectedTextBackgroundColor | `#DCDCDC`    | `#464646`   |
| unemphasizedSelectedTextColor | `#000000`        | `#FFFFFF`   |

## Table / List Colors

| Name                                    | Light Mode        | Dark Mode         |
|-----------------------------------------|-------------------|-------------------|
| alternatingContentBackgroundColor (even) | `#FFFFFF`         | `#1E1E1E`         |
| alternatingContentBackgroundColor (odd)  | `#F4F5F5`         | `#232323`         |
| selectedContentBackgroundColor           | `#0063E1`         | `#0058D0`         |
| headerTextColor                          | `rgba(0,0,0,0.85)` | `rgba(255,255,255,0.85)` |

## Sidebar-Specific Colors

When a table view uses `.sourceList` style, selection uses the accent color with vibrancy:

| State                    | Light Mode         | Dark Mode          |
|--------------------------|--------------------|--------------------|
| Selected row background  | Accent-tinted blur | Accent-tinted blur |
| Selected row text        | `#FFFFFF`          | `#FFFFFF`          |
| Unselected row text      | labelColor         | labelColor         |
| Group header text        | secondaryLabelColor | secondaryLabelColor |

## Color Usage Guidelines for Dija Skins

| Semantic Role          | NSColor Name                    | Fallback Opaque Light | Fallback Opaque Dark |
|------------------------|---------------------------------|-----------------------|----------------------|
| Primary text           | `labelColor`                    | `#262626`             | `#E5E5E5`           |
| Secondary text         | `secondaryLabelColor`           | `#808080`             | `#A0A0A0`           |
| Disabled text          | `disabledControlTextColor`      | `#BFBFBF`             | `#606060`           |
| Control fill           | `controlColor`                  | `#F0F0F0`             | `#3A3A3A`           |
| Input background       | `controlBackgroundColor`        | `#FFFFFF`             | `#1E1E1E`           |
| Page background        | `windowBackgroundColor`         | `#ECECEC`             | `#323232`           |
| Border / separator     | `separatorColor`                | `#E6E6E6`             | `#3A3A3A`           |
| Accent / interactive   | `controlAccentColor`            | `#007AFF`             | `#0A84FF`           |
| Destructive            | `systemRed`                     | `#FF3B30`             | `#FF453A`           |
| Success                | `systemGreen`                   | `#34C759`             | `#30D158`           |
| Warning                | `systemYellow`                  | `#FFCC00`             | `#FFD60A`           |
