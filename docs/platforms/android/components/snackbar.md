# Android — Snackbar (Material Design 3)

Source: m3.material.io/components/snackbar/specs

## Variants

| Variant | Layout | Duration |
|---------|--------|----------|
| Single-line | Text only | 4-10 seconds |
| Single-line with action | Text + action button | 4-10 seconds |
| Two-line | Longer text | 4-10 seconds |
| Two-line with action | Longer text + action below | 4-10 seconds |

## Metrics

| Property | Value |
|----------|-------|
| Min height (single-line) | 48dp |
| Min height (two-line) | 68dp |
| Corner radius | 4dp (extra-small) |
| Elevation | Level 3 (6dp) |
| Surface | inverseSurface |
| Horizontal padding | 16dp |
| Vertical padding | 14dp (single-line) |
| Vertical padding (two-line) | 12dp top, 12dp bottom |
| Action button padding | 8dp from right edge |
| Close icon padding | 12dp from right edge |
| Message font | Body Medium (Roboto Regular, 14sp) |
| Action font | Label Large (Roboto Medium, 14sp) + inversePrimary |
| Max width | 600dp |
| Min width | (fills available width on mobile minus margins) |
| Margin from screen edges | 8dp (bottom), 8dp (left/right) on mobile |

## Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#322F35` (inverseSurface) | `#E6E0E9` |
| Message | `#F5EFF7` (inverseOnSurface) | `#322F35` |
| Action button | `#D0BCFF` (inversePrimary) | `#6750A4` |
| Close icon | `#F5EFF7` (inverseOnSurface) | `#322F35` |

The snackbar uses **inverse** color roles to contrast with the surface behind it.

## Action Button

- Text button style (no container)
- Right-aligned, vertically centered (single-line)
- Below message (two-line with longer action text)
- Color: inversePrimary

## Close Icon (Optional)

- 24dp icon (X)
- Shown when the snackbar action is important and shouldn't auto-dismiss
- Right-most element

## Positioning

| Context | Position |
|---------|----------|
| Default | Bottom of screen, centered horizontally |
| With FAB | Slides up above FAB |
| With bottom nav | Above navigation bar |
| Tablet/desktop | Bottom-left corner, 8dp margin |

## States

Snackbars are not interactive except for:
- Action button: standard text button states (hover/focus/pressed)
- Close icon: standard icon button states

## Duration

| Type | Duration |
|------|----------|
| Short | 4000ms |
| Default | 6000ms |
| Long | 10000ms |
| Indefinite | Until dismissed (requires close icon) |

Snackbars auto-dismiss after duration. Only one snackbar visible at a time.
New snackbar replaces current one.

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Enter (slide up + fade) | Medium 2 (300ms) | Emphasized decelerate |
| Exit (fade out) | Short 4 (200ms) | Standard accelerate |
| Queue replace | Exit current, then enter next |

## Layout

### Single-line

```
+---------------------------------------------+
|  16dp  Message text          [Action]  16dp  |
+---------------------------------------------+
                    48dp height
```

### Single-line with close icon

```
+------------------------------------------------------+
|  16dp  Message text       [Action]  [X]  12dp  16dp  |
+------------------------------------------------------+
```

### Two-line with action

```
+---------------------------------------------+
|  12dp                                        |
|  16dp  Message text line 1                   |
|        Message text line 2      [Action]     |
|  12dp                             8dp        |
+---------------------------------------------+
                    68dp min height
```

## Comparison with iOS

M3 snackbar has no direct iOS equivalent. Closest:
- iOS toast (third-party)
- iOS notification banner (system-level)

| Property | M3 Snackbar | iOS (no native equiv) |
|----------|------------|----------------------|
| Position | Bottom | Top (banners) |
| Background | inverseSurface (opaque) | Material blur |
| Corner radius | 4dp | 14dp (squircle) |
| Action button | Text, inversePrimary | Tinted text |
