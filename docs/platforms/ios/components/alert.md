# iOS — Alert (UIAlertController, style: .alert)

Source: UIAlertController, SwiftUI Alert

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | Ultra-thick material | Ultra-thick material |
| Corner radius | 14pt | 14pt |
| Corner curve | `.continuous` (superellipse) | |
| Width | 270pt (fixed on iPhone) | 270pt |
| Width (iPad) | 270pt (centered in screen) | 270pt |
| Shadow | offset(0, 10) blur 40, black @ 0.3 | offset(0, 10) blur 40, black @ 0.4 |

## Dimming Backdrop

| Property | Value |
|----------|-------|
| Overlay | black @ 0.4 |
| Animation | Fade in 0.2s, fade out 0.15s |
| Background interaction | Blocked (modal) |

## Layout

| Region | Value |
|--------|-------|
| Content padding (top) | 20pt |
| Content padding (horizontal) | 16pt |
| Title-to-message spacing | 3pt |
| Message-to-buttons spacing | 20pt |
| Content-to-text-field spacing | 8pt |
| Text field height | 26pt |
| Text field corner radius | 5pt |
| Text field border | 0.5pt separator color |

## Typography

| Element | Font | Size | Weight | Color | Alignment |
|---------|------|------|--------|-------|-----------|
| Title | SF Pro | 17pt | Semibold | label | Centered |
| Message | SF Pro | 13pt | Regular | secondaryLabel | Centered |
| Default action | SF Pro | 17pt | Semibold | tintColor | Centered |
| Cancel action | SF Pro | 17pt | Semibold | tintColor | Centered |
| Regular action | SF Pro | 17pt | Regular | tintColor | Centered |
| Destructive action | SF Pro | 17pt | Regular | systemRed | Centered |
| Preferred action | SF Pro | 17pt | Semibold | tintColor | Centered (bold emphasis) |

## Button Layout

### 2 Buttons (Side by Side)

```
┌─────────────────────────────┐
│         Alert Title          │
│     This is the message      │
├──────────────┬──────────────┤
│    Cancel    │     OK       │  ← 44pt height each
└──────────────┴──────────────┘
```

| Property | Value |
|----------|-------|
| Button height | 44pt |
| Separator (horizontal) | 0.33pt, separator color |
| Separator (vertical) | 0.33pt, separator color |
| Layout | Left: cancel, Right: default/preferred |

### 3+ Buttons (Stacked)

```
┌─────────────────────────────┐
│         Alert Title          │
│     This is the message      │
├─────────────────────────────┤
│          Action 1            │
├─────────────────────────────┤
│          Action 2            │
├─────────────────────────────┤
│          Cancel              │  ← always last
└─────────────────────────────┘
```

| Property | Value |
|----------|-------|
| Each button | 44pt height, full width |
| Separator | 0.33pt horizontal between each |
| Cancel | Always last (bottom) |

## Button States

| State | Effect |
|-------|--------|
| Pressed | Background darkens slightly (gray highlight fill) |
| Disabled | Text alpha 0.3 |

## Text Fields in Alert

Alerts can contain 1–2 text fields (e.g., login prompt).

| Property | Value |
|----------|-------|
| Max text fields | 2 (username + password) |
| Position | Between message and buttons |
| Background | white (light) / `#1C1C1E` (dark) |
| Border | 0.5pt separator color |
| Corner radius | 5pt |
| Height | 26pt |
| Font | SF Pro Regular, 13pt |
| Horizontal padding | 8pt |

## Animation

### Present

| Property | Value |
|----------|-------|
| Duration | 0.25s |
| Scale | Start at 1.2, spring to 1.0 |
| Opacity | Fade in from 0 to 1 |
| Backdrop | Fade in black @ 0.4 |
| Spring damping | ~0.75 |

### Dismiss

| Property | Value |
|----------|-------|
| Duration | 0.2s |
| Scale | From 1.0 to 0.9 |
| Opacity | Fade out from 1 to 0 |
| Backdrop | Fade out |
| Curve | ease-in |

## Accessibility

| Property | Value |
|----------|-------|
| VoiceOver | "Alert, [title], [message]" |
| Focus | First action button (or preferred action) |
| Escape gesture | Triggers cancel action |
