# Android — Search Bar (Material Design 3)

Source: m3.material.io/components/search/specs

## Variants

| Variant | State | Description |
|---------|-------|------------|
| Search bar (docked) | Resting | Persistent bar in the layout |
| Search view (expanded) | Active | Full-width/full-screen search with suggestions |

## Search Bar (Docked) Metrics

| Property | Value |
|----------|-------|
| Height | 56dp |
| Corner radius | 28dp (full pill) |
| Surface | surfaceContainerHigh |
| Elevation | Level 2 (3dp) |
| Horizontal padding | 16dp |
| Leading icon size | 24dp |
| Trailing icon size | 24dp |
| Leading icon to text gap | 16dp |
| Text to trailing icon gap | 16dp |
| Placeholder font | Body Large (Roboto Regular, 16sp) |
| Input font | Body Large (Roboto Regular, 16sp) |

## Search View (Expanded) Metrics

| Property | Value |
|----------|-------|
| Height (header) | 72dp |
| Corner radius | 0dp (full width) or 28dp (overlay) |
| Surface | surfaceContainerHigh |
| Elevation | Level 2 (3dp) |
| Back icon size | 24dp |
| Clear icon size | 24dp |
| Input font | Body Large (Roboto Regular, 16sp) |
| Suggestion item height | 56dp |
| Suggestion icon size | 24dp |
| Suggestion font | Body Large (Roboto Regular, 16sp) |
| Divider | 1dp, outlineVariant |

## Colors

### Search Bar

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainerHigh) | `#2B2930` |
| Leading icon | `#49454F` (onSurface) | `#E6E0E9` |
| Placeholder text | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Input text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Trailing icon (avatar/action) | `#49454F` (onSurfaceVariant) | `#CAC4D0` |

### Search View

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainerHigh) | `#2B2930` |
| Back icon | `#1D1B20` (onSurface) | `#E6E0E9` |
| Input text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Clear icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Suggestion text | `#1D1B20` (onSurface) | `#E6E0E9` |
| Suggestion icon | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Divider | `#CAC4D0` (outlineVariant) | `#49454F` |

## States

### Search Bar States

| State | Effect |
|-------|--------|
| Resting | Default styling |
| Hovered | State layer 8% (onSurface) |
| Focused | Transitions to search view (expanded) |
| Pressed | Transitions to search view |

### Search View States

| State | Effect |
|-------|--------|
| Active | Input focused, keyboard visible |
| With results | Suggestion list below input |
| Empty | No suggestions, optional empty state |

## Transition Animation

Search bar to search view:

| Property | Duration | Easing |
|----------|----------|--------|
| Container morph | Medium 3 (350ms) | Emphasized decelerate |
| Corner radius (28dp -> 0dp) | Medium 2 (300ms) | Standard |
| Content cross-fade | Short 4 (200ms) | Standard |
| Suggestion list enter | Medium 1 (250ms) | Emphasized decelerate |

Search view to search bar (dismiss):

| Property | Duration | Easing |
|----------|----------|--------|
| Container morph | Medium 2 (300ms) | Standard accelerate |
| Corner radius (0dp -> 28dp) | Medium 2 (300ms) | Standard |
| Content cross-fade | Short 3 (150ms) | Standard |

## Layout

### Search Bar (Resting)

```
+-----------------------------------------------------------+
|  16dp  [Search icon]  16dp  "Search..."   [Avatar]  16dp  |
+-----------------------------------------------------------+
                        56dp height
                      28dp corner radius
```

### Search View (Expanded)

```
+-----------------------------------------------------------+
|  [<- Back]  16dp  "query text..."  [X Clear]              |
+-----------------------------------------------------------+  72dp header
|  -------divider (1dp)-------                              |
|  [Clock icon]  16dp  Recent search 1                      |  56dp
|  [Clock icon]  16dp  Recent search 2                      |  56dp
|  [Search icon] 16dp  Suggestion 1                         |  56dp
|  [Search icon] 16dp  Suggestion 2                         |  56dp
+-----------------------------------------------------------+
```

## Comparison with iOS

| Property | iOS Search Bar | M3 Search Bar |
|----------|---------------|--------------|
| Corner radius | 10dp (squircle) | 28dp (pill) |
| Background | systemGray6 | surfaceContainerHigh |
| Height | 36dp | 56dp |
| Cancel button | Text, right side | Back arrow, left side |
| Clear button | Circle X in field | X icon, right side |
| Scope bar | Segmented control below | Not standard |
