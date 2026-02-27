# Android — Color System (Material Design 3)

Source: Material Design 3 guidelines (m3.material.io), baseline purple theme

## Color Roles

M3 organizes colors into roles (semantic meaning), not raw palette values.
The baseline theme uses purple (#6750A4) as the seed/primary key color.

### Primary, Secondary, Tertiary, Error

| Role | Light | Dark |
|------|-------|------|
| primary | `#6750A4` | `#D0BCFF` |
| onPrimary | `#FFFFFF` | `#381E72` |
| primaryContainer | `#EADDFF` | `#4F378B` |
| onPrimaryContainer | `#21005D` | `#EADDFF` |
| secondary | `#625B71` | `#CCC2DC` |
| onSecondary | `#FFFFFF` | `#332D41` |
| secondaryContainer | `#E8DEF8` | `#4A4458` |
| onSecondaryContainer | `#1D192B` | `#E8DEF8` |
| tertiary | `#7D5260` | `#EFB8C8` |
| onTertiary | `#FFFFFF` | `#492532` |
| tertiaryContainer | `#FFD8E4` | `#633B48` |
| onTertiaryContainer | `#31111D` | `#FFD8E4` |
| error | `#B3261E` | `#F2B8B5` |
| onError | `#FFFFFF` | `#601410` |
| errorContainer | `#F9DEDC` | `#8C1D18` |
| onErrorContainer | `#410E0B` | `#F9DEDC` |

### Surface and Background

| Role | Light | Dark |
|------|-------|------|
| surface | `#FEF7FF` | `#141218` |
| onSurface | `#1D1B20` | `#E6E0E9` |
| surfaceVariant | `#E7E0EC` | `#49454F` |
| onSurfaceVariant | `#49454F` | `#CAC4D0` |
| surfaceDim | `#DED8E1` | `#141218` |
| surfaceBright | `#FEF7FF` | `#3B383E` |
| surfaceContainerLowest | `#FFFFFF` | `#0F0D13` |
| surfaceContainerLow | `#F7F2FA` | `#1D1B20` |
| surfaceContainer | `#F3EDF7` | `#211F26` |
| surfaceContainerHigh | `#ECE6F0` | `#2B2930` |
| surfaceContainerHighest | `#E6E0E9` | `#36343B` |
| inverseSurface | `#322F35` | `#E6E0E9` |
| inverseOnSurface | `#F5EFF7` | `#322F35` |
| inversePrimary | `#D0BCFF` | `#6750A4` |

### Outline and Utility

| Role | Light | Dark |
|------|-------|------|
| outline | `#79747E` | `#938F99` |
| outlineVariant | `#CAC4D0` | `#49454F` |
| scrim | `#000000` | `#000000` |
| shadow | `#000000` | `#000000` |

## Tonal Palettes

M3 generates 13 tones per key color (0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 95, 99, 100).
Color roles map to specific tones:

### Tone Mapping (Light / Dark)

| Role | Light tone | Dark tone |
|------|-----------|----------|
| primary | 40 | 80 |
| onPrimary | 100 | 20 |
| primaryContainer | 90 | 30 |
| onPrimaryContainer | 10 | 90 |
| surface | 98 | 6 |
| onSurface | 10 | 90 |
| surfaceContainerLowest | 100 | 4 |
| surfaceContainerLow | 96 | 10 |
| surfaceContainer | 94 | 12 |
| surfaceContainerHigh | 92 | 17 |
| surfaceContainerHighest | 90 | 22 |

### Baseline Primary Tonal Palette (#6750A4 seed)

| Tone | Hex |
|------|-----|
| 0 | `#000000` |
| 10 | `#21005D` |
| 20 | `#381E72` |
| 30 | `#4F378B` |
| 40 | `#6750A4` |
| 50 | `#7F67BE` |
| 60 | `#9A82DB` |
| 70 | `#B69DF8` |
| 80 | `#D0BCFF` |
| 90 | `#EADDFF` |
| 95 | `#F6EDFF` |
| 99 | `#FFFBFE` |
| 100 | `#FFFFFF` |

### Baseline Neutral Tonal Palette

| Tone | Hex |
|------|-----|
| 0 | `#000000` |
| 4 | `#0F0D13` |
| 6 | `#141218` |
| 10 | `#1D1B20` |
| 12 | `#211F26` |
| 17 | `#2B2930` |
| 20 | `#322F35` |
| 22 | `#36343B` |
| 24 | `#3B383E` |
| 30 | `#48464C` |
| 40 | `#605D64` |
| 50 | `#79767D` |
| 60 | `#938F96` |
| 70 | `#AEA9B1` |
| 80 | `#CAC5CD` |
| 87 | `#DED8E1` |
| 90 | `#E6E1E9` |
| 92 | `#ECE6F0` |
| 94 | `#F3EDF7` |
| 95 | `#F5EFF7` |
| 96 | `#F7F2FA` |
| 98 | `#FEF7FF` |
| 99 | `#FFFBFE` |
| 100 | `#FFFFFF` |

### Baseline Neutral-Variant Tonal Palette

| Tone | Hex |
|------|-----|
| 0 | `#000000` |
| 10 | `#1D192B` |
| 20 | `#332D41` |
| 30 | `#49454F` |
| 40 | `#625B71` |
| 50 | `#7A7289` |
| 60 | `#958DA5` |
| 70 | `#B0A7C0` |
| 80 | `#CAC4D0` |
| 90 | `#E7E0EC` |
| 95 | `#F5EEFA` |
| 99 | `#FFFBFE` |
| 100 | `#FFFFFF` |

## Dynamic Color

On Android 12+, M3 supports **dynamic color** extracted from the user's wallpaper.
The system generates a full tonal palette from the wallpaper's dominant color and
provides it as `dynamicLightColorScheme()` / `dynamicDarkColorScheme()`.

Dija must support both:
- Static baseline theme (the hex values above)
- Dynamic color (runtime palette from platform API)

## State Layer Colors

Interactive state feedback uses a color overlay (state layer) on top of the component:

| State | Opacity | Color source |
|-------|---------|-------------|
| Hover | 8% | Content color |
| Focus | 10% | Content color |
| Pressed | 10% | Content color |
| Dragged | 16% | Content color |
| Disabled (container) | 12% | onSurface |
| Disabled (content) | 38% | onSurface |

"Content color" = the `on*` color for that surface (e.g., onPrimary for primary buttons).
