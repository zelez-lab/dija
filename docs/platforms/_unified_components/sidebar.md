# Sidebar

A persistent side panel for app-level navigation, typically showing a list of sections or categories.

| Platform | Native Component | Status |
|---|---|---|
| iOS | — | No native equivalent |
| macOS | NSOutlineView (sidebar style) | Documented |
| Android | NavigationRail | Documented |
| Windows | NavigationView (pane) | Documented |
| Linux | AdwNavigationSplitView | Documented |

## iOS

No native equivalent. Dija renders as a collapsible side panel following iOS styling conventions.

## macOS

Reference: NSSplitViewItem (sidebar behavior), NSOutlineView (source list style), NSVisualEffectView (sidebar material), Apple HIG (macOS 14+).

### Overview

The macOS sidebar is a standard navigation pattern for organizing content hierarchically. It is typically implemented as an `NSOutlineView` with `.sourceList` style inside an `NSSplitViewItem` with `.sidebar` behavior. The sidebar gets automatic vibrancy, selection highlighting, and standard sizing.

### Layout

#### Width

| Property                  | Value (pt) |
|---------------------------|------------|
| Default width              | 240        |
| Minimum width              | 180        |
| Maximum width              | 320        |
| Recommended range          | 200-280    |
| Collapse threshold         | 100        |

#### Height

The sidebar extends the full height of the window. In "full-height sidebar" mode (macOS 11+), the sidebar extends behind the toolbar into the title bar area.

| Configuration            | Sidebar Top Edge                          |
|--------------------------|-------------------------------------------|
| Standard                 | Below toolbar separator                   |
| Full-height              | Top of window (behind titlebar/toolbar)    |

Full-height sidebar requires:
```swift
splitViewItem.allowsFullHeightLayout = true
window.titlebarSeparatorStyle = .none
```

### Metrics

#### Row Metrics

| Property                  | Value (pt) |
|---------------------------|------------|
| Row height                 | 24         |
| Row horizontal padding     | 10         |
| Row vertical padding       | 2          |
| Selection corner radius    | 6          |
| Selection inset (H)        | 10         |
| Selection inset (V)        | 0          |
| Indentation per level      | 16         |
| Icon size                  | 16         |
| Icon to text gap           | 6          |

#### Group Header Metrics

| Property                  | Value (pt) |
|---------------------------|------------|
| Group header height        | 28         |
| Group header top padding   | 16 (first), 8 (subsequent) |
| Group header font size     | 11         |
| Group header font weight   | Bold       |
| Group header letter spacing | +0.5 pt   |
| Group header text transform| Uppercase  |

#### Badge (Count Indicator)

Sidebar rows often show a count badge on the right side:

| Property                  | Value             |
|---------------------------|-------------------|
| Badge height               | 18 pt             |
| Badge min width            | 18 pt             |
| Badge horizontal padding   | 6 pt              |
| Badge corner radius        | 9 pt (capsule)    |
| Badge font size            | 10 pt             |
| Badge font weight          | Medium            |
| Badge right margin         | 6 pt              |

### Colors

#### Background

| State                    | Light Mode                   | Dark Mode                    |
|--------------------------|------------------------------|------------------------------|
| Background               | sidebar material vibrancy    | sidebar material vibrancy    |
| Fallback (no vibrancy)   | `#F6F6F6`                    | `#2D2D2D`                    |

#### Selection

| State                    | Light Mode                         | Dark Mode                          |
|--------------------------|------------------------------------|------------------------------------|
| Selected (focused)       | controlAccentColor with vibrancy   | controlAccentColor with vibrancy   |
| Selected (unfocused)     | `rgba(0,0,0,0.06)`                | `rgba(255,255,255,0.08)`           |
| Hover                    | `rgba(0,0,0,0.04)`                | `rgba(255,255,255,0.06)`           |
| Pressed                  | `rgba(0,0,0,0.08)`                | `rgba(255,255,255,0.10)`           |

The focused selection uses the accent color composited with vibrancy for a rich, translucent tint effect.

#### Text

| Element                  | Light Mode                 | Dark Mode                  |
|--------------------------|----------------------------|----------------------------|
| Item text                | labelColor                 | labelColor                 |
| Item selected text       | `#FFFFFF`                  | `#FFFFFF`                  |
| Group header text        | secondaryLabelColor        | secondaryLabelColor        |
| Badge text (normal)      | secondaryLabelColor        | secondaryLabelColor        |
| Badge text (selected)    | `#FFFFFF`                  | `#FFFFFF`                  |
| Badge background (normal)| `rgba(0,0,0,0.08)`        | `rgba(255,255,255,0.10)`   |
| Badge background (selected)| `rgba(255,255,255,0.25)` | `rgba(255,255,255,0.25)`   |

#### Icons

| State                    | Treatment                                    |
|--------------------------|----------------------------------------------|
| Normal                   | Template image, tinted with labelColor        |
| Selected (focused)       | Template image, tinted white                  |
| Selected (unfocused)     | Template image, tinted with labelColor        |
| Disabled                 | Template image at 40% opacity                 |

#### Separator

A thin separator line appears between the sidebar and the content area:

| Property                  | Value                            |
|---------------------------|----------------------------------|
| Width                      | 0.5 pt (1 px on Retina)        |
| Color (light)              | `rgba(0,0,0,0.12)`             |
| Color (dark)               | `rgba(255,255,255,0.12)`       |

### Disclosure (Expandable Groups)

| Element                  | Value                            |
|--------------------------|----------------------------------|
| Disclosure triangle size | 10x10 pt                         |
| Disclosure color         | tertiaryLabelColor               |
| Disclosure animation     | 150 ms rotate, Ease In Out       |
| Collapsed state          | Triangle points right            |
| Expanded state           | Triangle points down             |

### Interaction States

| Interaction              | Behavior                                     |
|--------------------------|----------------------------------------------|
| Click                    | Select item, navigate                        |
| Double-click             | Open in new window/tab (context-dependent)   |
| Right-click              | Context menu                                 |
| Drag                     | Reorder items (if enabled)                   |
| Drop                     | Rearrange or move content                    |
| Collapse sidebar         | Click toggle button or drag divider past min |

### Sidebar Toggle

The standard sidebar toggle button in the toolbar:
- SF Symbol: `sidebar.leading`
- Size: 16 pt icon, toolbar-style button
- Keyboard shortcut: Cmd+Shift+L (or Cmd+Control+S)

### Animation

| Transition                    | Duration (ms) | Curve          |
|-------------------------------|---------------|----------------|
| Sidebar collapse              | 250           | Ease In Out    |
| Sidebar expand                | 250           | Ease In Out    |
| Selection change              | 100           | Ease Out       |
| Disclosure expand/collapse    | 150           | Ease In Out    |
| Row insert/delete             | 250           | Ease In Out    |
| Badge count update            | 200           | Ease In Out    |
| Hover highlight               | 80            | Ease Out       |

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Up Arrow        | Move selection up one row                  |
| Down Arrow      | Move selection down one row                |
| Right Arrow     | Expand group / enter subgroup              |
| Left Arrow      | Collapse group / go to parent              |
| Return          | Open/navigate to selected item             |
| Tab             | Move focus to content area                 |
| Space           | Toggle selection (if applicable)           |
| Cmd+Shift+L     | Toggle sidebar visibility                  |

### Dija Skin Mapping

```
comp! Sidebar {
    // macOS skin should provide:
    // Background: sidebar vibrancy material
    // Rows: 24 pt height, 10 pt horizontal padding
    // Selection: accent-tinted vibrancy rect, 6 pt radius
    // Icons: 16 pt template images
    // Group headers: 11 pt bold uppercase
    // Separator: 0.5 pt line at trailing edge
    //
    // Full-height mode extends behind toolbar
    // Width: 240 pt default, 180-320 pt range
}
```

## Android

Source: m3.material.io/components/navigation-rail/specs

Vertical side navigation for tablets and larger screens. Replaces bottom
navigation bar when screen width >= 600dp (medium window size class).

### Metrics

| Property | Value |
|----------|-------|
| Width | 80dp |
| Elevation | Level 0 (0dp) |
| Surface | surface |
| Icon size | 24dp |
| Active indicator width | 56dp |
| Active indicator height | 32dp |
| Active indicator corner radius | 16dp (full pill) |
| Label font | Label Medium (Roboto Medium 500, 12sp) |
| Icon-to-label gap | 4dp |
| Item spacing (between items) | 0dp (vertically centered in 56dp slot) |
| Item height | 56dp (icon + label slot) |
| Top padding | 44dp (or FAB placement) |
| Alignment | Center (default), top |

### FAB Placement

The rail can host a FAB at the top, above the navigation items:

| Property | Value |
|----------|-------|
| FAB position | Top of rail, centered horizontally |
| FAB to first item gap | 12dp |
| FAB variant | Small (40dp) or standard (56dp) |

### Active Indicator

| Property | Value |
|----------|-------|
| Width | 56dp |
| Height | 32dp |
| Corner radius | 16dp (full pill) |
| Color | secondaryContainer |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#FEF7FF` (surface) | `#141218` |
| Active icon | `#1D192B` (onSecondaryContainer) | `#E8DEF8` |
| Active indicator | `#E8DEF8` (secondaryContainer) | `#4A4458` |
| Active label | `#1D1B20` (onSurface) | `#E6E0E9` |
| Inactive icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Inactive label | `#49454F` (onSurfaceVariant) | `#CAC4D0` |

### States

| State | Effect |
|-------|--------|
| Hovered | State layer 8% on indicator area |
| Focused | State layer 10% on indicator area |
| Pressed | State layer 10% + ripple on indicator area |

State layer color: onSurface for inactive, onSecondaryContainer for active.

### Configuration

| Mode | Labels | Description |
|------|--------|------------|
| Labels visible | All items | Always show icon + label |
| Labels selected | Active only | Only selected item shows label |
| Labels hidden | None | Icon-only rail |

### Menu Anchor

Navigation rail can show a menu icon at the top (above FAB) to
toggle an expanded navigation drawer. This is used in responsive
layouts:

- Compact (< 600dp): bottom navigation bar
- Medium (600-839dp): navigation rail
- Expanded (>= 840dp): navigation drawer

### Layout

```
+--------+
|  Menu  |  (optional hamburger icon)
| 44dp   |
|  FAB   |  (optional)
| 12dp   |
| [Icon] |
| Label  |
|        |
| [Icon] |
| Label  |
|        |
| [Icon] |
| Label  |
|        |
| [Icon] |
| Label  |
+--------+
   80dp
```

### Badge Position

Same as navigation bar: badges on top-right of icon.

## Windows

Source: WinUI 3 NavigationView control (pane display modes)

NavigationView in its default pane modes provides a collapsible sidebar (hamburger menu) with icons and labels, plus an optional header and content area.

### Display Modes

| Mode | Pane State | Trigger |
|------|-----------|---------|
| Expanded (Left) | Full sidebar, icon + label | Window width >= 1008px |
| Compact (LeftCompact) | Icons only, labels hidden | Window width 641-1007px |
| Minimal (LeftMinimal) | Hamburger button only, overlay pane | Window width <= 640px |

Breakpoints are configurable via `CompactModeThresholdWidth` (default 641px) and `ExpandedModeThresholdWidth` (default 1008px).

### Pane Metrics

| Property | Value |
|----------|-------|
| Expanded pane width | 320px (default, configurable via OpenPaneLength) |
| Compact pane width | 48px (default, configurable via CompactPaneLength) |
| Minimal: hamburger button area | 48x48px |
| Pane background | In-App Acrylic (overlay mode) or transparent (inline mode, inherits Mica) |
| Pane border (overlay mode) | 1px SurfaceStrokeColorFlyout on the right edge |

### Navigation Item

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

### Header

| Property | Value |
|----------|-------|
| Height | 52px |
| Font | 28px Title, SemiBold |
| Padding | 24px horizontal (expanded), 12px (compact) |
| Vertical alignment | Center |

### Hamburger Button

| Property | Value |
|----------|-------|
| Size | 48x48px (hit area), icon 16x16px |
| Icon | `&#xE700;` (hamburger glyph) |
| Background | Subtle (transparent -> hover fill) |
| Position | Top-left, vertically aligned with first item |

### Back Button

| Property | Value |
|----------|-------|
| Size | 40x36px |
| Icon | `&#xE72B;` (back arrow), 16x16px |
| Position | Above hamburger button |
| Background | Subtle style |

### Footer Items

Items placed at the bottom of the pane (e.g., Settings).

| Property | Value |
|----------|-------|
| Separator | 1px DividerStrokeColorDefault above footer section |
| Item metrics | Same as regular navigation items |
| Settings icon | `&#xE713;` (gear), always present if `IsSettingsVisible` |

### Pane Content Layout

```
+----------------------+
| [<-] Back button     |  <- optional
| [=] Hamburger button |
|                      |
| Search (AutoSuggest) |  <- optional
| -------------------- |
| [H] Home             |  <- selected (accent pill)
| [F] Files            |
| [G] Settings         |
| ...                  |
| -------------------- |
| [G] Settings         |  <- footer
+----------------------+
```

### Content Area

| Property | Value |
|----------|-------|
| Margin (minimal mode) | 12px |
| Margin (expanded mode) | 24px |
| Transition | Slide + fade (300ms, Decelerate) on page navigation |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Pane expand (compact -> expanded) | 300ms | Decelerate |
| Pane collapse (expanded -> compact) | 200ms | Accelerate |
| Selection pill slide (between items) | 200ms | Decelerate |
| Page content enter (slide + fade) | 300ms | Decelerate |
| Page content exit | 150ms | Accelerate |
| Overlay pane open (minimal mode) | 200ms | Decelerate |
| Overlay pane close | 150ms | Accelerate |

## Linux

Source: libadwaita (GTK4)

### Overview

libadwaita provides multiple sidebar/split-view patterns:

| Widget | Behavior |
|--------|----------|
| `AdwNavigationSplitView` | Sidebar + content, collapses to navigation stack |
| `AdwOverlaySplitView` | Sidebar overlays content on narrow windows |
| `AdwNavigationView` | Stack-based navigation (push/pop pages) |

### AdwNavigationSplitView

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Sidebar background | `#EBEBEB` (sidebar_bg_color) | `#303030` |
| Sidebar backdrop | `#F2F2F2` (sidebar_backdrop_color) | `#2A2A2A` |
| Content background | `#FAFAFA` (window_bg_color) | `#242424` |
| Separator (between panes) | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |

#### Metrics

| Property | Value |
|----------|-------|
| Sidebar width (fraction) | 25% of total window width |
| Sidebar min-width | 180px |
| Sidebar max-width | 280px |
| Width unit | `sp` (scale-independent pixels) |
| Sidebar padding | 0px (content fills edge-to-edge) |
| Content padding | 0px (up to content widgets) |

#### Adaptive Behavior

| Window Width | Layout |
|-------------|--------|
| >= sidebar min + content min (~460px) | Side-by-side (split view) |
| < breakpoint | Collapsed (navigation stack) |

When collapsed:
- Sidebar becomes a full-width page
- Selecting an item pushes the content page
- Back button appears in content header bar
- Transition: slide from right (400ms, ease-in-out-cubic)

### Sidebar Content

The sidebar typically contains a `GtkListBox` with `.navigation-sidebar` style:

#### Navigation Sidebar Row

| Property | Light | Dark |
|----------|-------|------|
| Background (rest) | transparent | transparent |
| Background (hover) | `rgba(0,0,0, 0.04)` | `rgba(255,255,255, 0.04)` |
| Background (selected) | `--accent-bg-color` @ 0.12 | `--accent-bg-color` @ 0.12 |
| Background (selected + hover) | `--accent-bg-color` @ 0.18 | `--accent-bg-color` @ 0.18 |
| Text color (rest) | window_fg_color | window_fg_color |
| Text color (selected) | `--accent-color` | `--accent-color` |
| Corner radius | 6px | 6px |
| Margin (horizontal) | 6px | 6px |
| Padding | 8px 12px | 8px 12px |
| Min-height | 34px | 34px |

#### Row Layout

```
+---+------+---+------------------------------------+---+-----+
| M | Icon | G |           Title                    | G | Badge|
+---+------+---+------------------------------------+---+-----+
 ^    16px  8px              15px                     8px
 6px margin
```

| Element | Size | Notes |
|---------|------|-------|
| Icon (prefix) | 16x16px | Optional |
| Icon-to-title gap | 8px | — |
| Title font | 15px, Regular | — |
| Badge/count (suffix) | `.caption` size, accent bg | Optional |

### AdwOverlaySplitView

#### Differences from NavigationSplitView

| Property | NavigationSplitView | OverlaySplitView |
|----------|-------------------|-----------------|
| Collapsed mode | Stack navigation | Sidebar overlays content |
| Animation | Page push/pop | Slide from edge |
| Content visibility | Replaced by sidebar | Dimmed under sidebar |
| Use case | Primary navigation | Secondary/optional panel |

#### Overlay Metrics

| Property | Value |
|----------|-------|
| Sidebar shadow (when overlay) | (4, 0) blur 12, black @ 0.15 |
| Content dim (when overlay) | black @ 0.20 |
| Sidebar slide direction | From left (LTR) or right (RTL) |
| Transition duration | 400ms |
| Transition easing | ease-in-out-cubic |

### Sidebar Header Bar

The sidebar pane has its own header bar:

| Property | Value |
|----------|-------|
| Height | Same as main header bar (47px) |
| Background | Same as sidebar_bg_color |
| Title | App name or section name |
| Window controls | Start side only (or none if right side) |
| Bottom border | 1px separator (same as main header bar) |

When collapsed, the sidebar header bar becomes the main header bar with a
hamburger menu or back navigation.

### Common Sidebar Patterns

#### Settings Sidebar

```
Navigation Sidebar:
  +-- General
  +-- Appearance
  +-- Notifications
  +-- Privacy
  +-- ...
```

#### Mail/Chat Sidebar

```
Navigation Sidebar:
  +-- Inbox        [42]
  +-- Starred
  +-- Sent
  +-- Drafts       [3]
  +-- Trash
```

#### File Manager Sidebar

```
Navigation Sidebar:
  +-- Home
  +-- Documents
  +-- Downloads
  +-- Pictures
  +-- ---separator---
  +-- Trash
  +-- Other Locations
```

### Keyboard Support

| Key | Action |
|-----|--------|
| Up / Down | Navigate sidebar items |
| Enter | Select item, show content |
| Alt+Left | Go back (when collapsed) |
| F9 | Toggle sidebar visibility |
| Ctrl+F | Search (if sidebar has search) |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Sidebar collapse | 400ms | ease-in-out-cubic |
| Sidebar expand | 400ms | ease-in-out-cubic |
| Page push (collapsed) | 400ms | ease-in-out-cubic |
| Page pop (collapsed) | 400ms | ease-in-out-cubic |
| Overlay show | 400ms | ease-in-out-cubic |
| Overlay dismiss | 400ms | ease-in-out-cubic |
| Overlay dim fade | 400ms | ease-in-out |
| Sidebar row select | immediate | — |
