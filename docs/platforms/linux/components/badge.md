# Linux (GNOME/Adwaita) — Badge (Notification Styling)

## Overview

GNOME does not have a dedicated badge widget in GTK4 or libadwaita. Notification
badges are implemented through custom styling — typically a small colored dot or
count label overlaid on an icon or sidebar row.

## Dot Badge (Unread Indicator)

Used in sidebars, tab bars, and app indicators to signal new/unread content.

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Border | none | 2px (parent bg color, for contrast) |
| Shape | Circle | Circle |

### Metrics

| Property | Value |
|----------|-------|
| Diameter | 8px |
| Border (when overlaid) | 2px, matches parent background |
| Total visual size | 12px (8px + 2px border each side) |
| Position | Top-right of parent icon/element |
| Offset from parent | -2px right, -2px top |

## Count Badge

Displays a numeric count (unread messages, notifications).

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `--accent-bg-color` (`#3584E4`) | `--accent-bg-color` |
| Text color | `--accent-fg-color` (`#FFFFFF`) | `#FFFFFF` |
| Border | none | 2px parent-bg-colored ring |
| Shape | Pill (capsule) | Pill |

### Metrics

| Property | Value |
|----------|-------|
| Min-width | 18px |
| Height | 18px |
| Corner radius | 9px (fully rounded) |
| Horizontal padding | 4px |
| Font | Adwaita Sans Bold, 11px |
| Text alignment | Center |
| Max digits shown | 2 ("99+") |

### Count Formatting

| Count | Display |
|-------|---------|
| 0 | Hidden (no badge) |
| 1-99 | Numeric ("1", "42") |
| 100+ | "99+" |

## Sidebar Badge (Inline Count)

Used in navigation sidebars to show item counts (e.g., mailbox unread count).

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `rgba(0,0,0, 0.08)` | `rgba(255,255,255, 0.08)` |
| Text color | dim-label color | dim-label color |
| Corner radius | 9px (pill) | 9px |

### Metrics

| Property | Value |
|----------|-------|
| Height | 18px |
| Min-width | 18px |
| Padding | 2px 6px |
| Font | Adwaita Sans Regular, 13px (.caption) |
| Position | Right-aligned in sidebar row (suffix) |
| Margin from row edge | 8px |

This variant uses muted colors to avoid competing with the sidebar selection highlight.

## Badge Position (Overlay)

When used as an overlay on icons:

```
+--------+
| Icon  *|  (* = badge, top-right corner)
|        |
+--------+
```

| Property | Value |
|----------|-------|
| Anchor | Top-right corner of parent |
| Offset X | -25% of badge width (overlaps parent) |
| Offset Y | -25% of badge height (overlaps parent) |
| Z-index | Above parent element |

## States

| State | Dot Badge | Count Badge |
|-------|-----------|-------------|
| Visible | accent circle | accent pill with number |
| Empty (count = 0) | Hidden | Hidden |
| Disabled parent | opacity 0.5 | opacity 0.5 |
| Selected parent row | May change to white/inverse | Stays accent |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Appear (scale) | 200ms | ease-out-cubic |
| Disappear (scale) | 150ms | ease-in-cubic |
| Count change | none (immediate update) | — |

### Appear Animation

```
Start:  scale(0.0), opacity(0)
End:    scale(1.0), opacity(1.0)
```

## Comparison to iOS

| Property | GNOME Badge | iOS Badge |
|----------|------------|-----------|
| Shape | Circle (dot) or pill (count) | Circle or pill |
| Default color | Accent (blue) | systemRed |
| Font size | 11px | 13pt |
| Border ring | 2px parent-bg | 2px white |
| Position | Top-right overlay | Top-right overlay |
| Standard widget | None (custom) | UITabBarItem badge |

## Dija Skin Mapping

```
skin! {
    BadgeSkin {
        field main
        field label

        platform linux {
            light {
                main: {
                    min_width: 18, height: 18,
                    padding: 2 4,
                    border_radius: 9,
                    background: #3584E4,
                }
                label: {
                    font_size: 11,
                    font_weight: bold,
                    color: #FFFFFF,
                }
            }
        }
    }
}
```
