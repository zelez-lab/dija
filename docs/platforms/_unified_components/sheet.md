# Sheet

A surface that slides in from the edge of the screen to present supplementary content or actions without leaving the current context.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UISheetPresentationController + UIAlertController (actionSheet) | Documented |
| macOS | NSPanel (sheet) | Documented |
| Android | BottomSheet (M3) | Documented |
| Windows | Flyout | Documented |
| Linux | --- | No native equivalent |

## iOS

### Sheet (UISheetPresentationController)

Source: UISheetPresentationController (iOS 15+), SwiftUI `.sheet` / `.presentationDetents`

#### Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | systemBackground (`#FFFFFF`) | secondarySystemBackground (`#1C1C1E`) |
| Corner radius | 10pt (top-left and top-right only) | 10pt |
| Corner curve | `.continuous` (superellipse) | |
| Shadow | offset(0, -10) blur 40, black @ 0.2 | offset(0, -10) blur 40, black @ 0.3 |
| Bottom corners | Square (extend to bottom of screen) | |

Note: In dark mode, sheets use an **elevated** background (`#1C1C1E`) rather than the base `#000000` to create visual separation from the underlying content.

#### Grabber Handle

| Property | Value |
|----------|-------|
| Size | 36 x 5pt |
| Corner radius | 2.5pt (fully rounded) |
| Color | systemGray3 (`#C7C7CC` / `#48484A`) |
| Position | Centered horizontally, 5pt from top |
| Visibility | Optional (shown by default when multiple detents) |
| Hit area | 44 x 44pt (for accessibility) |

#### Detents

Predefined stop points for sheet height:

| Detent | Height | Notes |
|--------|--------|-------|
| Medium | ~50% of screen height | Approximately half |
| Large | Full screen (minus status bar) | Default |
| Custom | Arbitrary value | Fraction of container, fixed pt, or content-based |

##### Detent Behavior

| Property | Value |
|----------|-------|
| Snap threshold | ~20% of distance between detents |
| Velocity threshold | High velocity overrides position threshold |
| Overdrag (past largest) | Rubber-band effect, springs back |
| Underdrag (past smallest) | Dismiss if `dismissible`, else rubber-band |

#### Background Dimming

| Property | Value |
|----------|-------|
| Dimming at large detent | black @ 0.4 (default) |
| Dimming at medium detent | None (by default) |
| `largestUndimmedDetentIdentifier` | Controls which detent stops dimming |
| Interaction behind sheet | Allowed when undimmed |
| Dimming animation | Tracks sheet position (not separate animation) |

#### Background Content Scaling

When presenting a sheet on top of another sheet or navigation:

| Property | Value |
|----------|-------|
| Background scale | Shrinks to ~0.92 of original size |
| Background corner radius | Matches device screen corners |
| Background offset | Moves up ~10pt |
| Transition | Synchronized with sheet presentation |
| `prefersEdgeAttachedInCompactHeight` | Sheet attaches to edge on compact |

#### Animation

##### Present

| Property | Value |
|----------|-------|
| Duration | 0.35s |
| Curve | Spring (damping ~0.85, response 0.35) |
| Direction | Slides up from bottom of screen |
| Backdrop dimming | Fades in during slide |
| Background scale | Animates to 0.92 simultaneously |
| Initial velocity | 0 (unless gesture-driven) |

##### Dismiss

| Property | Value |
|----------|-------|
| Duration | 0.3s |
| Curve | ease-in (or spring if gesture-driven) |
| Direction | Slides down to bottom |
| Backdrop dimming | Fades out |
| Background scale | Animates back to 1.0 |

##### Detent Transition

| Property | Value |
|----------|-------|
| Duration | 0.3s |
| Curve | Spring (damping ~0.8) |
| Snap | Springs to nearest detent |
| Velocity-based | Inherits gesture velocity |

#### Interactive Dismissal

| Property | Value |
|----------|-------|
| Gesture | Pan down on sheet |
| Gesture area | Grabber or navigation bar (preferably) |
| Content scrolling | Sheet dismissal deferred until scroll reaches top |
| Dismiss threshold | ~50% of current detent height or high velocity |
| Cancel threshold | Released above 50% → springs back to detent |
| Rubber-band | Present when dragging past top detent |
| Haptic | None during drag |

#### Scroll Integration

| Property | Value |
|----------|-------|
| `prefersScrollingExpandsWhenScrolledToEdge` | Scroll to top → expand sheet before bouncing |
| Scroll lock at medium | Content scrolls only when at large detent |
| Scroll-to-dismiss | Scroll to top at large detent → drag dismisses |

#### Navigation Bar in Sheet

| Property | Value |
|----------|-------|
| Title | SF Pro Semibold, 17pt, centered |
| Close button position | Top-right (SF Symbol: `xmark.circle.fill`) |
| Close button color | systemGray3 |
| Close button size | 30pt |
| Bar background | Transparent (no material) until scrolled |

#### Popover (iPad)

On iPad, `.sheet` can present as a popover or form sheet:

| Property | Value |
|----------|-------|
| Form sheet width | 540pt |
| Form sheet height | Content-dependent (max ~620pt) |
| Corner radius | 14pt (all four corners) |
| Shadow | offset(0, 10) blur 40, black @ 0.25 |
| Dimming | black @ 0.4 |
| Position | Centered on screen |

#### Accessibility

| Property | Value |
|----------|-------|
| Grabber | "Sheet grabber, adjustable" |
| Dismiss | Escape gesture or swipe down |
| VoiceOver | Announces sheet content on presentation |
| Focus | Moves to sheet content on present |

### Action Sheet (UIAlertController)

Source: UIAlertController (style: .actionSheet), SwiftUI confirmationDialog

#### iPhone Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | Ultra-thick material | Ultra-thick material |
| Corner radius | 14pt | 14pt |
| Corner curve | `.continuous` (superellipse) | |
| Position | Bottom of screen, above safe area | |
| Width | Screen width - 16pt (8pt margin each side) | |
| Safe area bottom margin | 8pt above home indicator | |

#### Layout

Action sheets on iPhone consist of two separate rounded cards:

```
+-----------------------------+
|       Header (optional)      |  <- Title + message
+-----------------------------+
|         Action 1             |  <- 57pt per action
+-----------------------------+
|         Action 2             |
+-----------------------------+
|    Destructive Action        |  <- systemRed text
+-----------------------------+
        8pt gap
+-----------------------------+
|          Cancel              |  <- separate card
+-----------------------------+
```

#### Dimensions

| Element | Value |
|---------|-------|
| Action button height | 57pt |
| Header padding (top/bottom) | 14pt |
| Header padding (horizontal) | 16pt |
| Separator | 0.33pt, separator color |
| Gap between action group and cancel | 8pt |
| Cancel button height | 57pt |
| Side margins | 8pt (each side) |

#### Typography

| Element | Font | Size | Weight | Color | Alignment |
|---------|------|------|--------|-------|-----------|
| Title | SF Pro | 13pt | Semibold | secondaryLabel | Centered |
| Message | SF Pro | 13pt | Regular | secondaryLabel | Centered |
| Regular action | SF Pro | 20pt | Regular | tintColor (systemBlue) | Centered |
| Destructive action | SF Pro | 20pt | Regular | systemRed | Centered |
| Cancel | SF Pro | 20pt | Semibold | tintColor | Centered |

Note: The title and message in action sheets use a smaller 13pt size compared to alerts (17pt title).

#### Button States

| State | Effect |
|-------|--------|
| Pressed | Background highlight (systemGray4 fill) |
| Disabled | Text alpha 0.3 |

#### iPad Presentation

On iPad, action sheets appear as popovers, not bottom sheets.

| Property | Value |
|----------|-------|
| Style | Popover (arrow pointing to source) |
| Width | ~320pt (content-dependent) |
| Corner radius | 14pt |
| Arrow size | 13pt height |
| Shadow | offset(0, 10) blur 40, black @ 0.25 |
| Background | Ultra-thick material |
| No cancel button | Dismiss by tapping outside |
| No dimming | Background remains interactive |

#### Dimming Backdrop (iPhone)

| Property | Value |
|----------|-------|
| Overlay | black @ 0.4 |
| Tap to dismiss | Tapping backdrop triggers cancel |
| Animation | Fade in/out with sheet |

#### Animation

##### Present (iPhone)

| Property | Value |
|----------|-------|
| Duration | 0.3s |
| Curve | Spring (damping ~0.85) |
| Direction | Slides up from bottom |
| Backdrop | Fades in simultaneously |
| Cancel card | Appears with main card (no stagger) |

##### Dismiss (iPhone)

| Property | Value |
|----------|-------|
| Duration | 0.25s |
| Curve | ease-in |
| Direction | Slides down to bottom |
| Backdrop | Fades out simultaneously |

##### Present (iPad Popover)

| Property | Value |
|----------|-------|
| Duration | 0.25s |
| Curve | ease-out |
| Scale | Start at 0.9, animate to 1.0 |
| Opacity | Fade in |

#### Interactive Dismissal

| Property | Value |
|----------|-------|
| Gesture | Swipe down on action sheet |
| Threshold | ~50pt or 50% velocity |
| Snap back | Spring if released above threshold |
| Dismiss | Animates down if below threshold |

#### Accessibility

| Property | Value |
|----------|-------|
| VoiceOver | "Action sheet, [title], [message]" |
| Focus | First action |
| Escape gesture | Triggers cancel |
| Actions | Each announced as button |

## macOS

Reference: NSPanel, NSWindow.beginSheet, Apple HIG (macOS 14+).

### Overview

A sheet is a modal dialog attached to a specific window. It slides down from the title bar area and blocks interaction with the parent window. Sheets are macOS-specific -- other platforms use full-screen modals or bottom sheets instead.

### Presentation

#### Attachment Point

The sheet attaches to the bottom edge of the parent window's toolbar/title bar area:

```
+========================================+
|  Parent Window Title Bar / Toolbar     |
+========================================+  <- sheet slides down from here
|  +----------------------------------+  |
|  |          Sheet Content           |  |
|  |                                  |  |
|  |        [Cancel]  [Confirm]       |  |
|  +----------------------------------+  |
|                                        |
|        (Parent content dimmed)         |
|                                        |
+========================================+
```

#### Animation

| Phase                  | Duration (ms) | Curve          |
|-----------------------|---------------|----------------|
| Presentation (drop)    | 250           | Ease In Out    |
| Dismissal (retract)    | 200           | Ease In Out    |
| Parent window dimming  | 200           | Ease In Out    |
| Content fade-in        | 200           | Ease Out       |

The sheet drops down with a slight vertical overshoot (very subtle spring), then settles.

### Metrics

#### Sizing

| Property                  | Value                   | Notes                        |
|---------------------------|-------------------------|------------------------------|
| Width                      | Parent window width - 40 (max) | Centered horizontally   |
| Minimum width              | 300 pt                  |                              |
| Maximum width              | Parent window width     | Cannot exceed parent          |
| Minimum height             | 100 pt                  |                              |
| Maximum height             | Parent window height - 44 | Leave room for title bar     |
| Corner radius              | 10 pt                   | Bottom corners only           |
| Top corners                | 0 pt (attached to title bar) | Attached flush             |

#### Content Layout

| Property                  | Value (pt) |
|---------------------------|------------|
| Content padding (top)      | 20         |
| Content padding (sides)    | 20         |
| Content padding (bottom)   | 20         |

#### Button Area

| Property                  | Value (pt) |
|---------------------------|------------|
| Button area margin top     | 16         |
| Button height              | 22         |
| Button min width           | 68         |
| Button spacing             | 8          |
| Button alignment           | Right-aligned |

### Parent Window Behavior

When a sheet is presented:

| Behavior                    | Description                                  |
|-----------------------------|----------------------------------------------|
| Parent interaction          | Blocked                                      |
| Parent window move          | Still movable (sheet moves with it)           |
| Parent window resize        | Depends on configuration                     |
| Parent dimming              | Subtle darkening of content area              |
| Parent title bar            | Still visible, traffic lights still work       |
| Close button (red)          | May dismiss sheet or close window (configurable) |

#### Parent Dimming

| Property                  | Value                    |
|---------------------------|--------------------------|
| Overlay color (light)      | `rgba(0,0,0,0.08)`     |
| Overlay color (dark)       | `rgba(0,0,0,0.15)`     |
| Covers                     | Content area only (not title bar) |

### Colors

#### Background

| Mode      | Value                                          |
|-----------|------------------------------------------------|
| Light     | `#ECECEC` (windowBackgroundColor)              |
| Dark      | `#323232` (windowBackgroundColor)              |

Sheets can also use vibrancy if desired (`.sheet` material).

#### Shadow

The sheet does not have its own shadow in the traditional sense since it is attached to the window. However, a subtle drop shadow separates it from the dimmed content below:

```
Color:   rgba(0, 0, 0, 0.15)
Offset:  (0, 4) pt
Blur:    16 pt
```

### Common Sheet Types

#### Save/Open Sheet (NSSavePanel / NSOpenPanel)

| Property                  | Value              |
|---------------------------|--------------------|
| Width                      | ~480 pt (standard) |
| File browser height        | ~320 pt            |
| Sidebar width              | ~160 pt            |

#### Print Sheet (NSPrintPanel)

| Property                  | Value              |
|---------------------------|--------------------|
| Width                      | ~640 pt            |
| Height                     | Varies with options |

#### Custom Sheet

For custom content, use `NSWindow.beginSheet(_:completionHandler:)`.

### Multiple Sheets

macOS supports stacking multiple sheets on a single window:
- Each subsequent sheet slides over the previous one
- Previous sheets compress upward (accordion effect)
- The topmost sheet is the only interactive one
- Dismissing the top sheet reveals the one beneath

#### Stacking Animation

| Phase              | Duration (ms) | Curve          |
|-------------------|---------------|----------------|
| Push (new sheet)   | 250           | Ease In Out    |
| Previous compress  | 250           | Ease In Out    |
| Pop (dismiss top)  | 200           | Ease In Out    |
| Previous expand    | 200           | Ease In Out    |

### Typography

| Element              | Font Size (pt) | Weight     | Color               |
|----------------------|----------------|------------|----------------------|
| Sheet title          | 13             | Bold       | labelColor           |
| Sheet body text      | 13             | Regular    | labelColor           |
| Sheet secondary text | 11             | Regular    | secondaryLabelColor  |

### Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Return / Enter  | Activate default button                    |
| Escape / Cmd+.  | Activate cancel button (dismiss sheet)     |
| Tab             | Navigate between controls                  |

### Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.sheet`                                  |
| Relation     | Child of parent window                     |
| Focus        | Trapped within sheet (modal)               |
| Announced    | Sheet title + content on presentation      |

### Dija Skin Mapping

```
comp! Sheet {
    // Sheet is a presentation mode, not a standalone component.
    // Dija needs:
    //
    // 1. Platform backend API to present a sheet on a window
    // 2. On macOS: use NSWindow.beginSheet() natively
    // 3. On other platforms: simulate with a modal overlay
    //
    // macOS skin properties:
    // Corner radius: 10 pt (bottom corners only)
    // Background: windowBackgroundColor
    // Animation: slide down 250ms ease-in-out
    // Dimming: rgba(0,0,0,0.08) light / rgba(0,0,0,0.15) dark
    // Width: constrained to parent window width
    // Buttons: right-aligned, default button accent-filled
}
```

## Android

Source: m3.material.io/components/bottom-sheets/specs

### Variants

| Variant | Behavior | Scrim |
|---------|----------|-------|
| Standard | Coexists with main content, non-blocking | No |
| Modal | Blocks main content, requires dismissal | Yes (32%) |

### Metrics

| Property | Value |
|----------|-------|
| Corner radius (top-left, top-right) | 28dp (extra-large) |
| Corner radius (bottom) | 0dp |
| Surface | surfaceContainerLow |
| Elevation | Level 1 (1dp) |
| Min height (peek) | Content-dependent |
| Max height | Screen height - status bar |
| Horizontal padding | 0dp (content provides own padding) |
| Content padding (typical) | 16dp - 24dp |

### Drag Handle

Optional drag handle at the top for swipe affordance:

| Property | Value |
|----------|-------|
| Width | 32dp |
| Height | 4dp |
| Corner radius | 2dp (full pill) |
| Color | onSurfaceVariant @ 40% |
| Top margin | 22dp (center of 48dp touch target) |
| Touch target | 48dp x 48dp |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#F7F2FA` (surfaceContainerLow) | `#1D1B20` |
| Drag handle | `#49454F` @ 40% | `#CAC4D0` @ 40% |
| Scrim (modal) | `#000000` @ 32% | `#000000` @ 32% |

### Sheet States

| State | Corner radius | Description |
|-------|---------------|-------------|
| Hidden | 28dp | Sheet below screen |
| Collapsed (peek) | 28dp | Partially visible, shows peek content |
| Half-expanded | 28dp | Midpoint, optional detent |
| Expanded | 28dp -> 0dp | Full height, corners may animate to 0dp |

When fully expanded to screen height, corners animate from 28dp to 0dp
to visually merge with the screen edge.

### Standard Bottom Sheet

- Sits alongside main content
- Can be swiped between collapsed and expanded
- Does not dim background
- Does not block interaction with main content

### Modal Bottom Sheet

- Overlays main content with scrim
- Tap scrim or swipe down to dismiss
- Blocks interaction with content behind
- Uses higher elevation (Level 1)

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Show (slide up) | Medium 3 (350ms) | Emphasized decelerate |
| Hide (slide down) | Medium 2 (300ms) | Standard accelerate |
| Snap to detent | Medium 1 (250ms) | Standard |
| Corner radius (expand) | Medium 2 (300ms) | Standard |
| Scrim fade in | Medium 2 (300ms) | Standard |
| Scrim fade out | Short 4 (200ms) | Standard accelerate |

### Swipe Behavior

- Swipe velocity threshold: 500dp/s (fast fling dismisses)
- Position threshold: 50% of remaining distance to next detent
- Overscroll: elastic resistance at bounds

### Layout

```
+--------------------------------------------+
|                                            |
|             Main Content                   |
|                                            |
+============================================+  <- top edge
|             ___________                    |
|            | drag handle |                 |
|             -----------                    |
|  28dp corner                    28dp corner|
|                                            |
|  Sheet content                             |
|  (scrollable)                              |
|                                            |
|                                            |
+--------------------------------------------+
```

### Comparison with iOS Sheet

| Property | iOS Sheet | M3 Bottom Sheet |
|----------|----------|----------------|
| Corner radius | 10dp (squircle) | 28dp (circular) |
| Background | System material (blur) | surfaceContainerLow (opaque) |
| Drag indicator | 36x5dp, gray pill | 32x4dp pill |
| Detents | medium, large, custom | collapsed, half, expanded |
| Scrim | Dim | Dim (32%, no blur) |

## Windows

Source: WinUI 3 Flyout, MenuFlyout, MenuBar controls

### Flyout (Generic Popup)

A light-dismiss popup anchored to a control, containing arbitrary content.

#### Metrics

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Padding | 16px |
| Border | 1px SurfaceStrokeColorFlyout |
| Shadow | Shadow 8 |
| Max width | 456px |
| Min width | 96px |

#### Placement

| Mode | Description |
|------|------------|
| Top | Above the target, centered |
| Bottom | Below the target, centered |
| Left | Left of target, vertically centered |
| Right | Right of target, vertically centered |
| Full | Centered in window |
| Auto | System chooses best placement |

Default placement: `Top`. Flyout repositions automatically to stay within window bounds.

#### Arrow gap

8px between the flyout surface and the anchor element.

### MenuFlyout (Context Menu)

A popup containing a list of selectable menu items, typically shown on right-click or via a menu button.

#### Container Metrics

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Padding | 4px vertical, 0px horizontal |
| Border | 1px SurfaceStrokeColorFlyout |
| Shadow | Shadow 8 |
| Min width | 128px |
| Max width | 456px |
| Max height | 480px (scrollable) |

#### MenuFlyoutItem

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px left, 12px right |
| Corner radius | 4px (with 2px horizontal margin) |
| Font | 14px, Regular |
| Icon size | 16x16px |
| Icon-to-text gap | 12px |
| Keyboard accelerator text | 12px, TextFillColorSecondary, right-aligned |
| Checkmark width | 16px (when applicable) |

#### MenuFlyoutItem States

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |
| Disabled | Transparent | TextFillColorDisabled |

#### MenuFlyoutSeparator

| Property | Value |
|----------|-------|
| Height | 1px |
| Color | DividerStrokeColorDefault |
| Margin | 4px vertical, 0px horizontal |

#### MenuFlyoutSubItem (Submenu)

| Property | Value |
|----------|-------|
| Chevron icon | `&#xE76C;` (right arrow), 12x12px, right-aligned |
| Submenu offset | Overlaps parent by 4px horizontally |
| Submenu open delay | 200ms (hover) |
| Submenu close delay | 150ms (mouse exit) |

#### Menu Structure

```
+-------------------------------+
| [ ] Menu item with checkmark  |
| [ ] Radio menu item           |
|     Menu item (no icon)       |
| ----------------------------- |
| [ ] Paste             Ctrl+V  |
| [ ] Open submenu          >   |
| ----------------------------- |
|     Disabled item             |
+-------------------------------+
```

### MenuBar

A horizontal bar of top-level menus (File, Edit, View, etc.).

#### Bar Metrics

| Property | Value |
|----------|-------|
| Height | 32px |
| Background | Transparent |
| Item padding | 12px horizontal |
| Item font | 14px, Regular |

#### MenuBarItem States

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Open (menu visible) | SubtleFillColorTertiary | TextFillColorPrimary |

### ToggleMenuFlyoutItem

Same as MenuFlyoutItem with a checkmark indicator:

| Property | Value |
|----------|-------|
| Checkmark icon | `&#xE73E;`, 16x16px, AccentColor |
| Checkmark position | Left, replacing the icon area |
| Unchecked | No checkmark, icon area empty |

### RadioMenuFlyoutItem

Same as ToggleMenuFlyoutItem but with a radio bullet:

| Property | Value |
|----------|-------|
| Bullet | 8px filled circle, AccentColor |
| Bullet position | Left, centered in 16px icon area |

### Behavior

| Behavior | Flyout | MenuFlyout |
|----------|--------|-----------|
| Light dismiss | Yes (click outside closes) | Yes |
| Escape key | Closes | Closes current level |
| Arrow keys | N/A | Navigate items |
| Enter | N/A | Activate item |
| Right arrow | N/A | Open submenu |
| Left arrow | N/A | Close submenu |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Flyout open (scale + fade) | 200ms | Decelerate |
| Flyout close (fade) | 150ms | Accelerate |
| Menu item hover fill | 100ms | Control fast |
| Submenu open | 200ms | Decelerate |
| Submenu close | 150ms | Accelerate |

## Linux

No native equivalent. Dija renders as a bottom slide-up panel following GNOME/Adwaita styling conventions.
