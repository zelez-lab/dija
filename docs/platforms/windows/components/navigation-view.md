# Windows — NavigationView

Source: WinUI 3 NavigationView control

NavigationView is the primary app navigation pattern in Windows 11: a collapsible sidebar (hamburger menu) with icons and labels, plus an optional header and content area.

## Display Modes

| Mode | Pane State | Trigger |
|------|-----------|---------|
| Expanded (Left) | Full sidebar, icon + label | Window width >= 1008px |
| Compact (LeftCompact) | Icons only, labels hidden | Window width 641-1007px |
| Minimal (LeftMinimal) | Hamburger button only, overlay pane | Window width <= 640px |
| Top | Horizontal nav bar across top | Explicit opt-in |

Breakpoints are configurable via `CompactModeThresholdWidth` (default 641px) and `ExpandedModeThresholdWidth` (default 1008px).

## Pane Metrics

| Property | Value |
|----------|-------|
| Expanded pane width | 320px (default, configurable via OpenPaneLength) |
| Compact pane width | 48px (default, configurable via CompactPaneLength) |
| Minimal: hamburger button area | 48x48px |
| Pane background | In-App Acrylic (overlay mode) or transparent (inline mode, inherits Mica) |
| Pane border (overlay mode) | 1px SurfaceStrokeColorFlyout on the right edge |

## Navigation Item

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px horizontal |
| Corner radius | 4px |
| Icon size | 16x16px |
| Icon-to-text gap | 12px |
| Font | 14px, Regular |
| Indent (sub-items) | +28px per level |

### Item States

| State | Background | Text | Indicator |
|-------|-----------|------|-----------|
| Rest | Transparent | TextFillColorPrimary | None |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary | None |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary | None |
| Selected | SubtleFillColorSecondary | TextFillColorPrimary | 3px accent pill (left) |
| Selected + Hover | SubtleFillColorTertiary | TextFillColorPrimary | 3px accent pill |
| Disabled | Transparent | TextFillColorDisabled | None |

### Selection Indicator (Pill)

Same as ListView: a **3px wide, 16px tall accent pill** on the left edge of the selected item.

| Property | Value |
|----------|-------|
| Width | 3px |
| Height | 16px |
| Corner radius | 1.5px |
| Color | AccentFillColorDefault |
| Animation | Slides vertically between items (200ms, Decelerate) |

## Header

| Property | Value |
|----------|-------|
| Height | 52px |
| Font | 28px Title, SemiBold |
| Padding | 24px horizontal (expanded), 12px (compact) |
| Vertical alignment | Center |

## Hamburger Button

| Property | Value |
|----------|-------|
| Size | 48x48px (hit area), icon 16x16px |
| Icon | `&#xE700;` (hamburger glyph) |
| Background | Subtle (transparent → hover fill) |
| Position | Top-left, vertically aligned with first item |

## Back Button

| Property | Value |
|----------|-------|
| Size | 40x36px |
| Icon | `&#xE72B;` (back arrow), 16x16px |
| Position | Above hamburger button |
| Background | Subtle style |

## Footer Items

Items placed at the bottom of the pane (e.g., Settings).

| Property | Value |
|----------|-------|
| Separator | 1px DividerStrokeColorDefault above footer section |
| Item metrics | Same as regular navigation items |
| Settings icon | `&#xE713;` (gear), always present if `IsSettingsVisible` |

## Pane Content Layout

```
┌──────────────────────┐
│ [←] Back button      │  ← optional
│ [☰] Hamburger button │
│                      │
│ Search (AutoSuggest) │  ← optional
│ ──────────────────── │
│ [🏠] Home            │  ← selected (accent pill)
│ [📁] Files           │
│ [⚙] Settings        │
│ ...                  │
│ ──────────────────── │
│ [⚙] Settings        │  ← footer
└──────────────────────┘
```

## Top Navigation Mode

When `PaneDisplayMode="Top"`:

| Property | Value |
|----------|-------|
| Bar height | 48px |
| Item padding | 12px horizontal |
| Selection indicator | 3px wide accent pill at bottom (horizontal, same 16px length) |
| Overflow | Items that don't fit go into a "More" dropdown |
| Background | Transparent (inherits parent background) |

## Content Area

| Property | Value |
|----------|-------|
| Margin (minimal mode) | 12px |
| Margin (expanded mode) | 24px |
| Transition | Slide + fade (300ms, Decelerate) on page navigation |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Pane expand (compact → expanded) | 300ms | Decelerate |
| Pane collapse (expanded → compact) | 200ms | Accelerate |
| Selection pill slide (between items) | 200ms | Decelerate |
| Page content enter (slide + fade) | 300ms | Decelerate |
| Page content exit | 150ms | Accelerate |
| Overlay pane open (minimal mode) | 200ms | Decelerate |
| Overlay pane close | 150ms | Accelerate |
