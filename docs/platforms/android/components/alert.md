# Android — Dialog (Material Design 3)

Source: m3.material.io/components/dialogs/specs

M3 equivalent of iOS alert. Two types: basic dialog and full-screen dialog.

## Variants

| Variant | Usage | Dismissible |
|---------|-------|------------|
| Basic dialog | Confirmations, simple choices | Tap outside or cancel button |
| Full-screen dialog | Complex tasks (compose, edit) | Close/X button only |

## Basic Dialog Metrics

| Property | Value |
|----------|-------|
| Min width | 280dp |
| Max width | 560dp |
| Corner radius | 28dp (extra-large) |
| Surface | surfaceContainerHigh |
| Elevation | Level 3 (6dp) |
| Padding (all sides) | 24dp |
| Icon size (optional) | 24dp |
| Icon-to-headline gap | 16dp |
| Headline-to-body gap | 16dp |
| Body-to-actions gap | 24dp |
| Action button gap | 8dp |
| Headline font | Headline Small (Roboto Regular, 24sp) |
| Body font | Body Medium (Roboto Regular, 14sp) |
| Action font | Label Large (Roboto Medium, 14sp) |

## Colors

| Element | Light | Dark |
|---------|-------|------|
| Container | `#ECE6F0` (surfaceContainerHigh) | `#2B2930` |
| Icon | `#6750A4` (secondary) | `#D0BCFF` |
| Headline | `#1D1B20` (onSurface) | `#E6E0E9` |
| Body | `#49454F` (onSurfaceVariant) | `#CAC4D0` |
| Action buttons | `#6750A4` (primary) | `#D0BCFF` |
| Scrim | `#000000` @ 32% | `#000000` @ 32% |

## Action Buttons

- Right-aligned, horizontally laid out
- Text buttons (no container)
- Confirming action on the right, dismissive on the left
- Max 2 action buttons for basic dialog

| Action | Example | Color |
|--------|---------|-------|
| Confirming | "Accept", "Save", "OK" | primary |
| Dismissive | "Cancel", "Dismiss" | primary |

## Full-Screen Dialog

| Property | Value |
|----------|-------|
| Corner radius | 0dp (fills screen) |
| Surface | surface |
| Top bar height | 56dp |
| Close icon | 24dp, onSurface |
| Title font | Title Large (Roboto Regular, 22sp) |
| Content padding | 24dp |
| Action button | Text button in top bar, right side |

## States

| State | Effect |
|-------|--------|
| Entering | Fade in + scale up from 85%, Medium 2 (300ms), Emphasized decelerate |
| Exiting | Fade out, Short 4 (200ms), Standard accelerate |
| Scrim | Fades in/out with dialog |

## Layout

### Basic Dialog

```
+------------------------------------+
|  24dp padding                      |
|  [Icon] (optional, centered)       |
|  16dp gap                          |
|  Headline (centered if icon)       |
|  16dp gap                          |
|  Body text                         |
|  24dp gap                          |
|           [Cancel]  [Confirm]      |
|  24dp padding                      |
+------------------------------------+
        280-560dp width
        corner radius 28dp
```

### With Divider

For dialogs with scrollable content, a 1dp divider (outlineVariant)
separates the header and footer from the scrollable body.

## Comparison with iOS Alert

| Property | iOS Alert | M3 Dialog |
|----------|----------|-----------|
| Corner radius | 14dp (squircle) | 28dp (circular) |
| Background | Ultra thick material (blur) | surfaceContainerHigh (opaque) |
| Button layout | Stacked (vertical) | Horizontal (right-aligned) |
| Button style | Tinted text | Text buttons |
| Scrim | Dim + blur | Dim only (32%) |
| Max width | ~270dp | 560dp |
