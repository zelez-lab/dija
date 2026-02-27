# macOS Platform Gaps for Dija

What Dija needs to implement or integrate with to feel native on macOS.

## Critical Gaps (P0 -- blocks native look)

### 1. Vibrancy / Translucent Materials

**Status:** Not implemented.

macOS windows, sidebars, menus, and popovers rely on real-time gaussian blur of background content combined with tint/saturation layers. Without vibrancy, Dija windows look flat and foreign.

**What Dija needs:**
- `Material` abstraction in dija-core (blur radius, tint, saturation, opacity)
- GPU blur pass in dija-render (dual-pass Kawase or box blur on render target)
- `NSVisualEffectView` integration on macOS Metal backend (embed `CAMetalLayer` inside vibrancy view)
- Opaque fallback for software backend and accessibility mode

**Complexity:** High. Requires compositor integration or multi-pass GPU rendering.

### 2. Title Bar Integration

**Status:** Not implemented.

macOS apps commonly extend content into the title bar area (unified toolbar, transparent titlebar, full-size content view). Finder, Safari, Xcode all do this.

**What Dija needs:**
- `NSWindow` style mask configuration: `.fullSizeContentView`, `.titlebarAppearsTransparent`
- Content insets for title bar height (52 pt unified, 38 pt compact)
- Safe area concept that accounts for title bar + toolbar
- `titleVisibility` control (`.visible` / `.hidden`)

### 3. Traffic Light Buttons (Window Controls)

**Status:** Not implemented.

The close/minimize/zoom buttons at top-left of every macOS window have specific behavior:
- 12x12 pt circles, 8 pt spacing between them
- 20 pt inset from top-left (standard) or centered in toolbar
- Hover: show X/minus/plus glyphs
- Inactive window: all gray
- Custom positioning when titlebar is transparent

**What Dija needs:**
- Platform backend hook to position/style window controls
- Support for `standardWindowButton(_:)` positioning
- Toolbar-integrated traffic lights (when toolbar style is unified)

### 4. System Font (SF Pro)

**Status:** Partial. Dija bundles Inter, not SF Pro.

macOS uses SF Pro exclusively. Apps using non-system fonts look out of place in the system context.

**What Dija needs:**
- Platform font resolution: on macOS, `FontFamily::System` should resolve to SF Pro
- Dynamic tracking support (SF Pro tracking varies by point size)
- SF Mono resolution for monospace contexts
- SF Pro Rounded variant support
- Respect for user text size preferences (System Settings > Display > Text Size)

### 5. Native Menus

**Status:** Not implemented.

macOS has a global menu bar. All apps are expected to have one. Context menus also use the system menu appearance.

**What Dija needs:**
- `NSMenu` / `NSMenuItem` integration for the application menu bar
- Context menu API that creates native `NSMenu` (not a custom rendered popup)
- Keyboard shortcut display in menu items (Command symbol rendering)
- Menu validation (enabling/disabling items based on state)

## High Priority (P1 -- feels non-native without these)

### 6. Cursor Management

macOS uses specific cursors for different contexts:
- Arrow (default), Pointing Hand (links), I-Beam (text), Crosshair (selection)
- Resize cursors (horizontal, vertical, diagonal variants)
- Drag cursors (copy, link, generic)
- NSCursor has 20+ standard cursor types

**What Dija needs:**
- `NSCursor` integration in the platform backend
- Cursor change API tied to hover/focus state of elements

### 7. Focus Ring

macOS draws a distinctive blue focus ring (3 pt stroke, 2 pt offset) around focused controls. It uses the accent color.

```
Color:   controlAccentColor with 0.50 alpha
Width:   3 pt stroke
Offset:  2 pt outset from control bounds
Radius:  control corner radius + 3 pt
Animation: 150 ms ease-out on focus, 200 ms ease-in on blur
```

**What Dija needs:**
- Focus ring rendering in dija-render (outset rounded rect with accent color)
- Focus ring animation
- Support for `focusRingType` (`.default`, `.none`, `.exterior`)

### 8. Scroll Bars

macOS scroll bars overlay content (not inset), auto-hide, expand on hover, and support elastic overscroll.

**What Dija needs:**
- Overlay scroll bar rendering (6 pt collapsed, 8 pt hover width)
- Auto-hide with 1500 ms timeout after scrolling stops
- Elastic overscroll (rubber band physics)
- Respect for "Show scroll bars" system preference (Always / When Scrolling / Automatic)
- Scroll bar color adapts to content underneath

### 9. Drag and Drop

macOS has deep system-wide drag and drop support (pasteboard, promised files, spring loading).

**What Dija needs:**
- `NSDraggingSource` / `NSDraggingDestination` protocol integration
- Drag preview rendering (semi-transparent snapshot of dragged content)
- Drop target highlighting
- Spring-loaded folders/containers (hover to expand)
- Pasteboard type registration

### 10. Sheets

Modal sheets slide down from the title bar with a specific animation and dim the parent window.

**What Dija needs:**
- Sheet presentation API (slide-down animation, 250 ms ease-in-out)
- Parent window dimming during sheet
- Sheet sizing (width constrained to window width minus padding)
- `NSPanel` sheet integration or equivalent custom rendering

### 11. Popovers

**What Dija needs:**
- Arrow-pointing popover rendering
- Automatic positioning (prefer below, flip if insufficient space)
- `.popover` material vibrancy background
- Click-outside dismissal
- Popover arrow: 16 pt wide, 8 pt tall

## Medium Priority (P2 -- polish and completeness)

### 12. System Color Scheme Detection

**What Dija needs:**
- `NSAppearance` observation for light/dark mode changes
- `effectiveAppearance` monitoring on views
- Respond to accent color changes
- Respond to "Increase Contrast" accessibility setting
- Respond to "Reduce Transparency" setting

### 13. Window Management

**What Dija needs:**
- `NSWindow.StyleMask` configuration (titled, closable, miniaturizable, resizable)
- Window level management (normal, floating, modal panel, status bar)
- Full-screen transition support
- Window tab grouping (macOS 12+)
- Stage Manager awareness (macOS 13+)
- Window restoration (state encoding/decoding)

### 14. Toolbar

**What Dija needs:**
- `NSToolbar` integration or equivalent rendering
- Toolbar styles: `.automatic`, `.expanded`, `.preference`, `.unified`, `.unifiedCompact`
- Overflow menu when toolbar items exceed width
- Customization sheet ("Customize Toolbar...")
- Toolbar item types: button, segmented, search, separator, flexible space

### 15. Touch Bar Support (Legacy)

Relevant for 2016-2020 MacBook Pro models. Low priority but consider an abstraction.

### 16. Accessibility

**What Dija needs:**
- `NSAccessibility` protocol integration
- VoiceOver support (roles, labels, traits, actions)
- Accessibility element tree mirroring the UI tree
- Keyboard navigation (Tab/Shift-Tab, arrow keys, Return/Space to activate)
- Reduced motion preference detection

### 17. Text Input

**What Dija needs:**
- `NSTextInputClient` protocol for input method support (IME)
- Marked text (inline composition) rendering
- Text selection with platform-standard keyboard shortcuts
- Spelling/grammar check integration (red underline)
- Autocorrect panel coordination
- Services menu support (text-based system services)

## Lower Priority (P3 -- nice-to-have)

### 18. Handoff / Continuity

Universal Clipboard, Handoff activity advertising.

### 19. Notification Center Integration

`NSUserNotification` / `UNUserNotificationCenter` for system notifications.

### 20. AppleScript / Automation Support

`NSScriptCommand` for scriptability. Low priority for v1.

### 21. Quick Look / Preview

Thumbnail and preview generation for Quick Look.

### 22. Share Sheet

`NSSharingServicePicker` integration.

### 23. Undo Manager

`NSUndoManager` integration for system undo/redo.

## Summary Matrix

| Gap                      | Priority | Complexity | Required For    |
|--------------------------|----------|------------|-----------------|
| Vibrancy                 | P0       | High       | Native look     |
| Title bar integration    | P0       | Medium     | Native look     |
| Traffic lights           | P0       | Medium     | Window controls |
| System font (SF Pro)     | P0       | Medium     | Typography      |
| Native menus             | P0       | Medium     | App structure   |
| Cursor management        | P1       | Low        | Interactions    |
| Focus ring               | P1       | Low        | Accessibility   |
| Scroll bars              | P1       | Medium     | Scrolling       |
| Drag and drop            | P1       | High       | Interactions    |
| Sheets                   | P1       | Medium     | Dialogs         |
| Popovers                 | P1       | Medium     | Overlays        |
| Color scheme detection   | P2       | Low        | Theming         |
| Window management        | P2       | Medium     | Multi-window    |
| Toolbar                  | P2       | Medium     | Navigation      |
| Touch Bar                | P2       | Low        | Legacy          |
| Accessibility            | P2       | High       | Compliance      |
| Text input (IME)         | P2       | High       | Internationalization |
| Handoff                  | P3       | Low        | Ecosystem       |
| Notifications            | P3       | Low        | System integration |
| AppleScript              | P3       | Low        | Automation      |
| Quick Look               | P3       | Low        | File handling   |
| Share sheet              | P3       | Low        | Sharing         |
| Undo manager             | P3       | Low        | Editing         |
