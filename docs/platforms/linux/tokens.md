# Linux (GNOME/Adwaita) — Design Tokens

Source: GNOME Human Interface Guidelines, libadwaita 1.x stylesheet (GTK4), Adwaita Sans

## Corner Radii

Adwaita uses **standard CSS `border-radius`** (circular arcs), not superellipses.

| Context | Value | CSS Variable |
|---------|-------|--------------|
| Buttons (default) | 6px | — |
| Text entries, search entries | 6px | — |
| Popovers | 12px | — |
| Cards (.card) | 12px | — |
| Dialogs (AdwAlertDialog) | 12px | — |
| Windows (CSD, normal) | 12px | `--window-radius` |
| Windows (maximized/tiled) | 0px | `--window-radius` |
| Toggle buttons (linked group) | 6px (outer only, inner 0) | — |
| Circular buttons (.circular) | 9999px (fully round) | — |
| Pill buttons (.pill) | 9999px (fully round) | — |
| Check/radio indicators | 4px (check), 50% (radio) | — |
| Tab bar tabs | 6px | — |
| OSD toolbar | 12px | — |

The `--window-radius` CSS variable dynamically changes from 12px to 0px when the
window is maximized, tiled to a screen edge, or fullscreen.

## Shadows

Adwaita follows a **flat design** philosophy. Shadows are minimal and used sparingly.

| Context | Offset (x, y) | Blur | Spread | Color |
|---------|---------------|------|--------|-------|
| Buttons (raised, default) | (0, 1) | 2px | 0 | black @ 0.07 |
| Buttons (raised, hover) | (0, 1) | 3px | 0 | black @ 0.09 |
| Buttons (raised, active) | inset (0, 1) | 2px | 0 | black @ 0.07 |
| Cards (.card) | (0, 1) | 3px | 0 | black @ 0.06 |
| Popovers | (0, 4) | 12px | 0 | black @ 0.15 |
| Dialogs | (0, 12) | 36px | 0 | black @ 0.25 |
| OSD elements | (0, 2) | 8px | 0 | black @ 0.20 |
| Window (CSD) | (0, 3) | 12px | 1px | black @ 0.20 |
| Window (focused CSD) | (0, 6) | 18px | 2px | black @ 0.25 |
| Switch thumb | (0, 1) | 2px | 0 | black @ 0.10 |

Flat buttons (`.flat`) have **no shadow at all** — they are completely flush with the
background until hovered.

## Typography

### Font Families

| Family | Usage | Introduced |
|--------|-------|------------|
| Adwaita Sans (custom Inter) | Default UI font (GNOME 48+) | 2025 |
| Cantarell | Legacy UI font (GNOME 3–47) | 2011 |
| Adwaita Mono (custom Source Code Pro) | Monospace (GNOME 48+) | 2025 |
| Source Code Pro | Legacy monospace | — |
| System sans-serif fallback | `sans-serif` stack | — |

Adwaita Sans is a customized variant of Inter by Rasmus Andersson. It replaced Cantarell
starting with GNOME 48. Distributions may still ship Cantarell as a fallback.

### Font Weights

| Weight Name | CSS Weight | Usage |
|-------------|-----------|-------|
| Light | 300 | Rarely used |
| Regular | 400 | Body text, most UI |
| Medium | 500 | Not commonly used |
| Semibold | 600 | Not commonly used |
| Bold | 700 | Headings, emphasis |

### Type Scale (libadwaita style classes)

Default system font size: 11pt (~15px at 96 DPI).

| Style Class | Font Size | Weight | Line Height | Usage |
|-------------|-----------|--------|-------------|-------|
| `.display` | 36px | 300 (Light) | 44px | Large splash screens, onboarding |
| `.title-1` | 24px | 700 (Bold) | 32px | Page/view titles |
| `.title-2` | 20px | 700 (Bold) | 28px | Section titles |
| `.title-3` | 18px | 700 (Bold) | 24px | Sub-section titles |
| `.title-4` | 16px | 700 (Bold) | 22px | Card/group titles |
| `.heading` | 15px (default) | 700 (Bold) | 20px | Window titles, row headers |
| `.body` | 15px (default) | 400 (Regular) | 22px | Body text, descriptions |
| `.caption-heading` | 13px | 700 (Bold) | 18px | Small heading, sub-labels |
| `.caption` | 13px | 400 (Regular) | 18px | Secondary text, timestamps |
| `.monospace` | 15px (default) | 400 (Regular) | 20px | Code, terminal |
| `.numeric` | 15px (default) | tabular-nums | 20px | Numeric data |

The base font size of ~15px comes from the GTK default of 11pt at 96 DPI (11 * 96/72 = 14.67, rounded to 15).

### Common Component Typography

| Usage | Size | Weight |
|-------|------|--------|
| Header bar title | 15px | Bold |
| Header bar subtitle | 13px | Regular |
| Button label (default) | 15px | Regular |
| Button label (.suggested-action) | 15px | Bold |
| Menu item | 15px | Regular |
| Dialog title | 18px | Bold |
| Dialog body | 15px | Regular |
| Tab label | 13px | Regular |
| Tooltip text | 13px | Regular |
| Badge text | 11px | Bold |
| Entry placeholder | 15px | Regular, alpha 0.5 |

## Spacing

**6px base grid** with common multiples.

| Token | Value |
|-------|-------|
| xxs | 2px |
| xs | 4px |
| sm | 6px |
| md | 8px |
| lg | 12px |
| xl | 16px |
| 2xl | 18px |
| 3xl | 24px |
| 4xl | 32px |
| 5xl | 48px |

### Common Spacing Values

| Context | Value |
|---------|-------|
| Header bar padding (horizontal) | 6px |
| Header bar widget spacing | 6px |
| Header bar minimum height | 47px |
| Toolbar minimum height | 46px |
| Button padding (horizontal) | 16px |
| Button padding (vertical) | 8px |
| Card padding (content) | 12px |
| Card margin (in boxed lists) | 0px (flush) |
| Boxed list row padding | 8px 12px |
| Boxed list row min-height | 34px |
| Dialog content margin | 24px |
| Popover padding | 6px |
| Sidebar width (default) | 25% (min 180px, max 280px) |
| Content margins (default) | 12–18px |
| List separator inset | 0px (full-width) |
| Linked button group gap | 0px (buttons touch) |

## Hit Target Sizes

| Element | Minimum Size |
|---------|-------------|
| Buttons (default) | 34px height (with padding) |
| Header bar buttons | 34px height |
| Circular/icon buttons | 34x34px |
| Switch | 42x26px |
| Check/radio box | 20x20px (visual), 34x34px (hit area) |
| Slider thumb | 20px diameter (34px hit area) |
| List rows | 34px min-height |
| Menu items | 32px min-height |

GNOME follows Fitts's law: interactive elements should be comfortably clickable.
No explicit 44px mandate like iOS, but ~34px minimum is standard.

## Opacity Levels

| Usage | Alpha |
|-------|-------|
| Disabled controls | 0.5 (via `--disabled-opacity`) |
| Dim/secondary text | 0.55 (via `--dim-opacity`) |
| Borders | 0.15 (via `--border-opacity`) |
| Placeholder text | 0.5 |
| Insensitive (disabled) text | 0.5 |
| Flat button (rest state) | 0.0 background |
| Flat button (hover) | ~0.07 background |
| Flat button (active) | ~0.12 background |

## Animations

### Standard Durations

| Animation | Duration | Easing |
|-----------|----------|--------|
| Button hover/press | 200ms | ease-in-out |
| Switch toggle | 250ms | ease-in-out |
| Sidebar collapse/expand | 400ms | ease-in-out-cubic |
| Dialog appear | 250ms | ease-out-cubic |
| Dialog dismiss | 200ms | ease-in-cubic |
| Toast slide in | 350ms | ease-out-cubic |
| Toast slide out | 300ms | ease-in-cubic |
| Popover appear | 200ms | ease-out-cubic |
| Popover dismiss | 150ms | ease-in-cubic |
| Page transition (push) | 400ms | ease-in-out-cubic |
| Spinner rotation | 1050ms per cycle | linear |
| Progress pulse | 750ms per cycle | ease-in-out |
| Tab switch | 250ms | ease-in-out |
| Revealer expand/collapse | 250ms | ease-in-out |

### Easing Curves (AdwEasing)

| Name | Bezier | Usage |
|------|--------|-------|
| `EASE_IN_CUBIC` | (0.32, 0, 0.67, 0) | Elements leaving |
| `EASE_OUT_CUBIC` | (0.33, 1, 0.68, 1) | Elements appearing |
| `EASE_IN_OUT_CUBIC` | (0.65, 0, 0.35, 1) | Most transitions |
| `EASE_IN_QUAD` | (0.11, 0, 0.5, 0) | Subtle acceleration |
| `EASE_OUT_QUAD` | (0.5, 1, 0.89, 1) | Subtle deceleration |
| `LINEAR` | (0, 0, 1, 1) | Spinners, progress |

libadwaita's `AdwTimedAnimation` API takes duration (ms) + `AdwEasing` enum.
No spring physics in the animation API — all transitions are cubic bezier.

## Border Widths

| Context | Value |
|---------|-------|
| Button border | 1px (subtle, uses border-opacity) |
| Card border | 1px |
| Entry border | 1px |
| Separator / divider | 1px |
| Header bar bottom border | 1px |
| Linked group inner borders | 1px |
| Switch outline | 2px |
| Focus ring | 2px, offset 2px |

## Focus Indication

| Property | Value |
|----------|-------|
| Ring color | `--accent-color` (default blue `#3584e4`) |
| Ring width | 2px |
| Ring offset | 2px |
| Ring radius | element radius + 2px |
| Style | outline, not box-shadow |
