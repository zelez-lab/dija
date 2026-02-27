# iOS — Stepper (UIStepper)

Source: UIStepper, SwiftUI Stepper

## Appearance

| Property | Value |
|----------|-------|
| Width | 94pt |
| Height | 32pt |
| Corner radius | 8pt |
| Corner curve | `.continuous` (superellipse) |
| Background | tertiarySystemFill (`#767680` @ 0.12 / @ 0.24) |
| Divider | 0.5pt vertical line, separator color, centered |

## Segments

The stepper has two segments: minus (-) on the left, plus (+) on the right.

| Property | Value |
|----------|-------|
| Segment width | 47pt each (94pt / 2) |
| Icon | SF Symbol `minus` / `plus` |
| Icon size | 17pt |
| Icon weight | Medium |
| Icon color | tintColor (systemBlue default) |
| Hit area | Each segment is 47 x 32pt (padded to 44pt minimum vertically) |

## States

| State | Effect |
|-------|--------|
| Normal | Standard appearance |
| Pressed (-) | Left segment background darkens (systemFill highlight) |
| Pressed (+) | Right segment background darkens (systemFill highlight) |
| Disabled | Alpha 0.3 on entire stepper |
| At minimum | Minus icon at alpha 0.3, non-interactive |
| At maximum | Plus icon at alpha 0.3, non-interactive |

## Behavior

| Property | Value |
|----------|-------|
| Tap | Increments/decrements by `stepValue` (default: 1) |
| Long press | Auto-repeat after ~0.5s hold, accelerating |
| Auto-repeat initial rate | ~0.5s between increments |
| Auto-repeat fast rate | ~0.1s between increments (after ~2s) |
| Wraps | Optional — wraps from max to min (default: false) |
| Continuous | Sends value events during interaction (default: true) |
| Haptic | Light impact on each increment |

## Value Configuration

| Property | Type | Default |
|----------|------|---------|
| `value` | Double | 0 |
| `minimumValue` | Double | 0 |
| `maximumValue` | Double | 100 |
| `stepValue` | Double | 1 |
| `wraps` | Bool | false |

## Animation

| Property | Value |
|----------|-------|
| Press highlight | Immediate (no transition) |
| Release | ~0.15s fade back |
| Value change | No animation on stepper itself (label updates are app-managed) |
| Reached limit | Bounce effect on icon (subtle) |

## Layout with Label

Steppers are typically paired with a label showing the current value:

```
┌────────────────────────────────────────────────┐
│ Quantity              2          [-] [+]        │
│ (label)           (value)      (stepper)       │
└────────────────────────────────────────────────┘
```

| Property | Value |
|----------|-------|
| Label font | SF Pro Regular, 17pt |
| Value font | SF Pro Regular, 17pt |
| Spacing (value to stepper) | 8pt |
| Common layout | In a table cell, label left-aligned, stepper right-aligned |

## SwiftUI Stepper

SwiftUI provides a more integrated Stepper with built-in label:

```swift
Stepper("Quantity: \(value)", value: $value, in: 0...10)
```

| Property | Value |
|----------|-------|
| Label | Left-aligned, SF Pro Regular, 17pt |
| Stepper control | Right-aligned |
| Row height | 44pt (matches table cell) |

## Custom Appearance

The stepper supports custom images for increment/decrement:

| Property | Description |
|----------|-------------|
| `setIncrementImage` | Custom image for plus button |
| `setDecrementImage` | Custom image for minus button |
| `setBackgroundImage` | Custom background per state |
| `setDividerImage` | Custom divider between segments |

## Accessibility

| Property | Value |
|----------|-------|
| Role | Stepper (adjustable) |
| VoiceOver | "[Label], [value], adjustable" |
| Increment/decrement | Swipe up/down |
| At limit | "Minimum value" / "Maximum value" announcement |
