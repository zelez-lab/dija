# Stepper

A control for incrementing or decrementing a numeric value in discrete steps.

| Platform | Native Component | Status |
|---|---|---|
| iOS | UIStepper | Documented |
| macOS | NSStepper | Documented |
| Android | — | No native equivalent |
| Windows | NumberBox | Documented |
| Linux | GtkSpinButton / AdwSpinRow | Documented |

## iOS

Source: UIStepper, SwiftUI Stepper

### Appearance

| Property | Value |
|----------|-------|
| Width | 94pt |
| Height | 32pt |
| Corner radius | 8pt |
| Corner curve | `.continuous` (superellipse) |
| Background | tertiarySystemFill (`#767680` @ 0.12 / @ 0.24) |
| Divider | 0.5pt vertical line, separator color, centered |

### Segments

The stepper has two segments: minus (-) on the left, plus (+) on the right.

| Property | Value |
|----------|-------|
| Segment width | 47pt each (94pt / 2) |
| Icon | SF Symbol `minus` / `plus` |
| Icon size | 17pt |
| Icon weight | Medium |
| Icon color | tintColor (systemBlue default) |
| Hit area | Each segment is 47 x 32pt (padded to 44pt minimum vertically) |

### States

| State | Effect |
|-------|--------|
| Normal | Standard appearance |
| Pressed (-) | Left segment background darkens (systemFill highlight) |
| Pressed (+) | Right segment background darkens (systemFill highlight) |
| Disabled | Alpha 0.3 on entire stepper |
| At minimum | Minus icon at alpha 0.3, non-interactive |
| At maximum | Plus icon at alpha 0.3, non-interactive |

### Behavior

| Property | Value |
|----------|-------|
| Tap | Increments/decrements by `stepValue` (default: 1) |
| Long press | Auto-repeat after ~0.5s hold, accelerating |
| Auto-repeat initial rate | ~0.5s between increments |
| Auto-repeat fast rate | ~0.1s between increments (after ~2s) |
| Wraps | Optional — wraps from max to min (default: false) |
| Continuous | Sends value events during interaction (default: true) |
| Haptic | Light impact on each increment |

### Value Configuration

| Property | Type | Default |
|----------|------|---------|
| `value` | Double | 0 |
| `minimumValue` | Double | 0 |
| `maximumValue` | Double | 100 |
| `stepValue` | Double | 1 |
| `wraps` | Bool | false |

### Animation

| Property | Value |
|----------|-------|
| Press highlight | Immediate (no transition) |
| Release | ~0.15s fade back |
| Value change | No animation on stepper itself (label updates are app-managed) |
| Reached limit | Bounce effect on icon (subtle) |

### Layout with Label

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

### SwiftUI Stepper

SwiftUI provides a more integrated Stepper with built-in label:

```swift
Stepper("Quantity: \(value)", value: $value, in: 0...10)
```

| Property | Value |
|----------|-------|
| Label | Left-aligned, SF Pro Regular, 17pt |
| Stepper control | Right-aligned |
| Row height | 44pt (matches table cell) |

### Custom Appearance

The stepper supports custom images for increment/decrement:

| Property | Description |
|----------|-------------|
| `setIncrementImage` | Custom image for plus button |
| `setDecrementImage` | Custom image for minus button |
| `setBackgroundImage` | Custom background per state |
| `setDividerImage` | Custom divider between segments |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Stepper (adjustable) |
| VoiceOver | "[Label], [value], adjustable" |
| Increment/decrement | Swipe up/down |
| At limit | "Minimum value" / "Maximum value" announcement |

## macOS

Source: NSStepper (AppKit), SwiftUI Stepper

### Overview

NSStepper is a small control with vertically stacked up/down arrow buttons for incrementing or decrementing a numeric value. Unlike the iOS stepper (horizontal +/- segments), macOS uses a compact vertical arrow layout. The stepper is always paired with a separate text field or label — it has no built-in value display.

### Anatomy

```
┌───┐
│ ▲ │  ← up arrow (increment)
├───┤
│ ▼ │  ← down arrow (decrement)
└───┘
```

The control consists of two stacked buttons sharing a single bezel. A thin divider separates the up and down regions.

### Metrics

NSStepper supports three control sizes via `controlSize`:

| Control Size | Width | Height | Arrow icon size |
|-------------|-------|--------|-----------------|
| Regular | 19pt | 27pt | ~9pt |
| Small | 15pt | 21pt | ~7pt |
| Mini | 13pt | 16pt | ~5pt |

| Property | Value |
|----------|-------|
| Corner radius | 4pt (Aqua bezel) |
| Background | Standard button bezel (system-managed gradient) |
| Arrows | System-drawn chevrons, textColor |
| Divider | 1pt horizontal line at center, separator color |

### States

| State | Effect |
|-------|--------|
| Normal | Standard bezel appearance |
| Hover (up) | Upper half highlights (subtle bezel change) |
| Hover (down) | Lower half highlights (subtle bezel change) |
| Pressed (up) | Upper half darkens, pressed bezel |
| Pressed (down) | Lower half darkens, pressed bezel |
| Disabled | Entire control dimmed (alpha ~0.35), non-interactive |
| At minimum | Down arrow dimmed (alpha ~0.35), non-interactive |
| At maximum | Up arrow dimmed (alpha ~0.35), non-interactive |
| Focused | Focus ring (2pt blue outline with 1pt offset) |

### Behavior

| Property | Value |
|----------|-------|
| Click | Increments/decrements by `increment` (default: 1) |
| Auto-repeat | When `autorepeat` is true: first click fires once, then after 0.5s hold, repeats at ~10 times/second |
| Value wrapping | When `valueWraps` is true, exceeding max wraps to min and vice versa |
| Continuous | Sends value-changed action during interaction (default: true) |

### Value Configuration

| Property | Type | Default |
|----------|------|---------|
| `doubleValue` | Double | 0 |
| `minValue` | Double | 0 |
| `maxValue` | Double | 59 |
| `increment` | Double | 1 |
| `autorepeat` | Bool | true |
| `valueWraps` | Bool | false |

### Layout with Text Field

NSStepper is typically paired with an NSTextField to display and edit the value:

```
┌─────────────┐ ┌───┐
│     42      │ │ ▲ │
│             │ ├───┤
│             │ │ ▼ │
└─────────────┘ └───┘
  (text field)   (stepper)
```

| Property | Value |
|----------|-------|
| Text field font | System font, 13pt (regular control size) |
| Gap (text field to stepper) | 0–2pt (typically flush or near-flush) |
| Vertical alignment | Stepper center-aligned to text field |
| Common context | Form fields, date pickers, preferences |

### SwiftUI Stepper

SwiftUI on macOS renders a Stepper that adapts to the platform style:

```swift
Stepper("Quantity: \(value)", value: $value, in: 0...100)
```

| Property | Value |
|----------|-------|
| Label | Left-aligned, system font 13pt |
| Stepper control | Right-aligned, NSStepper appearance |
| Row height | ~22pt (compact macOS forms) |

### Accessibility

| Property | Value |
|----------|-------|
| Role | Incrementor (NSAccessibilityIncrementorRole) |
| VoiceOver | "[Label], [value], stepper" |
| Actions | Increment, Decrement |
| At limit | Value does not change; no explicit announcement |
| Keyboard | Arrow Up/Down when focused |

## Android

No native stepper equivalent. Android's Material Design does not define a stepper/increment-decrement control. Numeric input is typically handled by `TextInputEditText` with `inputType="number"`, or custom quantity selectors in e-commerce apps.

Dija renders as a horizontal +/- control following Material 3 styling conventions:

| Property | Value |
|----------|-------|
| Height | 40dp |
| Button size | 40x40dp (circular or rounded-square) |
| Value display width | 48dp minimum |
| Corner radius | 8dp (M3 small) |
| Button icon | `remove` / `add` Material Symbols, 24dp |
| Icon color | onSurfaceVariant |
| Button background | Outlined (1dp border, outline color) |
| Value font | Body Large (Roboto 400, 16sp) |
| Value color | onSurface |
| Gap (button to value) | 0dp (joined) or 8dp (separated) |
| Touch target | 48dp minimum |

### States

| State | Effect |
|-------|--------|
| Enabled | Standard appearance |
| Pressed | State layer 10% (onSurface) + ripple |
| Disabled | Container onSurface @ 12%, content onSurface @ 38% |
| At minimum | Minus button disabled appearance |
| At maximum | Plus button disabled appearance |

## Windows

Source: WinUI 3 NumberBox (Microsoft.UI.Xaml.Controls)

### Overview

Windows uses NumberBox — a text input field with optional spin buttons for incrementing/decrementing. Unlike iOS/macOS steppers that are pure button controls, NumberBox combines a text field with spinner buttons, supporting direct numeric entry, expression evaluation, and formatted display.

### Anatomy

NumberBox has two spin button placement modes:

**Inline mode** — spin buttons appear as up/down arrows beside the text field:

```
┌──────────────────┬───┬───┐
│       42         │ ▼ │ ▲ │
└──────────────────┴───┴───┘
   (text input)     (spin buttons)
```

**Compact mode** — spin buttons appear as a floating flyout when the control is focused:

```
             ┌───┐
             │ ▲ │  (flyout, shown on focus)
┌────────────┼───┤
│     42     │ ↕ │  (collapse indicator)
└────────────┼───┤
             │ ▼ │
             └───┘
```

### Metrics

| Property | Value |
|----------|-------|
| Height | 32px (default) |
| Height (compact density) | 24px |
| Min width | 0px (no inherent minimum) |
| Corner radius | 4px (controlCornerRadius) |
| Padding | 11px horizontal, 5px top, 6px bottom |
| Font | Segoe UI Variable, 14px |
| Spin button width | 32px each (inline mode) |
| Spin button icon | ChevronUp / ChevronDown, 12px |
| Border | 1px ControlStrokeColorDefault + bottom ControlStrokeColorSecondary |

### Colors

| Element | Light | Dark |
|---------|-------|------|
| Background | ControlFillColorDefault (`#B3FFFFFF`) | ControlFillColorDefault (`#0FFFFFFF`) |
| Text | TextFillColorPrimary | TextFillColorPrimary |
| Border (top/sides) | ControlStrokeColorDefault (`#0F000000`) | ControlStrokeColorDefault (`#12FFFFFF`) |
| Border (bottom) | ControlStrokeColorSecondary (`#29000000`) | ControlStrokeColorSecondary (`#18FFFFFF`) |
| Spin button icon | TextFillColorSecondary | TextFillColorSecondary |
| Header text | TextFillColorPrimary | TextFillColorPrimary |
| Placeholder text | TextFillColorSecondary | TextFillColorSecondary |

### States

| State | Background | Border | Text |
|-------|-----------|--------|------|
| Rest | ControlFillColorDefault | ControlStrokeColorDefault | TextFillColorPrimary |
| Hover | ControlFillColorSecondary | ControlStrokeColorDefault | TextFillColorPrimary |
| Focused | ControlFillColorInputActive | AccentFillColorDefault (2px bottom) | TextFillColorPrimary |
| Disabled | ControlFillColorDisabled | ControlStrokeColorDefault (reduced) | TextFillColorDisabled |

Spin button states (inline):

| State | Effect |
|-------|--------|
| Rest | Transparent background, icon in TextFillColorSecondary |
| Hover | SubtleFillColorSecondary background |
| Pressed | SubtleFillColorTertiary background |
| Disabled | Icon in TextFillColorDisabled, non-interactive |
| At minimum | Down button disabled |
| At maximum | Up button disabled |

### Behavior

| Property | Value |
|----------|-------|
| Click (spin button) | Increments/decrements by `SmallChange` |
| Arrow Up/Down keys | Increments/decrements by `SmallChange` |
| PageUp/PageDown keys | Increments/decrements by `LargeChange` |
| Scroll wheel | Increments/decrements by `SmallChange` (when focused) |
| Direct text entry | User types a numeric value directly |
| Expression evaluation | When `AcceptsExpression` is true, supports +, -, *, /, ^ with standard order of operations |
| Validation | On Enter key or loss of focus; invalid input behavior controlled by `ValidationMode` |
| Number formatting | Controlled by `NumberFormatter` (decimal, currency, percent, significant figures) |

### Value Configuration

| Property | Type | Default |
|----------|------|---------|
| `Value` | Double | NaN |
| `Minimum` | Double | -Infinity |
| `Maximum` | Double | Infinity |
| `SmallChange` | Double | 1 |
| `LargeChange` | Double | 10 |
| `SpinButtonPlacementMode` | Enum | Hidden |
| `AcceptsExpression` | Bool | false |
| `ValidationMode` | Enum | InvalidInputOverwritten |
| `Header` | Object | null |
| `PlaceholderText` | String | "" |
| `NumberFormatter` | INumberFormatter2 | null |
| `IsWrapEnabled` | Bool | false |

### SpinButtonPlacementMode

| Value | Description |
|-------|-------------|
| Hidden | No spin buttons (default) |
| Compact | Small collapse indicator; up/down buttons appear as flyout on focus |
| Inline | Up/down buttons rendered beside the text field |

### ValidationMode

| Value | Description |
|-------|-------------|
| InvalidInputOverwritten | Invalid input reverts to last valid value (default) |
| Disabled | No built-in validation; app handles validation |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Rest to Hover (fill) | 100ms | Control fast |
| Focus bottom accent bar | 100ms | Control fast |
| Compact flyout appear | 150ms | Decelerate |
| Compact flyout dismiss | 100ms | Accelerate |

### Accessibility

| Property | Value |
|----------|-------|
| AutomationPeer | NumberBoxAutomationPeer |
| Control type | Spinner |
| Input scope | Number (digits 0-9) |
| Live region | Polite (value changes announced) |
| Spin buttons | Labeled "Increase" / "Decrease" |

## Linux

Source: GtkSpinButton (GTK 4), AdwSpinRow (libadwaita 1.4+)

### Overview

Linux offers two stepper controls: **GtkSpinButton** — a standalone text entry with +/- buttons — and **AdwSpinRow** — an Adwaita list row variant embedding a GtkSpinButton. Both use GtkAdjustment for value bounds and stepping.

### GtkSpinButton

#### Anatomy

GtkSpinButton has two orientations:

**Horizontal (default):**

```
┌──────────────┬───┬───┐
│      42      │ - │ + │
└──────────────┴───┴───┘
  (text entry)   (buttons)
```

**Vertical:**

```
    ┌───┐
    │ + │
┌───┼───┤
│   42  │
└───┼───┤
    │ - │
    └───┘
```

#### CSS Nodes

```
spinbutton[.horizontal|.vertical]
├── text
├── button.up
└── button.down
```

The orientation is reflected as `.horizontal` or `.vertical` style class on the main `spinbutton` node.

#### Metrics

| Property | Value |
|----------|-------|
| Min height | 34px |
| Button width | ~34px each |
| Corner radius | 6px |
| Horizontal padding (entry) | 8px |
| Font | Adwaita Sans Regular, 15px |
| Border | 1px, `rgba(0,0,0,0.15)` (light) / `rgba(255,255,255,0.15)` (dark) |
| Shadow | (0,1) blur 2, black @ 0.07 |

#### Colors

| Element | Light | Dark |
|---------|-------|------|
| Entry background | `#FFFFFF` | `#404040` |
| Entry text | `#2E3436` (label color) | `#FFFFFF` |
| Button background | `#FFFFFF` | `#404040` |
| Button icon | `#2E3436` | `#FFFFFF` |
| Border | `rgba(0,0,0,0.15)` | `rgba(255,255,255,0.15)` |

#### States

| State | Effect |
|-------|--------|
| Normal | Standard bezel, entry editable |
| Hover (button) | Button background lightens/darkens |
| Pressed (button) | Button background inverts (inset shadow) |
| Focused | 2px accent outline (`#3584E4`) around entire control |
| Disabled | Opacity 0.5, non-interactive |
| At minimum | Down/minus button insensitive (dimmed) |
| At maximum | Up/plus button insensitive (dimmed) |

#### Behavior

| Property | Value |
|----------|-------|
| Click (button) | Increments/decrements by `step_increment` |
| Long press | Auto-repeat, accelerating with `climb_rate` |
| Arrow Up/Down keys | Increments/decrements by `step_increment` |
| PageUp/PageDown keys | Increments/decrements by `page_increment` |
| Direct text entry | User types value; validated on focus-out or Enter |
| Wrapping | When `wrap` is true, exceeding upper wraps to lower and vice versa |
| Snap to ticks | When `snap_to_ticks` is true, values snap to nearest step increment |
| Numeric only | When `numeric` is true, non-numeric characters are rejected |
| Update policy | `Always` (update on any change) or `IfValid` (update only on valid input) |

#### Value Configuration (GtkAdjustment)

| Property | Type | Default |
|----------|------|---------|
| `value` | Double | 0 |
| `lower` | Double | 0 |
| `upper` | Double | 100 |
| `step_increment` | Double | 1 |
| `page_increment` | Double | 10 |
| `climb_rate` | Double | 0 |
| `digits` | UInt | 0 (integer display) |
| `numeric` | Bool | false |
| `snap_to_ticks` | Bool | false |
| `wrap` | Bool | false |

### AdwSpinRow

#### Overview

AdwSpinRow (libadwaita 1.4+) wraps a GtkSpinButton in an Adwaita-styled list row, providing title, subtitle, and integrated +/- buttons. Used in preferences windows and settings panels.

#### Anatomy

```
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  Quantity                                    [-] 42 [+]  │
│  Number of items to order                                │
│  (subtitle)                                              │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

#### CSS Nodes

AdwSpinRow inherits from AdwActionRow:

```
row
├── box.header
│   ├── box.title
│   │   ├── label.title
│   │   └── label.subtitle
│   └── spinbutton (embedded)
│       ├── button.down  (-)
│       ├── text
│       └── button.up    (+)
```

#### Metrics

| Property | Value |
|----------|-------|
| Row min height | 56px (AdwActionRow standard) |
| Horizontal padding | 12px |
| Title font | Adwaita Sans Regular, 15px |
| Subtitle font | Adwaita Sans Regular, 13px |
| Subtitle color | dimLabel color |
| Spin button height | 34px (within row) |
| Spin button corner radius | 6px |
| Gap (title block to spin button) | 12px |

#### Properties

AdwSpinRow exposes the same value configuration as GtkSpinButton, plus row-level properties:

| Property | Type | Description |
|----------|------|-------------|
| `title` | String | Primary label text |
| `subtitle` | String | Secondary descriptive text |
| `adjustment` | GtkAdjustment | Value bounds and stepping |
| `digits` | UInt | Decimal places to display |
| `climb_rate` | Double | Acceleration rate for held buttons |
| `numeric` | Bool | Reject non-numeric characters |
| `snap_to_ticks` | Bool | Snap to nearest step increment |
| `wrap` | Bool | Wrap at bounds |

#### States

Inherits GtkSpinButton button states. Row-level states:

| State | Effect |
|-------|--------|
| Normal | Standard row background |
| Hover (row) | Row background subtly highlighted |
| Focused | 2px accent outline around spin button area |
| Disabled | Entire row dimmed, non-interactive |

### Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Button background change | 200ms | ease-in-out |
| Focus ring | 200ms | ease-in-out |
| Press (active) | Immediate | — |

### Accessibility

| Property | Value |
|----------|-------|
| Role | SpinButton (GTK_ACCESSIBLE_ROLE_SPIN_BUTTON) |
| Value properties | value-now, value-min, value-max |
| Orca/screen reader | "[Label], [value], spin button" |
| Keyboard | Arrow Up/Down for step, PageUp/PageDown for page |
| At limit | Value clamped, no wrap unless `wrap` is true |
