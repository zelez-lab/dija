# App Bar

A persistent bar at the top of the screen providing navigation, branding, and contextual actions.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UINavigationBar | Documented |
| macOS | NSToolbar | Documented |
| Android | TopAppBar (M3) | Documented |
| Windows | CommandBar | Documented |
| Linux | AdwHeaderBar | Documented |

## iOS

Source: UINavigationBar, UINavigationItem, SwiftUI NavigationStack

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background (scrolled to top) | Material Regular (translucent) | Material Regular |
| Background (content scrolled under) | Solid systemBackground | Solid `#000000` (elevated: `#1C1C1E`) |
| Bottom separator (at rest) | Hidden | Hidden |
| Bottom separator (scrolled) | 0.33pt separator color | 0.33pt separator color |
| Tint color (bar buttons) | systemBlue | systemBlue |

The navigation bar is transparent/material at rest and transitions to a solid opaque surface when content scrolls underneath it.

### Height

| Configuration | Height | Notes |
|--------------|--------|-------|
| Standard title | 44pt | Fixed |
| Large title (expanded) | 96pt | Title below bar buttons |
| Large title (collapsed) | 44pt | Same as standard after scroll |
| Total (with status bar) | 44pt + status bar height | Status bar: 54pt (Dynamic Island), 47pt (notch), 20pt (legacy) |

### Title

| Style | Font | Weight | Size | Color | Alignment |
|-------|------|--------|------|-------|-----------|
| Standard | SF Pro | Semibold | 17pt | label | Centered |
| Large | SF Pro | Bold | 34pt | label | Left-aligned, below bar buttons |
| Large (search visible) | SF Pro | Bold | 34pt | label | Left-aligned |

#### Large Title Behavior

| Property | Value |
|----------|-------|
| Collapse threshold | ~50pt of scroll |
| Collapse animation | Smooth, tied to scroll offset (not spring) |
| Expand animation | Smooth, reverse of collapse |
| Large title left inset | 20pt |
| Large title bottom padding | 8pt |
| Transition | Title slides up and scales down to centered 17pt |

### Bar Buttons

| Property | Value |
|----------|-------|
| Font | SF Pro Regular, 17pt (text buttons) |
| Bold font | SF Pro Semibold, 17pt (emphasized/done buttons) |
| Icon size | SF Symbol, 22pt (medium weight) |
| Color | tintColor (systemBlue default) |
| Hit area | 44 x 44pt minimum |
| Spacing between buttons | 8pt |
| Left/right margin | 8pt from screen edge, 16pt content inset |

#### Back Button

| Property | Value |
|----------|-------|
| Icon | Chevron left (SF Symbol: `chevron.backward`) |
| Icon size | ~21pt height |
| Title | Previous screen's title (or "Back") |
| Title font | SF Pro Regular, 17pt |
| Color | tintColor |
| Max title width | ~2/3 of bar width, then ellipsis or hidden |
| Hit area | 44 x 44pt (extends right of chevron) |
| Swipe-back gesture | Interactive edge swipe from left 20pt |

### Search Bar Integration

When a search bar is attached to the navigation bar:

| Property | Value |
|----------|-------|
| Position | Below large title, above content |
| Visibility | Hidden by default, revealed on pull-down |
| Background | tertiarySystemFill in a rounded rect |
| Corner radius | 10pt |
| Height | 36pt |
| Animation | Slides down from under navigation bar |
| Cancel button | Appears right of search bar on focus |
| Cancel font | SF Pro Regular, 17pt |
| Cancel color | tintColor |

### Navigation Transitions

| Transition | Duration | Curve |
|-----------|----------|-------|
| Push | 0.35s | ease-in-out (interactive: matches gesture) |
| Pop | 0.35s | ease-in-out (interactive: matches gesture) |
| Interactive pop (swipe) | Gesture-driven | Linear with gesture, then spring to complete/cancel |
| Title crossfade | 0.2s | Fade during push/pop |

#### Push Animation Details

1. New view slides in from right edge
2. Current view slides left and dims slightly (parallax: moves ~1/3 speed)
3. Back button chevron slides in from left
4. New title fades in, old title fades out
5. If large title: new large title slides up into position

### Toolbar

A toolbar can appear at the bottom of the navigation controller.

| Property | Value |
|----------|-------|
| Height | 44pt (78pt with safe area) |
| Background | Material Regular (same as navigation bar) |
| Top separator | 0.33pt separator color |
| Button spacing | Flexible (equally distributed) |
| Button font | SF Pro Regular, 17pt |
| Button color | tintColor |

### Accessibility

| Property | Value |
|----------|-------|
| Back button | "Back" or previous title, button trait |
| Title | Header trait |
| VoiceOver navigation | Adjustable (swipe up/down to navigate sections) |

## macOS

Reference: NSToolbar, NSToolbarItem, NSWindow.ToolbarStyle, Apple HIG (macOS 14+).

### Overview

`NSToolbar` manages the toolbar area at the top of a window. Since macOS 11, toolbars are integrated with the title bar and support several display styles. The toolbar is a system-managed container -- you provide items and the system handles layout, overflow, and customization.

### Toolbar Styles

#### NSWindow.ToolbarStyle

| Style                | Height (pt) | Description                                      |
|----------------------|-------------|--------------------------------------------------|
| `.automatic`         | varies      | System picks based on window configuration       |
| `.expanded`          | ~78         | Tall toolbar with title above, items below        |
| `.preference`        | ~78         | Same as expanded, used for preferences windows    |
| `.unified`           | ~52         | Title and toolbar items on same row              |
| `.unifiedCompact`    | ~38         | Shorter unified, for utility/secondary windows    |

#### Height Breakdown (`.unified`)

| Component            | Height (pt) |
|---------------------|-------------|
| Title bar area       | 28          |
| Toolbar content area | 24          |
| Total                | 52          |

#### Height Breakdown (`.unifiedCompact`)

| Component            | Height (pt) |
|---------------------|-------------|
| Total                | 38          |

#### Height Breakdown (`.expanded`)

| Component            | Height (pt) |
|---------------------|-------------|
| Title bar area       | 28          |
| Toolbar content area | ~50         |
| Total                | ~78         |

### Toolbar Items

#### Standard Item Types

| Type                          | Description                                    |
|-------------------------------|------------------------------------------------|
| Custom item (with view)       | Any NSView embedded in toolbar                 |
| Image item                    | SF Symbol or NSImage button                    |
| Segmented item                | NSSegmentedControl in toolbar                  |
| Search item                   | NSSearchField in toolbar                       |
| Tracking separator            | Links to split view divider                     |
| Space                         | Fixed-size space (16 pt)                       |
| Flexible space                | Expanding space that fills available width       |
| Sidebar tracking separator    | Separator that tracks sidebar split view        |

#### Standard Identifiers

| Identifier                       | Description                                  |
|----------------------------------|----------------------------------------------|
| `.sidebarTrackingSeparator`      | Tracks sidebar divider position              |
| `.flexibleSpace`                 | Expanding gap                                |
| `.space`                         | Fixed 16 pt gap                              |
| `.toggleSidebar`                 | Standard sidebar toggle button               |
| `.print`                         | Standard print button                        |
| `.showColors`                    | Standard color panel button                  |
| `.showFonts`                     | Standard font panel button                   |
| `.inspectorTrackingSeparator`    | Tracks inspector divider (macOS 14+)         |
| `.toggleInspector`               | Standard inspector toggle button             |

### Metrics

#### Toolbar Item Sizing

| Control Size | Button Height (pt) | Icon Size (pt) | Min Width (pt) |
|-------------|-------------------|----------------|----------------|
| Regular     | 24                | 16             | 28             |
| Small       | 20                | 13             | 22             |

#### Spacing

| Property                        | Value (pt) |
|---------------------------------|------------|
| Inter-item spacing              | 8          |
| Item to edge padding            | 12         |
| Icon to label gap (labeled)     | 2          |
| Section gap (around separators) | 12         |

#### Toolbar Item Labels

When `displayMode` includes labels:

| Property                        | Value             |
|---------------------------------|-------------------|
| Font size                       | 10 pt             |
| Font weight                     | Regular           |
| Label position                  | Below icon        |
| Combined item height            | ~44 pt            |

### Colors

#### Toolbar Background

| Configuration           | Light Mode                   | Dark Mode                    |
|------------------------|------------------------------|------------------------------|
| Standard               | titlebar material vibrancy   | titlebar material vibrancy   |
| Fallback (no vibrancy) | `#ECECEC`                    | `#323232`                    |

#### Toolbar Items

| State        | Light Mode                    | Dark Mode                     |
|-------------|-------------------------------|-------------------------------|
| Normal       | Transparent                   | Transparent                   |
| Hover        | `rgba(0,0,0,0.06)`           | `rgba(255,255,255,0.08)`      |
| Pressed      | `rgba(0,0,0,0.10)`           | `rgba(255,255,255,0.12)`      |
| Selected     | `rgba(0,0,0,0.08)`           | `rgba(255,255,255,0.10)`      |
| Disabled     | 40% opacity icon/text         | 40% opacity icon/text         |

#### Separator Line

The separator line between toolbar and content:

| Context               | Light Mode              | Dark Mode               |
|-----------------------|-------------------------|-------------------------|
| Separator             | `rgba(0,0,0,0.12)`     | `rgba(255,255,255,0.12)`|
| Width                 | full window width       | full window width       |
| Height                | 0.5 pt                 | 0.5 pt                  |

#### Title Text

| Configuration      | Color Light          | Color Dark           | Font Size (pt) | Weight    |
|--------------------|----------------------|----------------------|----------------|-----------|
| Window title       | labelColor           | labelColor           | 13             | Semibold  |
| Subtitle           | secondaryLabelColor  | secondaryLabelColor  | 11             | Regular   |

### Traffic Light Positioning

The close/minimize/zoom buttons position depends on toolbar style:

| Style              | Traffic Light Position              |
|--------------------|-------------------------------------|
| `.unified`         | Vertically centered in title area   |
| `.unifiedCompact`  | Vertically centered in toolbar      |
| `.expanded`        | Top-left at standard offset (20, 20)|

Traffic light buttons:
- Diameter: 12 pt each
- Spacing: 8 pt between centers
- Left offset: 20 pt from window edge (7 pt from each button edge to next)

### Display Modes

#### NSToolbar.DisplayMode

| Mode              | Description                                  |
|-------------------|----------------------------------------------|
| `.default`        | System-chosen (currently icon only)          |
| `.iconAndLabel`   | Icons with text labels below                 |
| `.iconOnly`       | Icons only (most common)                     |
| `.labelOnly`      | Text labels only                             |

### Overflow Menu

When the window is too narrow for all toolbar items:
- Overflow chevron button appears at the right edge
- Clicking opens a menu with overflowed items
- Items overflow right-to-left (rightmost items overflow first)
- Flexible space items collapse before other items

### Toolbar Customization

Users can customize the toolbar (right-click > "Customize Toolbar..."):
- Drag items in/out of the toolbar
- Rearrange item order
- Choose display mode
- Reset to defaults
- Sheet presentation with all available items

### Animation

| Transition                        | Duration (ms) | Curve         |
|-----------------------------------|---------------|---------------|
| Toolbar show/hide                 | 250           | Ease In Out   |
| Toolbar item reorder              | 200           | Ease In Out   |
| Overflow menu appear              | 150           | Ease Out      |
| Sidebar tracking separator move   | 0             | Immediate     |
| Toolbar style change              | 300           | Ease In Out   |

### Dija Skin Mapping

```
comp! Toolbar {
    attr style, ToolbarStyle, default: ToolbarStyle::Unified
    attr display_mode, ToolbarDisplayMode, default: ToolbarDisplayMode::IconOnly

    // macOS skin maps:
    // ToolbarStyle::Unified        -> .unified (52 pt)
    // ToolbarStyle::UnifiedCompact -> .unifiedCompact (38 pt)
    // ToolbarStyle::Expanded       -> .expanded (78 pt)
    //
    // Background: titlebar vibrancy material
    // Items: transparent, hover highlight, 24 pt height
    // Separator: 0.5 pt line below toolbar
    // Traffic lights: system-positioned
}
```

## Android

Source: Material Design 3 TopAppBar, m3.material.io/components/app-bars/specs

### Overview

The top app bar displays navigation, actions, and text at the top of a screen. It contains a title and actions related to the current screen. M3 defines four variants: Small, Center-Aligned, Medium, and Large.

### Anatomy

```
+--------+------------------------------+--------+--------+--------+
| [Nav]  |         Title                | [Act1] | [Act2] | [More] |
+--------+------------------------------+--------+--------+--------+
```

| Element | Description |
|---------|-------------|
| Container | Background surface spanning full width |
| Navigation icon | Leading icon (back arrow, menu drawer) — 48x48dp touch target |
| Title | Primary text label (left-aligned or centered) |
| Action icons | Up to 3 trailing icons for contextual actions |
| Overflow menu | "More" icon revealing additional actions in a dropdown |

### Variants

| Variant | Container Height | Title Typography | Title Alignment | Description |
|---------|-----------------|-----------------|-----------------|-------------|
| Small | 64dp | Title Large (Roboto Regular 400, 22sp) | Left-aligned | Standard compact bar |
| Center-Aligned | 64dp | Title Large (Roboto Regular 400, 22sp) | Centered | Same as Small with centered title |
| Medium | 112dp | Headline Small (Roboto Regular 400, 24sp) | Left-aligned, bottom area | Two-row bar, title in expanded area below icons |
| Large | 152dp | Headline Medium (Roboto Regular 400, 28sp) | Left-aligned, bottom area | Tallest variant, prominent title below icons |

### Metrics

| Property | Value |
|----------|-------|
| Container width | Full screen width |
| Small/Center-Aligned height | 64dp |
| Medium height (expanded) | 112dp |
| Medium height (collapsed) | 64dp |
| Large height (expanded) | 152dp |
| Large height (collapsed) | 64dp |
| Horizontal padding (leading/trailing) | 4dp |
| Navigation icon container | 48x48dp |
| Navigation icon size | 24dp |
| Action icon container | 48x48dp |
| Action icon size | 24dp |
| Title left padding (with nav icon) | 16dp from nav icon end |
| Title left padding (no nav icon) | 16dp from container edge |
| Title bottom padding (Medium) | 24dp |
| Title bottom padding (Large) | 28dp |
| Title horizontal padding (Medium/Large expanded) | 16dp |

### Colors

#### Container

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Container (at rest) | surface | `#FEF7FF` | `#141218` |
| Container (scrolled) | surfaceContainer | `#F3EDF7` | `#211F26` |

#### Text and Icons

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Title text | onSurface | `#1D1B20` | `#E6E0E9` |
| Navigation icon | onSurface | `#1D1B20` | `#E6E0E9` |
| Action icons | onSurfaceVariant | `#49454F` | `#CAC4D0` |
| Overflow icon | onSurfaceVariant | `#49454F` | `#CAC4D0` |

### Elevation

| State | Elevation Level | Shadow (dp) |
|-------|----------------|-------------|
| At rest (flat) | Level 0 | 0dp |
| Scrolled (lifted) | Level 2 | 3dp (tonal elevation, no shadow — uses surfaceContainer) |

M3 uses tonal elevation rather than shadow-based elevation. The container color shifts from `surface` to `surfaceContainer` when content scrolls underneath, producing a subtle tint change instead of a drop shadow.

### States (Action Icon Buttons)

State layers use onSurfaceVariant at varying opacity, applied over the icon button area:

| State | State Layer Opacity | Icon Color |
|-------|-------------------|------------|
| Enabled | 0% | onSurfaceVariant |
| Hovered | 8% | onSurfaceVariant |
| Focused | 10% | onSurfaceVariant |
| Pressed | 10% + ripple | onSurfaceVariant |
| Disabled | 0% | onSurface @ 38% |

### Scroll Behavior

| Behavior | Description |
|----------|-------------|
| Pinned | Bar remains fixed, does not react to scroll |
| Lift on scroll | Bar stays fixed but elevates (surface to surfaceContainer) when content scrolls under — used by Small and Center-Aligned |
| Enter always | Bar collapses on scroll up, reappears on any scroll down |
| Exit until collapsed | Medium/Large collapse to 64dp on scroll up, expand when user reaches content top or scrolls down |

#### Collapsing Behavior (Medium / Large)

| Property | Value |
|----------|-------|
| Collapsed height | 64dp (same as Small) |
| Collapsed title style | Title Large (22sp) — matches Small variant |
| Title transition | Fades and slides from expanded position to collapsed inline position |
| Scroll connection | Tied to scroll offset (not spring-based) |
| Expand trigger | Scroll back to top of content |

### Overflow Menu

| Property | Value |
|----------|-------|
| Trigger icon | More vert (three vertical dots), 24dp |
| Menu background | surfaceContainer |
| Menu elevation | Level 2 (3dp) |
| Menu corner radius | 4dp |
| Menu item height | 48dp |
| Menu item font | Body Large (Roboto Regular 400, 16sp) |
| Menu item icon size | 24dp |
| Menu item padding | 12dp horizontal |
| Menu shadow | Elevation Level 2 |

### Accessibility

| Property | Value |
|----------|-------|
| Navigation icon | Content description required (e.g., "Navigate up") |
| Action icons | Content description required |
| Title | Heading semantics |
| Min touch target | 48x48dp for all interactive elements |
| Focus order | Navigation icon, title, action icons (left to right) |

## Windows

Source: WinUI 3 CommandBar, CommandBarFlyout controls

### CommandBar (Toolbar)

A horizontal bar containing AppBarButton commands with icon + optional label.

#### Bar Metrics

| Property | Value |
|----------|-------|
| Height (open, labels visible) | 60px |
| Height (compact, icons only) | 48px |
| Background | Transparent (inherits parent, typically Mica) |
| Padding | 8px horizontal |
| Corner radius | None (spans full width) |

#### AppBarButton

| Property | Value |
|----------|-------|
| Width | 48px (compact), variable (open with label) |
| Height | 48px (compact), 60px (open) |
| Icon size | 20x20px |
| Label font | 10px Caption, Regular |
| Label position | Below icon (when labels visible) |
| Corner radius | 4px |
| Background (rest) | Transparent |
| Background (hover) | SubtleFillColorSecondary |
| Background (pressed) | SubtleFillColorTertiary |

#### AppBarToggleButton

Same metrics as AppBarButton. When toggled on:

| State | Background |
|-------|-----------|
| Toggled rest | SubtleFillColorSecondary |
| Toggled hover | SubtleFillColorTertiary |
| Toggled pressed | SubtleFillColorSecondary |

#### AppBarSeparator

| Property | Value |
|----------|-------|
| Width | 1px |
| Height | 20px (centered vertically) |
| Color | DividerStrokeColorDefault |
| Margin | 8px horizontal |

#### Overflow (More) Button

| Property | Value |
|----------|-------|
| Icon | `&#xE10C;` (ellipsis / "...") |
| Size | 48x48px (same as AppBarButton) |
| Position | Right end of command bar |

#### Overflow Menu

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Padding | 4px vertical |
| Shadow | Shadow 8 |
| Border | 1px SurfaceStrokeColorFlyout |
| Item height | 40px |
| Item icon size | 16x16px (note: smaller than primary area) |
| Item font | 14px, Regular |
| Item padding | 12px horizontal |
| Max height | 480px (scrollable) |

### CommandBarFlyout

A floating command bar that appears contextually (e.g., on text selection or right-click). Consists of a primary row of icon buttons and an optional secondary menu.

#### Flyout Metrics

| Property | Value |
|----------|-------|
| Primary row height | 40px |
| Primary button width | 40px |
| Primary button icon size | 16x16px |
| Corner radius | 8px (layerCornerRadius) |
| Background | Acrylic (Background type) |
| Shadow | Shadow 8 |
| Border | 1px SurfaceStrokeColorFlyout |
| Padding | 4px |

#### Primary vs Secondary

```
+----------------------------------+
| [B] [I] [U] [link] [...]        |  <- Primary commands (icon-only, 40px)
+----------------------------------+
| Cut                     Ctrl+X   |  <- Secondary commands (menu items)
| Copy                    Ctrl+C   |
| Paste                   Ctrl+V   |
| ------------------------------- |
| Select All              Ctrl+A   |
+----------------------------------+
```

#### Secondary Menu Item

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px horizontal |
| Font | 14px, Regular |
| Icon size | 16x16px |
| Keyboard accelerator | 12px, TextFillColorSecondary, right-aligned |
| Icon-to-text gap | 12px |
| Separator | 1px DividerStrokeColorDefault, 4px vertical padding |

### States (Both)

#### AppBarButton / CommandBarFlyout Button States

| State | Background | Icon color |
|-------|-----------|-----------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |
| Disabled | Transparent | TextFillColorDisabled |

### Placement

| CommandBar | Position |
|-----------|----------|
| Top of page | Full width, below title bar |
| Bottom of page | Full width, above bottom edge |
| CommandBarFlyout | Anchored near selection or right-click point |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| CommandBarFlyout open | 200ms | Decelerate |
| CommandBarFlyout close | 150ms | Accelerate |
| Overflow menu expand | 200ms | Decelerate |
| Overflow menu collapse | 150ms | Accelerate |
| Button hover fill | 100ms | Control fast |

## Linux

### Overview

AdwHeaderBar is the defining UI element of GNOME applications. It replaces both the
OS title bar and toolbar, providing CSD (client-side decorations) with integrated
window controls.

### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | `#EBEBEB` (headerbar_bg_color) | `#303030` |
| Backdrop (unfocused) | `#FAFAFA` (window_bg_color) | `#242424` |
| Text color | `#2E3436` | `#FFFFFF` |
| Bottom border | 1px `rgba(0,0,0, 0.15)` | 1px `rgba(255,255,255, 0.15)` |
| Top corners | 12px (matches window CSD) | 12px |
| Top corners (maximized) | 0px | 0px |

### Metrics

| Property | Value |
|----------|-------|
| Min height | 47px |
| Horizontal padding | 6px |
| Widget spacing | 6px |
| Title area | Centered, between start/end widgets |
| Window controls size | 24px icons |
| Window controls spacing | 6px |

### Layout

```
+---+------+---+---------------------+---+------+---+
| P | [Btn] | S |       Title        | S | [Btn]| C |
+---+------+---+---------------------+---+------+---+
 ^                    ^                          ^
 6px padding     Centered title              6px padding
```

- **Start area**: Left-aligned buttons and widgets
- **Center area**: Title widget (text, view switcher, or custom)
- **End area**: Right-aligned buttons and widgets
- **Window controls**: Close, minimize, maximize (configurable position)

### Window Controls

Position determined by `org.gnome.desktop.wm.preferences button-layout`:

| Layout String | Result |
|--------------|--------|
| `close,minimize,maximize:` | Controls on left (macOS-like) |
| `:minimize,maximize,close` | Controls on right (default) |
| `close:` | Close only, on left |
| `:close` | Close only, on right |
| (empty) | No window controls |

#### Button Sizes

| Button | Icon Size | Hit Area |
|--------|-----------|----------|
| Close | 16px | 24x24px |
| Minimize | 16px | 24x24px |
| Maximize | 16px | 24x24px |

#### Close Button

| State | Light | Dark |
|-------|-------|------|
| Rest | transparent (flat) | transparent |
| Hover | `rgba(224,27,36, 0.15)` (red tint) | `rgba(224,27,36, 0.15)` |
| Active | `rgba(224,27,36, 0.30)` | `rgba(224,27,36, 0.30)` |

The close button has a distinctive red hover state, unlike other window controls.

### Title

#### Text Title (Default)

| Property | Value |
|----------|-------|
| Font | Adwaita Sans Bold, 15px |
| Alignment | Centered in available space |
| Ellipsis | Truncate with "..." when no space |

#### Title + Subtitle

| Property | Value |
|----------|-------|
| Title font | Adwaita Sans Bold, 15px |
| Subtitle font | Adwaita Sans Regular, 13px, dim-label |
| Subtitle color | secondary (dim) |
| Vertical stacking | Title above, subtitle below |

#### Custom Title Widget

The title area can be replaced with any widget:

| Common replacements | Widget |
|--------------------|--------|
| View switcher | `AdwViewSwitcher` (tabs in header) |
| Search entry | `GtkSearchEntry` (search mode) |
| Custom combo | `GtkDropDown` |
| Breadcrumbs | Custom widget |

### Header Bar Variants

#### Default (.toolbar Style)

All header bars automatically get the `.toolbar` appearance:

| Property | Value |
|----------|-------|
| Inner buttons | Flat style by default |
| Button padding | 8px 10px |
| Button min-size | 34px |

#### Flat Header Bar

Adding `.flat` removes the bottom border and makes the header bar blend with content:

| Property | Value |
|----------|-------|
| Background | transparent (inherits window bg) |
| Bottom border | none |
| Usage | Single-view apps, content-heavy layouts |

#### Development Style

Adding `.devel` adds a striped pattern for development/nightly builds:

| Property | Value |
|----------|-------|
| Background | Diagonal stripes overlay |
| Usage | Development builds, nightly apps |

### Backdrop Behavior

When the window loses focus:

| Property | Focused | Unfocused (Backdrop) |
|----------|---------|---------------------|
| Background | headerbar_bg_color | window_bg_color |
| Text opacity | 1.0 | 1.0 (text remains readable) |
| Button opacity | 1.0 | subtly reduced |
| Transition | — | 200ms ease-in-out |

### Integration with Content

The header bar is typically the first child of `AdwToolbarView`:

```
AdwToolbarView
 +-- AdwHeaderBar (top-bar)
 +-- Content (scrollable)
 +-- [Bottom bar] (optional)
```

| Property | Value |
|----------|-------|
| Top bar mode | `ADW_TOOLBAR_FLAT` or `ADW_TOOLBAR_RAISED` |
| Raised mode | Adds bottom shadow when content is scrolled |
| Raised border | Replaces static border with scroll-dependent shadow |

### Keyboard Support

| Key | Action |
|-----|--------|
| Alt+F4 | Close window |
| Super+Up | Maximize |
| Super+Down | Restore/minimize |
| Alt+Space | Window menu |
| F11 | Fullscreen toggle |

### Drag Behavior

| Action | Effect |
|--------|--------|
| Drag on empty header bar area | Move window |
| Double-click on header bar | Maximize / restore |
| Right-click on header bar | Window context menu |
| Middle-click on header bar | Lower window (configurable) |

### Fullscreen and Maximized

| State | Header Bar Changes |
|-------|--------------------|
| Normal | 12px top corners, full controls |
| Maximized | 0px top corners, full controls |
| Tiled (half screen) | 0px on tiled edge, 12px on free edge |
| Fullscreen | Header bar auto-hides, revealed on mouse hover at top |
