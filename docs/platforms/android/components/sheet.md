# Android — Bottom Sheet (Material Design 3)

Source: m3.material.io/components/bottom-sheets/specs

## Variants

| Variant | Behavior | Scrim |
|---------|----------|-------|
| Standard | Coexists with main content, non-blocking | No |
| Modal | Blocks main content, requires dismissal | Yes (32%) |

## Metrics

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

## Drag Handle

Optional drag handle at the top for swipe affordance:

| Property | Value |
|----------|-------|
| Width | 32dp |
| Height | 4dp |
| Corner radius | 2dp (full pill) |
| Color | onSurfaceVariant @ 40% |
| Top margin | 22dp (center of 48dp touch target) |
| Touch target | 48dp x 48dp |

## Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#F7F2FA` (surfaceContainerLow) | `#1D1B20` |
| Drag handle | `#49454F` @ 40% | `#CAC4D0` @ 40% |
| Scrim (modal) | `#000000` @ 32% | `#000000` @ 32% |

## Sheet States

| State | Corner radius | Description |
|-------|---------------|-------------|
| Hidden | 28dp | Sheet below screen |
| Collapsed (peek) | 28dp | Partially visible, shows peek content |
| Half-expanded | 28dp | Midpoint, optional detent |
| Expanded | 28dp -> 0dp | Full height, corners may animate to 0dp |

When fully expanded to screen height, corners animate from 28dp to 0dp
to visually merge with the screen edge.

## Standard Bottom Sheet

- Sits alongside main content
- Can be swiped between collapsed and expanded
- Does not dim background
- Does not block interaction with main content

## Modal Bottom Sheet

- Overlays main content with scrim
- Tap scrim or swipe down to dismiss
- Blocks interaction with content behind
- Uses higher elevation (Level 1)

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Show (slide up) | Medium 3 (350ms) | Emphasized decelerate |
| Hide (slide down) | Medium 2 (300ms) | Standard accelerate |
| Snap to detent | Medium 1 (250ms) | Standard |
| Corner radius (expand) | Medium 2 (300ms) | Standard |
| Scrim fade in | Medium 2 (300ms) | Standard |
| Scrim fade out | Short 4 (200ms) | Standard accelerate |

## Swipe Behavior

- Swipe velocity threshold: 500dp/s (fast fling dismisses)
- Position threshold: 50% of remaining distance to next detent
- Overscroll: elastic resistance at bounds

## Layout

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

## Comparison with iOS Sheet

| Property | iOS Sheet | M3 Bottom Sheet |
|----------|----------|----------------|
| Corner radius | 10dp (squircle) | 28dp (circular) |
| Background | System material (blur) | surfaceContainerLow (opaque) |
| Drag indicator | 36x5dp, gray pill | 32x4dp pill |
| Detents | medium, large, custom | collapsed, half, expanded |
| Scrim | Dim | Dim (32%, no blur) |
