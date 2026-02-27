# Android — Design Tokens (Material Design 3)

Source: Material Design 3 guidelines (m3.material.io), Android 14+

## Corner Radii (Shape System)

M3 uses standard `border-radius` (circular arcs), NOT superellipse like iOS.

| Shape scale | Value | Usage |
|-------------|-------|-------|
| None | 0dp | Sharp rectangles (full-screen surfaces) |
| Extra-small | 4dp | Autocomplete menu, select menu, snackbar, text field (outlined) |
| Small | 8dp | Chips, rich tooltip |
| Medium | 12dp | Cards, small FAB |
| Large | 16dp | Extended FAB, FAB, navigation drawer |
| Extra-large | 28dp | Bottom sheet, dialog, large FAB, search bar, time picker |
| Full | 9999dp (pill) | Badges, buttons, sliders, switches, search bar (docked) |

Extra-small top-only variant (4dp top, 0dp bottom) used by filled text field.

## Shadows (Elevation System)

M3 prefers **tonal elevation** (surface tint) over drop shadows. Shadows are reserved
for components that need visual separation (menus, dialogs, FABs).

| Level | dp | Shadow usage | Components |
|-------|-----|-------------|------------|
| 0 | 0dp | No shadow | Filled button, outlined card, text field |
| 1 | 1dp | Minimal | Elevated card, bottom app bar, top app bar (scrolled) |
| 2 | 3dp | Low | Elevated button, bottom sheet (standard), navigation bar |
| 3 | 6dp | Medium | FAB, snackbar |
| 4 | 8dp | High | (hover states) |
| 5 | 12dp | Highest | (drag states) |

Shadow rendering uses two layers (key light + ambient):

| Level | Key light offset | Key light blur | Ambient blur |
|-------|-----------------|----------------|--------------|
| 1 | (0, 1dp) | 2dp | 1dp |
| 2 | (0, 1dp) | 3dp | 3dp |
| 3 | (0, 3dp) | 5dp | 6dp |
| 4 | (0, 4dp) | 6dp | 8dp |
| 5 | (0, 6dp) | 10dp | 12dp |

Shadow color: black @ 0.30 (key light), black @ 0.15 (ambient).

## Typography (Type Scale)

Default font: Roboto. Two weights: Regular (400), Medium (500).

| Role | Font | Weight | Size (sp) | Line height (sp) | Letter spacing (sp) |
|------|------|--------|-----------|-------------------|---------------------|
| Display Large | Roboto | Regular 400 | 57 | 64 | -0.25 |
| Display Medium | Roboto | Regular 400 | 45 | 52 | 0 |
| Display Small | Roboto | Regular 400 | 36 | 44 | 0 |
| Headline Large | Roboto | Regular 400 | 32 | 40 | 0 |
| Headline Medium | Roboto | Regular 400 | 28 | 36 | 0 |
| Headline Small | Roboto | Regular 400 | 24 | 32 | 0 |
| Title Large | Roboto | Regular 400 | 22 | 28 | 0 |
| Title Medium | Roboto | Medium 500 | 16 | 24 | 0.15 |
| Title Small | Roboto | Medium 500 | 14 | 20 | 0.1 |
| Body Large | Roboto | Regular 400 | 16 | 24 | 0.5 |
| Body Medium | Roboto | Regular 400 | 14 | 20 | 0.25 |
| Body Small | Roboto | Regular 400 | 12 | 16 | 0.4 |
| Label Large | Roboto | Medium 500 | 14 | 20 | 0.1 |
| Label Medium | Roboto | Medium 500 | 12 | 16 | 0.5 |
| Label Small | Roboto | Medium 500 | 11 | 16 | 0.5 |

## Spacing

4dp base grid. Content paddings:

| Token | Value |
|-------|-------|
| Compact | 4dp |
| Small | 8dp |
| Medium | 12dp |
| Large | 16dp |
| Extra-large | 24dp |
| XXL | 32dp |

Screen edge margins: 16dp (compact), 24dp (medium), 32dp (expanded).

Touch target minimum: 48dp x 48dp.

## Motion

### Easing Curves

| Token | Cubic bezier | Usage |
|-------|-------------|-------|
| Standard | (0.2, 0.0, 0, 1.0) | General transitions |
| Standard decelerate | (0, 0, 0, 1) | Elements entering screen |
| Standard accelerate | (0.3, 0, 1, 1) | Elements leaving screen |
| Emphasized | (0.2, 0.0, 0, 1.0) | Important transitions (same as standard) |
| Emphasized decelerate | (0.05, 0.7, 0.1, 1.0) | Overshooting enter |
| Emphasized accelerate | (0.3, 0.0, 0.8, 0.15) | Dramatic exit |
| Legacy (M2) | (0.4, 0.0, 0.2, 1.0) | Backward compat |

### Duration Tokens

| Token | ms | Usage |
|-------|-----|-------|
| Short 1 | 50 | Micro-interactions (ripple start) |
| Short 2 | 100 | Small state changes |
| Short 3 | 150 | Icon transitions |
| Short 4 | 200 | Small component transitions |
| Medium 1 | 250 | Medium component transitions |
| Medium 2 | 300 | Page element transitions |
| Medium 3 | 350 | Navigation transitions |
| Medium 4 | 400 | Complex transitions |
| Long 1 | 450 | Large component enter |
| Long 2 | 500 | Full-screen transitions |
| Long 3 | 550 | Complex enter sequences |
| Long 4 | 600 | Complex full sequences |
| Extra-long 1 | 700 | Background processes |
| Extra-long 2 | 800 | Ambient motion |
| Extra-long 3 | 900 | Extended animations |
| Extra-long 4 | 1000 | Maximum duration |
