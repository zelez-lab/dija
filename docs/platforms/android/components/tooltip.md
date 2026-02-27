# Android — Tooltip (Material Design 3)

Source: m3.material.io/components/tooltips/specs

## Variants

| Variant | Content | Duration | Interaction |
|---------|---------|----------|------------|
| Plain | Short text label | Short (1500ms) | Long-press or hover |
| Rich | Title, text, actions, link | Persistent until dismissed | Long-press or hover |

## Plain Tooltip

### Metrics

| Property | Value |
|----------|-------|
| Height | 24dp (single line, auto-height for wrap) |
| Max width | 200dp |
| Corner radius | 4dp (extra-small) |
| Horizontal padding | 8dp |
| Vertical padding | 4dp |
| Label font | Body Small (Roboto Regular, 12sp) |
| Caret (arrow) height | 5dp |
| Caret width | 8dp |
| Offset from anchor | 8dp |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#322F35` (inverseSurface) | `#E6E0E9` |
| Label | `#F5EFF7` (inverseOnSurface) | `#322F35` |

## Rich Tooltip

### Metrics

| Property | Value |
|----------|-------|
| Max width | 320dp |
| Min width | 180dp |
| Corner radius | 12dp (medium) |
| Padding | 16dp (all sides) |
| Subhead font | Title Small (Roboto Medium, 14sp) |
| Supporting text font | Body Medium (Roboto Regular, 14sp) |
| Action font | Label Large (Roboto Medium, 14sp) |
| Subhead-to-text gap | 4dp |
| Text-to-action gap | 16dp |
| Caret height | 5dp |
| Caret width | 8dp |
| Offset from anchor | 8dp |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainer) | `#2B2930` |
| Subhead | `#1D1B20` (onSurfaceVariant) | `#E6E0E9` |
| Supporting text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Action button | `#6750A4` (primary) | `#D0BCFF` |

## Caret (Arrow)

Optional triangular pointer connecting the tooltip to its anchor:

| Property | Value |
|----------|-------|
| Width | 8dp |
| Height | 5dp |
| Shape | Triangle / rounded triangle |
| Position | Centered on anchor, auto-adjusted to stay on screen |
| Color | Same as container |

Caret can point up, down, left, or right depending on tooltip position
relative to its anchor.

## Positioning

Tooltips auto-position relative to their anchor in 8dp increments:

| Preference | Description |
|-----------|------------|
| Below | Default placement |
| Above | When below would clip screen |
| Start/End | When vertical space is limited |

Margin from screen edges: 8dp minimum.

## Behavior

### Plain Tooltip

| Trigger | Duration |
|---------|----------|
| Long-press | Show after 500ms hold, auto-hide after 1500ms |
| Hover (desktop) | Show after 500ms hover, auto-hide after 1500ms |
| Focus (keyboard) | Show immediately, hide on blur |

### Rich Tooltip

| Trigger | Duration |
|---------|----------|
| Long-press | Persistent until tap elsewhere |
| Hover (desktop) | Persistent while hovering tooltip or anchor |
| Focus (keyboard) | Persistent until Escape or blur |

Rich tooltips can include:
- Subhead (optional)
- Supporting text (required)
- Action button (optional, max 1)
- Close icon (optional for persistent tooltips)

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Enter (fade in + scale) | Short 4 (200ms) | Emphasized decelerate |
| Exit (fade out) | Short 3 (150ms) | Standard accelerate |

Enter scales from 0.85 to 1.0 with simultaneous fade from 0 to 1.

## Layout

### Plain Tooltip

```
         +-------------------+
         | 8dp  Label  8dp  |  24dp height
         +-------------------+
               \/  caret 5dp
         +-----------+
         |  Anchor   |
         +-----------+
```

### Rich Tooltip

```
+-------------------------------+
|  16dp                         |
|  Subhead (Title Small)        |
|  4dp                          |
|  Supporting text (Body Med)   |
|  Supporting text line 2       |
|  16dp                         |
|            [Action]     16dp  |
+-------------------------------+
        180-320dp width
        12dp corner radius
```

## Comparison with iOS

iOS does not have a native tooltip component. Closest alternatives:
- `UIPopoverPresentationController` (iPad only)
- `UIMenuController` (deprecated)
- Custom popover views

| Property | M3 Plain Tooltip | M3 Rich Tooltip |
|----------|-----------------|-----------------|
| Corner radius | 4dp | 12dp |
| Background | inverseSurface | surfaceContainer |
| Max width | 200dp | 320dp |
| Caret | Optional | Optional |
| Actions | None | Up to 1 button |
