# macOS Sheet (NSPanel Sheet Presentation)

Reference: NSPanel, NSWindow.beginSheet, Apple HIG (macOS 14+).

## Overview

A sheet is a modal dialog attached to a specific window. It slides down from the title bar area and blocks interaction with the parent window. Sheets are macOS-specific -- other platforms use full-screen modals or bottom sheets instead.

## Presentation

### Attachment Point

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

### Animation

| Phase                  | Duration (ms) | Curve          |
|-----------------------|---------------|----------------|
| Presentation (drop)    | 250           | Ease In Out    |
| Dismissal (retract)    | 200           | Ease In Out    |
| Parent window dimming  | 200           | Ease In Out    |
| Content fade-in        | 200           | Ease Out       |

The sheet drops down with a slight vertical overshoot (very subtle spring), then settles.

## Metrics

### Sizing

| Property                  | Value                   | Notes                        |
|---------------------------|-------------------------|------------------------------|
| Width                      | Parent window width - 40 (max) | Centered horizontally   |
| Minimum width              | 300 pt                  |                              |
| Maximum width              | Parent window width     | Cannot exceed parent          |
| Minimum height             | 100 pt                  |                              |
| Maximum height             | Parent window height - 44 | Leave room for title bar     |
| Corner radius              | 10 pt                   | Bottom corners only           |
| Top corners                | 0 pt (attached to title bar) | Attached flush             |

### Content Layout

| Property                  | Value (pt) |
|---------------------------|------------|
| Content padding (top)      | 20         |
| Content padding (sides)    | 20         |
| Content padding (bottom)   | 20         |

### Button Area

| Property                  | Value (pt) |
|---------------------------|------------|
| Button area margin top     | 16         |
| Button height              | 22         |
| Button min width           | 68         |
| Button spacing             | 8          |
| Button alignment           | Right-aligned |

## Parent Window Behavior

When a sheet is presented:

| Behavior                    | Description                                  |
|-----------------------------|----------------------------------------------|
| Parent interaction          | Blocked                                      |
| Parent window move          | Still movable (sheet moves with it)           |
| Parent window resize        | Depends on configuration                     |
| Parent dimming              | Subtle darkening of content area              |
| Parent title bar            | Still visible, traffic lights still work       |
| Close button (red)          | May dismiss sheet or close window (configurable) |

### Parent Dimming

| Property                  | Value                    |
|---------------------------|--------------------------|
| Overlay color (light)      | `rgba(0,0,0,0.08)`     |
| Overlay color (dark)       | `rgba(0,0,0,0.15)`     |
| Covers                     | Content area only (not title bar) |

## Colors

### Background

| Mode      | Value                                          |
|-----------|------------------------------------------------|
| Light     | `#ECECEC` (windowBackgroundColor)              |
| Dark      | `#323232` (windowBackgroundColor)              |

Sheets can also use vibrancy if desired (`.sheet` material).

### Shadow

The sheet does not have its own shadow in the traditional sense since it is attached to the window. However, a subtle drop shadow separates it from the dimmed content below:

```
Color:   rgba(0, 0, 0, 0.15)
Offset:  (0, 4) pt
Blur:    16 pt
```

## Common Sheet Types

### Save/Open Sheet (NSSavePanel / NSOpenPanel)

| Property                  | Value              |
|---------------------------|--------------------|
| Width                      | ~480 pt (standard) |
| File browser height        | ~320 pt            |
| Sidebar width              | ~160 pt            |

### Print Sheet (NSPrintPanel)

| Property                  | Value              |
|---------------------------|--------------------|
| Width                      | ~640 pt            |
| Height                     | Varies with options |

### Custom Sheet

For custom content, use `NSWindow.beginSheet(_:completionHandler:)`.

## Multiple Sheets

macOS supports stacking multiple sheets on a single window:
- Each subsequent sheet slides over the previous one
- Previous sheets compress upward (accordion effect)
- The topmost sheet is the only interactive one
- Dismissing the top sheet reveals the one beneath

### Stacking Animation

| Phase              | Duration (ms) | Curve          |
|-------------------|---------------|----------------|
| Push (new sheet)   | 250           | Ease In Out    |
| Previous compress  | 250           | Ease In Out    |
| Pop (dismiss top)  | 200           | Ease In Out    |
| Previous expand    | 200           | Ease In Out    |

## Typography

| Element              | Font Size (pt) | Weight     | Color               |
|----------------------|----------------|------------|----------------------|
| Sheet title          | 13             | Bold       | labelColor           |
| Sheet body text      | 13             | Regular    | labelColor           |
| Sheet secondary text | 11             | Regular    | secondaryLabelColor  |

## Keyboard Interaction

| Key              | Action                                    |
|-----------------|-------------------------------------------|
| Return / Enter  | Activate default button                    |
| Escape / Cmd+.  | Activate cancel button (dismiss sheet)     |
| Tab             | Navigate between controls                  |

## Accessibility

| Property     | Value                                     |
|-------------|-------------------------------------------|
| Role         | `.sheet`                                  |
| Relation     | Child of parent window                     |
| Focus        | Trapped within sheet (modal)               |
| Announced    | Sheet title + content on presentation      |

## Dija Skin Mapping

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
