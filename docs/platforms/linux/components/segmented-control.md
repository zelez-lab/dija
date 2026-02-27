# Linux (GNOME/Adwaita) — Segmented Control (GtkToggleButton Linked Group)

## Overview

GNOME does not have a dedicated segmented control widget like iOS. Instead, it uses
a **linked group of GtkToggleButton** widgets, where buttons share borders and only
outer corners are rounded.

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Group background | transparent (buttons provide own bg) | transparent |
| Button background (unselected) | `#FFFFFF` | `#404040` |
| Button background (selected) | `#FFFFFF` (same, but pressed look) | `#404040` |
| Button background (selected, checked) | `rgba(0,0,0, 0.07)` | `rgba(255,255,255, 0.07)` |
| Border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Inner separator | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Text color (unselected) | `#2E3436` | `#FFFFFF` |
| Text color (selected) | `#2E3436` | `#FFFFFF` |

## Metrics

| Property | Value |
|----------|-------|
| Button min-height | 34px |
| Button horizontal padding | 16px |
| Button vertical padding | 8px |
| Outer corner radius | 6px |
| Inner corner radius | 0px |
| Font | Adwaita Sans Regular, 15px |
| Gap between buttons | 0px (touching) |
| Icon size | 16x16px |

## Corner Radius Pattern

For a group of N linked buttons:

```
[First] [Middle...] [Last]
  6|0     0|0        0|6    (left|right radius)
```

| Position | Border Radius |
|----------|--------------|
| First (leftmost) | top-left: 6px, bottom-left: 6px, right: 0px |
| Middle | all 0px |
| Last (rightmost) | top-right: 6px, bottom-right: 6px, left: 0px |
| Single (only one) | all 6px |

## States

| State | Background | Border |
|-------|-----------|--------|
| Unselected (rest) | button bg | 1px border |
| Unselected (hover) | slightly darker/lighter | 1px border |
| Unselected (active) | pressed bg | inset shadow |
| Selected (checked) | `rgba(0,0,0, 0.07)` / `rgba(255,255,255, 0.07)` | 1px border |
| Selected (hover) | `rgba(0,0,0, 0.12)` / `rgba(255,255,255, 0.12)` | 1px border |
| Disabled | rest, opacity 0.5 | 1px border |

## Selection Behavior

| Property | Value |
|----------|-------|
| Selection mode | Single (radio-like, one active at a time) |
| Allow none selected | Depends on app (usually no) |
| Click behavior | Click selects, deselects others |

Unlike iOS segmented controls, there is **no sliding indicator animation**. Selection
change is immediate with a simple background color transition.

## Keyboard Support

| Key | Action |
|-----|--------|
| Space / Enter | Toggle current button |
| Tab | Move focus to next button in group |
| Arrow Left/Right | Move focus within linked group |

## Vertical Linked Groups

Linked buttons can also be grouped vertically:

```
[ Top    ]  radius: 6 6 0 0
[ Middle ]  radius: 0 0 0 0
[ Bottom ]  radius: 0 0 6 6
```

## Alternative: AdwViewSwitcher

For tab-like navigation (not toggle selection), GNOME uses `AdwViewSwitcher`:

| Property | Value |
|----------|-------|
| Style | Flat buttons with icon + label |
| Selected indicator | Accent-colored bottom line (2px) |
| Layout | Horizontal in header bar, vertical in bottom bar |
| Adaptive | Switches between wide (icon+label) and narrow (icon only) |

The view switcher is preferred over segmented controls for page/view switching.

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Background color | 200ms | ease-in-out |
| Check state change | immediate | — |
