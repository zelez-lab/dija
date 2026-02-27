# Android — Surfaces (Material Design 3)

Source: Material Design 3 guidelines (m3.material.io)

Android's signature look: **tonal elevation** (color shifts), NOT blur materials (unlike iOS).

## Tonal Elevation

M3 replaces M2 shadow-based elevation with **surface tint**: as elevation increases,
the surface color shifts toward the primary color. In dark mode this is essential
for visual hierarchy.

### Formula

```
tinted_color = blend(surface_color, primary_color, elevation_alpha)
```

Where `elevation_alpha` maps from elevation level to tint amount:

| Elevation level | dp | Tint opacity (dark) | Tint opacity (light) |
|----------------|-----|--------------------|--------------------|
| 0 | 0dp | 0% | 0% |
| 1 | 1dp | 5% | 5% |
| 2 | 3dp | 8% | 8% |
| 3 | 6dp | 11% | 11% |
| 4 | 8dp | 12% | 12% |
| 5 | 12dp | 14% | 14% |

In practice, light theme uses **distinct surface container tokens** rather than
computed tint. Tonal elevation is most visible in dark theme.

## Surface Containers

M3 provides 5 surface container roles for layered UI, replacing computed tint
with explicit design tokens:

| Role | Light hex | Dark hex | Usage |
|------|-----------|----------|-------|
| Surface container lowest | `#FFFFFF` | `#0F0D13` | Deepest background layer |
| Surface container low | `#F7F2FA` | `#1D1B20` | Recessed areas, side sheets |
| Surface container | `#F3EDF7` | `#211F26` | Default cards, sheets |
| Surface container high | `#ECE6F0` | `#2B2930` | Search bars, menus |
| Surface container highest | `#E6E0E9` | `#36343B` | Navigation drawers, input surfaces |

Additionally:

| Role | Light hex | Dark hex | Usage |
|------|-----------|----------|-------|
| Surface | `#FEF7FF` | `#141218` | Page/scaffold background |
| Surface dim | `#DED8E1` | `#141218` | Dimmed surface variant |
| Surface bright | `#FEF7FF` | `#3B383E` | Elevated bright surface |

## No Blur Materials

Unlike iOS (which uses backdrop blur + saturation boost for translucency),
M3 uses **opaque surfaces with tonal color** for hierarchy. There is no blur,
no translucency, no vibrancy.

| iOS concept | M3 equivalent |
|------------|---------------|
| Ultra thin material | Surface container lowest |
| Thin material | Surface container low |
| Regular material | Surface container |
| Thick material | Surface container high |
| Ultra thick material | Surface container highest |
| Backdrop blur | Not used |
| Saturation boost | Not used |

## Component Surface Mapping

| Component | Surface role | Elevation |
|-----------|-------------|-----------|
| Scaffold background | Surface | Level 0 |
| Card (filled) | Surface container highest | Level 0 |
| Card (elevated) | Surface container low | Level 1 |
| Card (outlined) | Surface | Level 0 |
| Bottom sheet | Surface container low | Level 1 |
| Navigation bar | Surface container | Level 2 |
| Navigation drawer | Surface container low | Level 1 |
| Navigation rail | Surface | Level 0 |
| Top app bar | Surface | Level 0 (Level 2 scrolled) |
| Dialog | Surface container high | Level 3 |
| Menu | Surface container | Level 2 |
| FAB | Primary container | Level 3 |
| Snackbar | Inverse surface | Level 3 |
| Search bar | Surface container high | Level 2 |
| Bottom app bar | Surface container | Level 2 |

## Scrim

Modal surfaces (dialogs, modal sheets) use a scrim overlay on the content behind:

- Color: `#000000` (scrim token)
- Opacity: 32%
- No blur

## Comparison with iOS

| Property | iOS | M3 (Android) |
|----------|-----|-------------|
| Translucency | Core feature (blur + tint) | Not used |
| Elevation visual | Drop shadows only | Tonal color shift + optional shadows |
| Dark mode hierarchy | Elevated = lighter gray | Elevated = primary-tinted surface |
| Corner shape | Superellipse (squircle) | Standard circular radius |
| Surface container tokens | None (material levels) | 5 explicit container roles |
