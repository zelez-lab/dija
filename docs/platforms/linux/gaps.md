# Linux (GNOME/Adwaita) — Dija Gaps

What Dija needs to fully replicate GNOME/Adwaita native look.

## Effect System Gaps

| Adwaita visual | EffectKind needed | Status |
|----------------|------------------|--------|
| Solid fill | `Background(Color)` | Have it |
| Rounded corners (circular) | `BorderRadius(f32)` | Have it |
| Padding | `PaddingAll/PaddingEdges` | Have it |
| Border (1px, alpha) | `BorderColor/BorderWidth` | Have it |
| Box shadow (minimal) | `BoxShadow(...)` | Have it in DrawCommand |
| Opacity | `Opacity(f32)` | Have it |
| Font size/weight | `FontSize/FontWeight` | Have it |
| Text color | `TextColor` | Have it |
| Focus ring (outline) | `Outline(width, offset, color)` | **Missing** |
| Backdrop state (unfocused) | `BackdropFade(bg_color)` | **Missing** |
| Inset shadow (pressed buttons) | `InsetBoxShadow(...)` | **Missing** |
| Linked corners (adjacent radii = 0) | Context-aware radius | **Missing** |

## Critical: Client-Side Decorations (CSD)

GNOME windows use CSD — the application owns the title bar (header bar) and window
controls. This is the single biggest architectural difference from other platforms.

**What Dija needs:**

1. **CSD window frame** — Dija must render its own window chrome on Linux (no OS title bar)
2. **Window controls placement** — close/minimize/maximize buttons inside the header bar,
   respecting user settings (`button-layout` from GSettings, e.g., `close:` or `:minimize,maximize,close`)
3. **Dynamic `--window-radius`** — 12px normally, 0px when maximized/tiled
4. **Window shadow rendering** — CSD windows must draw their own shadow around the frame
5. **Drag-to-move** — the header bar acts as a drag handle for window movement
6. **Double-click title** — maximize/restore on double-click in header bar area
7. **Resize handles** — invisible resize grips around the window border

Without CSD, a Dija app on GNOME would have a redundant server-side title bar above
the header bar — a visually broken experience.

## Critical: Adaptive Layouts (libadwaita)

libadwaita provides adaptive layout widgets that respond to window width:

| Widget | Behavior | Dija equivalent needed |
|--------|----------|----------------------|
| `AdwNavigationSplitView` | Shows sidebar+content above breakpoint, collapses to stack below | **Layout breakpoint system** |
| `AdwOverlaySplitView` | Sidebar overlays content on narrow widths | **Overlay layout mode** |
| `AdwBreakpoint` | Arbitrary layout changes at width thresholds | **Breakpoint/media query system** |
| `AdwClamp` | Constrains content to max-width, centered | `max-width` + `margin: auto` (have it) |
| `AdwMultiLayoutView` | Switch between entirely different layouts | **Multi-layout container** |

Adaptive layouts are expected by GNOME users. Apps that do not adapt to narrow windows
look broken on phones (Phosh/GNOME on mobile) and split-screen setups.

**Breakpoints needed:**
- `< 400px` — phone/compact (single column, collapsed nav)
- `400–600px` — narrow (sidebar collapses)
- `> 600px` — wide (sidebar + content side by side)

## Critical: Boxed Lists

GNOME's standard pattern for settings and preferences is the **boxed list** — a card
containing vertically stacked rows with separators.

| Feature | Detail |
|---------|--------|
| Container | `.boxed-list` card, 12px radius, no inner padding |
| Row | `.property` or custom widget, 34px min-height, 12px padding |
| Separator | 1px, full-width, `rgba(0,0,0,0.15)` |
| Row types | Switch row, action row, combo row, entry row, spinner row |
| Suffix/prefix | Rows can have prefix (icon) and suffix (switch, arrow) |

Dija needs a composable row system for boxed lists.

## Header Bar Features

| Feature | Detail | Status |
|---------|--------|--------|
| CSD integration | Window controls inside header bar | **Missing** |
| Flat/raised style | `.flat` by default, `.raised` for emphasis | **Missing** (style class system) |
| Title widget | Centered title (text or custom widget) | **Missing** |
| Subtitle | Optional smaller text below title | **Missing** |
| Search mode | Header bar transforms to search entry | **Missing** |
| Toolbar style | `.toolbar` class for consistent toolbar appearance | **Missing** |
| View switcher in header | `AdwViewSwitcher` as title widget | **Missing** |

## Missing Components

| Component | GTK/libadwaita | Priority |
|-----------|---------------|----------|
| View switcher | `AdwViewSwitcher` / `AdwViewSwitcherBar` | High |
| Preferences page | `AdwPreferencesPage` / `AdwPreferencesGroup` | High |
| Status page | `AdwStatusPage` (empty states, errors) | Medium |
| About dialog | `AdwAboutDialog` (standardized) | Medium |
| Banner | `AdwBanner` (in-app notification bar) | Medium |
| Carousel | `AdwCarousel` (swipeable pages) | Low |
| Flap | `AdwFlap` (collapsible side panel) | Low |
| Tab view/bar | `AdwTabView` / `AdwTabBar` | Medium |
| Spin row | `AdwSpinRow` (number input in boxed list) | Medium |

## Theming Integration

| Need | Detail |
|------|--------|
| CSS variable mapping | Map Dija theme tokens to libadwaita variable names |
| Dark mode toggle | Respond to `prefers-color-scheme` (via `AdwStyleManager`) |
| Accent color | Read system accent color preference (GNOME 47+) |
| High contrast | Support `ADW_COLOR_SCHEME_PREFER_LIGHT/DARK` + high contrast mode |
| Font scaling | Respect GNOME `text-scaling-factor` (0.5x to 3.0x) |
| Animation preference | Respect `gtk-enable-animations` setting |

## Style Class System

libadwaita relies heavily on CSS-like style classes for variant selection:

| Pattern | Examples |
|---------|----------|
| Button variants | `.flat`, `.raised`, `.suggested-action`, `.destructive-action`, `.circular`, `.pill`, `.osd` |
| Typography | `.title-1`, `.title-2`, `.heading`, `.body`, `.caption`, `.monospace`, `.numeric` |
| List styles | `.boxed-list`, `.navigation-sidebar`, `.rich-list` |
| Toolbar | `.toolbar`, `.toolbar-flat` |
| Cards | `.card`, `.card.activatable` |
| View | `.view`, `.background` |
| Status | `.error`, `.warning`, `.success` |
| Opacity | `.dim-label` |

Dija needs a mechanism to apply named style variants to components — either through
the skin system or a dedicated style class API.

## Platform Detection

On Linux, Dija should detect:

1. **Desktop environment** — GNOME vs KDE vs other (XDG_CURRENT_DESKTOP)
2. **GTK version** — GTK4 + libadwaita present?
3. **Color scheme** — `org.gnome.desktop.interface color-scheme` (GSettings)
4. **Accent color** — `org.gnome.desktop.interface accent-color` (GNOME 47+)
5. **Font settings** — `org.gnome.desktop.interface font-name`
6. **Scaling factor** — `org.gnome.desktop.interface text-scaling-factor`
7. **Animation preference** — `org.gnome.desktop.interface enable-animations`
8. **Button layout** — `org.gnome.desktop.wm.preferences button-layout`

On non-GNOME Linux desktops (KDE, XFCE, etc.), Dija should fall back to a generic
Adwaita-like theme rather than trying to match KDE Breeze or other toolkits.
