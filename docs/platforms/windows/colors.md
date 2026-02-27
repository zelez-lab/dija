# Windows — System Colors

Source: WinUI 3 XAML Theme Resources, Windows App SDK 1.5+

## Accent Colors

Windows accent color defaults to `#0078D4` (blue). The system generates a palette of lighter and darker shades for use across UI states.

### Default Accent Palette (Blue)

| Token | Hex | Usage |
|-------|-----|-------|
| SystemAccentColorLight3 | `#99EBFF` | Light theme: accent text on dark backgrounds |
| SystemAccentColorLight2 | `#4CC2FF` | Light theme: accent hover states |
| SystemAccentColorLight1 | `#0093F9` | Light theme: accent active/pressed |
| SystemAccentColor | `#0078D4` | Primary accent (user-configurable) |
| SystemAccentColorDark1 | `#005EB7` | Dark theme: accent active/pressed |
| SystemAccentColorDark2 | `#003D92` | Dark theme: accent text on light backgrounds |
| SystemAccentColorDark3 | `#001968` | Dark theme: darkest accent shade |

The accent color is user-configurable. Windows generates Light1-3 and Dark1-3 automatically from any chosen color, optimized for contrast in both themes.

### Accent Usage

| Context | Light Theme | Dark Theme |
|---------|------------|------------|
| Accent button fill | SystemAccentColor | SystemAccentColor |
| Accent button fill (hover) | SystemAccentColorDark1 | SystemAccentColorLight1 |
| Accent button fill (pressed) | SystemAccentColorDark2 | SystemAccentColorLight2 |
| Accent text | SystemAccentColorDark2 | SystemAccentColorLight2 |
| Accent text (hover) | SystemAccentColorDark1 | SystemAccentColorLight3 |
| Focus ring (outer) | Black or White (for contrast) | White or Black |
| Hyperlink text | SystemAccentColorDark1 | SystemAccentColorLight2 |
| Toggle/switch on track | SystemAccentColor | SystemAccentColor |
| Slider filled track | SystemAccentColor | SystemAccentColor |
| TextBox focus bottom stroke | SystemAccentColor | SystemAccentColor |

## Text Fill Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| TextFillColorPrimary | `#E4000000` | `#FFFFFFFF` | Primary text, labels |
| TextFillColorSecondary | `#9E000000` | `#C5FFFFFF` | Secondary text, subtitles |
| TextFillColorTertiary | `#72000000` | `#87FFFFFF` | Placeholder text |
| TextFillColorDisabled | `#5C000000` | `#5DFFFFFF` | Disabled text |
| TextFillColorInverse | `#FFFFFFFF` | `#E4000000` | Text on accent backgrounds |

### Accent Text Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| AccentTextFillColorPrimary | AccentDark2 | AccentLight2 | Hyperlinks, accent labels |
| AccentTextFillColorSecondary | AccentDark3 | AccentLight3 | Hover state accent text |
| AccentTextFillColorTertiary | AccentColor | AccentColor | Subtle accent labels |
| AccentTextFillColorDisabled | `#5C000000` | `#5DFFFFFF` | Disabled accent text |
| TextOnAccentFillColorPrimary | `#FFFFFFFF` | `#FF000000` | Text on accent button |
| TextOnAccentFillColorSecondary | `#B3FFFFFF` | `#80000000` | Secondary text on accent |
| TextOnAccentFillColorDisabled | `#FFFFFFFF` | `#87FFFFFF` | Disabled text on accent |
| TextOnAccentFillColorSelectedText | `#FFFFFFFF` | `#FFFFFFFF` | Selected text highlight |

## Control Fill Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| ControlFillColorDefault | `#B3FFFFFF` | `#0FFFFFFF` | Button/control resting state |
| ControlFillColorSecondary | `#80F9F9F9` | `#15FFFFFF` | Button hover |
| ControlFillColorTertiary | `#4DF9F9F9` | `#08FFFFFF` | Button pressed |
| ControlFillColorDisabled | `#4DF9F9F9` | `#0BFFFFFF` | Disabled controls |
| ControlFillColorTransparent | `#00FFFFFF` | `#00FFFFFF` | Transparent state |
| ControlFillColorInputActive | `#FFFFFFFF` | `#1EFFFFFF` | Active TextBox/ComboBox |

### Subtle Fill Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| SubtleFillColorTransparent | `#00FFFFFF` | `#00FFFFFF` | Subtle button rest |
| SubtleFillColorSecondary | `#09000000` | `#0FFFFFFF` | Subtle button hover |
| SubtleFillColorTertiary | `#06000000` | `#0AFFFFFF` | Subtle button pressed |
| SubtleFillColorDisabled | `#00FFFFFF` | `#00FFFFFF` | Subtle disabled |

### Accent Fill Colors

| Resource | Light | Dark | Usage |
|----------|-------|------|-------|
| AccentFillColorDefaultBrush | AccentColor | AccentColor | Accent button rest |
| AccentFillColorSecondary | AccentDark1 | AccentLight1 | Accent button hover |
| AccentFillColorTertiary | AccentDark2 | AccentLight2 | Accent button pressed |
| AccentFillColorDisabled | `#37000000` | `#28FFFFFF` | Disabled accent fill |
| AccentFillColorSelectedTextBackground | AccentColor | AccentColor | Text selection highlight |

## Control Stroke Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| ControlStrokeColorDefault | `#0F000000` | `#12FFFFFF` | Default control border |
| ControlStrokeColorSecondary | `#29000000` | `#18FFFFFF` | Secondary/bottom border |
| ControlStrokeColorOnAccentDefault | `#14FFFFFF` | `#14FFFFFF` | Border on accent surfaces |
| ControlStrokeColorOnAccentSecondary | `#66000000` | `#23000000` | Bottom border on accent |
| ControlStrokeColorOnAccentTertiary | `#37000000` | `#37000000` | Tertiary accent stroke |
| ControlStrokeColorOnAccentDisabled | `#0F000000` | `#33000000` | Disabled accent stroke |
| ControlStrokeColorForStrongFillWhenOnImage | `#59FFFFFF` | `#6B000000` | Strokes over images |

### Card and Surface Stroke Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| CardStrokeColorDefault | `#0F000000` | `#19000000` | Card border |
| CardStrokeColorDefaultSolid | `#EBEBEB` | `#1C1C1C` | Opaque card border |
| FocusStrokeColorOuter | `#E4000000` | `#FFFFFFFF` | Focus ring (outer, 2px) |
| FocusStrokeColorInner | `#B3FFFFFF` | `#B3000000` | Focus ring (inner, 1px) |
| DividerStrokeColorDefault | `#0F000000` | `#15FFFFFF` | Divider/separator stroke |
| SurfaceStrokeColorDefault | `#66757575` | `#66757575` | Surface boundaries |
| SurfaceStrokeColorFlyout | `#0F000000` | `#33000000` | Flyout border |

## Background Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| SolidBackgroundFillColorBase | `#F3F3F3` | `#202020` | App background (Mica fallback) |
| SolidBackgroundFillColorSecondary | `#EEEEEE` | `#1C1C1C` | Secondary background |
| SolidBackgroundFillColorTertiary | `#F9F9F9` | `#282828` | Tertiary/elevated background |
| SolidBackgroundFillColorQuarternary | `#FFFFFF` | `#2C2C2C` | Highest elevation solid |
| SolidBackgroundFillColorBaseAlt | `#DADADA` | `#0A0A0A` | Alternate base (behind Mica) |

### Layer Colors (for surfaces on top of Mica/Acrylic base)

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| LayerFillColorDefault | `#80FFFFFF` | `#0DFFFFFF` | Primary content layer |
| LayerFillColorAlt | `#FFFFFFFF` | `#0DFFFFFF` | Alternate content layer |
| LayerOnAcrylicFillColorDefault | `#40FFFFFF` | `#09FFFFFF` | Content on Acrylic base |
| LayerOnAccentAcrylicFillColorDefault | `#40FFFFFF` | `#09FFFFFF` | Content on accent Acrylic |
| LayerOnMicaBaseAltFillColorDefault | `#73FFFFFF` | `#0DFFFFFF` | Content on Mica Alt base |
| LayerOnMicaBaseAltFillColorSecondary | `#00FFFFFF` | `#0AFFFFFF` | Secondary on Mica Alt |
| LayerOnMicaBaseAltFillColorTertiary | `#F9F9F9` | `#0DFFFFFF` | Tertiary on Mica Alt |
| LayerOnMicaBaseAltFillColorTransparent | `#00FFFFFF` | `#00000000` | Transparent on Mica Alt |

## Signal / Status Colors

| Resource | Light | Dark | Usage |
|----------|-------|------|-------|
| SystemFillColorSuccess | `#0F7B0F` | `#6CCB5F` | Success / positive |
| SystemFillColorSuccessBackground | `#DFF6DD` | `#393D1B` | Success background |
| SystemFillColorCaution | `#9D5D00` | `#FCE100` | Warning / caution |
| SystemFillColorCautionBackground | `#FFF4CE` | `#433519` | Caution background |
| SystemFillColorCritical | `#C42B1C` | `#FF99A4` | Error / critical |
| SystemFillColorCriticalBackground | `#FDE7E9` | `#442726` | Critical background |
| SystemFillColorAttention | AccentColor | AccentColor | Informational |
| SystemFillColorAttentionBackground | `#F6F6F6` | `#08FFFFFF` | Attention background |
| SystemFillColorNeutral | `#72000000` | `#8BFFFFFF` | Neutral informational |
| SystemFillColorNeutralBackground | `#06000000` | `#08FFFFFF` | Neutral background |
| SystemFillColorSolidNeutral | `#9D9D9D` | `#9D9D9D` | Solid neutral fill |
| SystemFillColorSolidAttentionBackground | `#F7F7F7` | `#2E2E2E` | Solid attention bg |
| SystemFillColorSolidNeutralBackground | `#F3F3F3` | `#2D2D2D` | Solid neutral bg |

## Smoke / Overlay Colors

| Resource | Light (ARGB) | Dark (ARGB) | Usage |
|----------|-------------|-------------|-------|
| SmokeFillColorDefault | `#4D000000` (black@30%) | `#66000000` (black@40%) | Dialog backdrop overlay |
| BackgroundFillColorSmoke | same as above | same as above | Alias for smoke |

## Gray / Neutral Ramp

For reference, the Fluent 2 neutral ramp (approximate solids):

| Shade | Light | Dark |
|-------|-------|------|
| Grey 2 | `#F9F9F9` | `#282828` |
| Grey 4 | `#F3F3F3` | `#2C2C2C` |
| Grey 6 | `#EEEEEE` | `#333333` |
| Grey 8 | `#E6E6E6` | `#383838` |
| Grey 10 | `#DADADA` | `#404040` |
| Grey 12 | `#D1D1D1` | `#484848` |
| Grey 14 | `#C8C8C8` | `#505050` |
| Grey 20 | `#A6A6A6` | `#6E6E6E` |
| Grey 30 | `#8A8A8A` | `#8A8A8A` |
| Grey 40 | `#6E6E6E` | `#A6A6A6` |
| Grey 50 | `#505050` | `#C8C8C8` |
| Grey 60 | `#383838` | `#DADADA` |
| Grey 70 | `#2C2C2C` | `#E6E6E6` |
| Grey 80 | `#1F1F1F` | `#EEEEEE` |
| Grey 90 | `#141414` | `#F3F3F3` |
| Grey 100 | `#000000` | `#FFFFFF` |

## Color Usage Guidelines

### Semantic Color Selection

| Need | Use |
|------|-----|
| Primary text | TextFillColorPrimary |
| Secondary text | TextFillColorSecondary |
| Disabled text | TextFillColorDisabled |
| Input placeholder | TextFillColorTertiary |
| Link / hyperlink | AccentTextFillColorPrimary |
| Destructive action | SystemFillColorCritical |
| Success / confirmation | SystemFillColorSuccess |
| Warning | SystemFillColorCaution |
| App background | Mica material or SolidBackgroundFillColorBase |
| Card / surface | LayerFillColorDefault + CardStrokeColorDefault |
| Control border | ControlStrokeColorDefault |
| Focus indicator | FocusStrokeColorOuter + FocusStrokeColorInner |
| Control fill (rest) | ControlFillColorDefault |
| Control fill (hover) | ControlFillColorSecondary |
| Control fill (pressed) | ControlFillColorTertiary |
| Dialog backdrop | SmokeFillColorDefault |

### Dark Mode Notes

- Dark mode backgrounds are NOT pure black. Base is `#202020` (slightly elevated from OLED black).
- Controls use semi-transparent white overlays on dark backgrounds for depth (e.g., `#0FFFFFFF`).
- Accent colors shift lighter in dark mode for contrast.
- Mica material applies desktop wallpaper tint even in dark mode.
- Focus rings invert: outer becomes white, inner becomes semi-transparent black.
