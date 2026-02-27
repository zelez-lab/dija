# Windows — InfoBar

Source: WinUI 3 InfoBar control

## Appearance

An inline notification bar that appears within the app content area to inform users of status changes, errors, warnings, or informational messages. Does NOT block interaction.

### Container Metrics

| Property | Value |
|----------|-------|
| Min height | 40px |
| Padding | 12px horizontal, 8px vertical |
| Corner radius | 8px (layerCornerRadius) |
| Border | 1px (varies by severity) |
| Background | Varies by severity (see below) |
| Icon size | 20x20px |
| Icon-to-content gap | 12px |
| Close button size | 32x32px hit area, 16x16px icon |

## Structure

```
┌──────────────────────────────────────────────────┐
│ [🛈] Title  Message text              [Action] [X]│
└──────────────────────────────────────────────────┘
```

Multi-line variant:
```
┌──────────────────────────────────────────────────┐
│ [🛈] Title                                    [X] │
│      Message text that wraps to multiple lines    │
│                                        [Action]   │
└──────────────────────────────────────────────────┘
```

## Severity Colors

| Severity | Icon | Background (Light) | Background (Dark) | Border (Light) | Border (Dark) |
|----------|------|-------------------|-------------------|----------------|---------------|
| Informational | `i` circle | `#F6F6F6` | `#08FFFFFF` | `#0F000000` | `#15FFFFFF` |
| Success | Checkmark circle | `#DFF6DD` | `#393D1B` | `#0F000000` | `#15FFFFFF` |
| Warning | Exclamation triangle | `#FFF4CE` | `#433519` | `#0F000000` | `#15FFFFFF` |
| Error | X circle | `#FDE7E9` | `#442726` | `#0F000000` | `#15FFFFFF` |

### Severity Icon Colors

| Severity | Icon color (Light) | Icon color (Dark) |
|----------|-------------------|-------------------|
| Informational | TextFillColorSecondary | TextFillColorSecondary |
| Success | `#0F7B0F` | `#6CCB5F` |
| Warning | `#9D5D00` | `#FCE100` |
| Error | `#C42B1C` | `#FF99A4` |

## Typography

| Element | Font | Color |
|---------|------|-------|
| Title | 14px Body Strong, SemiBold (600) | TextFillColorPrimary |
| Message | 14px Body, Regular (400) | TextFillColorPrimary |
| Hyperlink (in message) | 14px, Regular | AccentTextFillColorPrimary |

## Close Button

| Property | Value |
|----------|-------|
| Icon | `&#xE711;` (X glyph) |
| Size | 32x32px hit area |
| Position | Top-right corner |
| Style | Subtle (transparent → hover fill) |
| Corner radius | 4px |

Close button uses subtle style states:

| State | Background |
|-------|-----------|
| Rest | Transparent |
| Hover | SubtleFillColorSecondary |
| Pressed | SubtleFillColorTertiary |

## Action Button

| Property | Value |
|----------|-------|
| Style | HyperlinkButton or DefaultButtonStyle |
| Height | 32px |
| Position | Right side (single-line) or bottom-right (multi-line) |
| Font | 14px, SemiBold |

## Custom Content

InfoBar supports custom content below the message text:

| Property | Value |
|----------|-------|
| Content area | Below message, full width minus icon/close areas |
| Padding | 0px additional (inherits container padding) |

## Layout Behavior

| Condition | Layout |
|-----------|--------|
| Short content (fits single line) | Horizontal: icon, title, message, action, close |
| Long content | Wraps: title on first line, message below, action below message |
| Very long message | Message text wraps freely |
| Width < 500px | Stacks to multi-line layout |

## Position

InfoBar is placed inline in the content area. Common placements:

| Position | Description |
|----------|------------|
| Top of page | Directly below header/navigation |
| Above content area | Pushes content down |
| Bottom of page | Above status bar or footer |

InfoBar takes up space in the layout and pushes sibling elements. It is NOT a floating overlay.

## IsClosable

When `IsClosable = false`:
- Close button is hidden
- InfoBar remains visible until programmatically removed
- Used for persistent status messages

## IsIconVisible

When `IsIconVisible = false`:
- Severity icon is hidden
- Content shifts left to fill the space
- Background and border still reflect severity

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| InfoBar appear (expand height + fade) | 300ms | Decelerate |
| InfoBar close (collapse height + fade) | 200ms | Accelerate |
| Content reflow (after close) | 200ms | Decelerate |

The appear animation: starts at 0 height and 0 opacity, expands to full height while fading in. The close animation reverses this: collapses height while fading out, and surrounding content smoothly fills the space.
