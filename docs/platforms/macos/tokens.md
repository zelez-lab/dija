# macOS Design Tokens

Reference: Apple Human Interface Guidelines (macOS 14+), AppKit, SF Pro.

## Corner Radii

macOS uses consistent corner radii across the system. Window corners use a continuous (squircle) curve, not a simple circular arc.

| Element                  | Radius (pt) | Notes                                      |
|--------------------------|-------------|---------------------------------------------|
| Window                   | 10          | Continuous curve (superellipse)              |
| Sheet                    | 10          | Inherits window radius                      |
| Popover                  | 6           | Arrow tip is separate                        |
| Menu                     | 6           |                                              |
| Push button (regular)    | 6           | `NSButton.BezelStyle.push`                   |
| Push button (large)      | 8           | `controlSize = .large`                       |
| Push button (small)      | 4           | `controlSize = .small`                       |
| Push button (mini)       | 3           | `controlSize = .mini`                        |
| Text field               | 5           | `NSTextField.BezelStyle.roundedBezel`        |
| Search field             | 10          | Full capsule for regular height              |
| Segmented control        | 5           | `.capsule` style uses full capsule           |
| Toggle (switch track)    | 8           | Capsule shape                                |
| Toolbar item             | 6           |                                              |
| Alert                    | 10          | Matches window                               |
| Tooltip                  | 4           |                                              |
| Badge                    | full        | Circular or capsule                          |
| Sidebar selection        | 6           | Rounded rect highlight                       |
| Tab (segmented)          | 5           |                                              |

## Shadows

macOS shadows are subtle. Apple uses `shadowRadius` which equals `blur / 2` compared to CSS `box-shadow` blur.

### Window Shadow

```
Color:   #000000
Opacity: 0.30
Offset:  (0, 8) pt
Blur:    40 pt (CSS) / 20 pt (shadowRadius)
Spread:  0
```

Inactive window shadow is lighter:

```
Color:   #000000
Opacity: 0.18
Offset:  (0, 4) pt
Blur:    20 pt (CSS) / 10 pt (shadowRadius)
Spread:  0
```

### Menu / Popover Shadow

```
Color:   #000000
Opacity: 0.20
Offset:  (0, 4) pt
Blur:    20 pt (CSS) / 10 pt (shadowRadius)
Spread:  0
```

### Tooltip Shadow

```
Color:   #000000
Opacity: 0.12
Offset:  (0, 2) pt
Blur:    8 pt (CSS) / 4 pt (shadowRadius)
Spread:  0
```

### Button / Control Shadow (raised state)

```
Color:   #000000
Opacity: 0.06
Offset:  (0, 0.5) pt
Blur:    2 pt (CSS) / 1 pt (shadowRadius)
Spread:  0
```

Additional inner shadow for push buttons:

```
Color:   #000000
Opacity: 0.08
Offset:  (0, 0.5) pt
Blur:    0 pt
Type:    inset
```

## Typography

macOS uses SF Pro as the system font. SF Pro Text is used at 19 pt and below; SF Pro Display at 20 pt and above. Since macOS 11, the system uses a variable font that interpolates seamlessly between optical sizes.

### System Text Styles (macOS 11+)

| Style          | Size (pt) | Weight       | Line Height (pt) | Emphasized Weight |
|----------------|-----------|-------------|-------------------|-------------------|
| Large Title    | 26        | Regular     | 32                | Bold              |
| Title 1        | 22        | Regular     | 26                | Bold              |
| Title 2        | 17        | Regular     | 22                | Bold              |
| Title 3        | 15        | Regular     | 20                | Semibold           |
| Headline       | 13        | Bold        | 16                | Heavy             |
| Body           | 13        | Regular     | 16                | Semibold           |
| Callout        | 12        | Regular     | 15                | Semibold           |
| Subheadline    | 11        | Regular     | 14                | Semibold           |
| Footnote       | 10        | Regular     | 13                | Semibold           |
| Caption 1      | 10        | Regular     | 13                | Medium            |
| Caption 2      | 10        | Medium      | 13                | Semibold           |

### Font Weights (SF Pro)

| Weight       | CSS Value | SF Pro Value |
|-------------|-----------|-------------|
| Ultralight  | 100       | `.ultraLight` |
| Thin        | 200       | `.thin`       |
| Light       | 300       | `.light`      |
| Regular     | 400       | `.regular`    |
| Medium      | 500       | `.medium`     |
| Semibold    | 600       | `.semibold`   |
| Bold        | 700       | `.bold`       |
| Heavy       | 800       | `.heavy`      |
| Black       | 900       | `.black`      |

### Tracking (Letter Spacing)

SF Pro applies dynamic tracking that varies by point size. Larger sizes use tighter tracking; smaller sizes use wider tracking.

| Size Range (pt) | Tracking (em) | Notes                       |
|-----------------|---------------|-----------------------------|
| 6               | +0.072        | Wide for legibility          |
| 9               | +0.024        |                              |
| 12              | +0.012        |                              |
| 13 (Body)       | +0.006        |                              |
| 17              | -0.011        | Starts tightening            |
| 20              | -0.019        | SF Pro Display threshold     |
| 26              | -0.022        | Large Title                  |
| 34              | -0.026        |                              |
| 48+             | -0.030        | Display sizes                |

### Monospace Font

SF Mono is the system monospace font. Used in code editors, Terminal, Xcode.

| Style      | Size (pt) | Weight    |
|-----------|-----------|-----------|
| Code Body  | 13        | Regular   |
| Code Small | 11        | Regular   |

## Spacing Grid

macOS uses a **4-point grid** for most spacing decisions. The base unit is 4 pt, with 8 pt being the primary rhythm.

| Token                | Value (pt) | Usage                                      |
|---------------------|------------|---------------------------------------------|
| `spacing-0`          | 0          | No spacing                                   |
| `spacing-xxs`        | 2          | Tight spacing, inline elements               |
| `spacing-xs`         | 4          | Icon-to-label gap, tight padding             |
| `spacing-sm`         | 6          | Between related controls                     |
| `spacing-md`         | 8          | Standard padding, between groups             |
| `spacing-lg`         | 12         | Section padding, larger gaps                 |
| `spacing-xl`         | 16         | Window content margin, group spacing         |
| `spacing-xxl`        | 20         | Window edge padding, large sections          |
| `spacing-xxxl`       | 24         | Sheet padding, hero sections                 |

### Standard Gaps

| Context                          | Gap (pt) |
|----------------------------------|----------|
| Label to control                 | 8        |
| Between buttons (horizontal)     | 8        |
| Between buttons (vertical)       | 6        |
| Between form rows                | 8        |
| Between sections                 | 20       |
| Window content padding           | 20       |
| Alert body padding               | 20       |
| Toolbar item spacing             | 8        |
| Sidebar row vertical padding     | 4        |
| Sidebar row horizontal padding   | 10       |

## Animation Curves

macOS uses `NSAnimationContext` for AppKit animations and standard `CAMediaTimingFunction` curves.

### Standard Timing Functions

| Name              | Control Points              | Duration (ms) | Usage                            |
|-------------------|-----------------------------|--------------|-----------------------------------|
| Default           | (0.25, 0.1, 0.25, 1.0)     | 250          | General UI transitions            |
| Ease In           | (0.42, 0.0, 1.0, 1.0)      | 250          | Elements exiting                  |
| Ease Out          | (0.0, 0.0, 0.58, 1.0)      | 250          | Elements entering                 |
| Ease In Out       | (0.42, 0.0, 0.58, 1.0)     | 250          | Elements moving                   |
| Spring (default)  | bounce: 0.0, duration: 0.5  | 500          | SwiftUI default spring            |
| Spring (bouncy)   | bounce: 0.3, duration: 0.5  | 500          | Playful interactions              |
| Spring (snappy)   | bounce: 0.15, duration: 0.4 | 400          | Quick responsive feedback         |
| Linear            | (0.0, 0.0, 1.0, 1.0)       | varies       | Progress bars, loading            |

### Standard Durations

| Context                      | Duration (ms) | Curve             |
|------------------------------|--------------|-------------------|
| Button highlight             | 50           | Ease Out          |
| Button un-highlight          | 150          | Ease In Out       |
| Focus ring appearance        | 150          | Ease Out          |
| Focus ring removal           | 200          | Ease In           |
| Menu appearance              | 150          | Ease Out          |
| Menu dismissal               | 100          | Ease In           |
| Sheet presentation           | 250          | Ease In Out       |
| Sheet dismissal              | 200          | Ease In Out       |
| Popover appearance           | 200          | Ease Out          |
| Popover dismissal            | 150          | Ease In           |
| Sidebar collapse/expand      | 250          | Ease In Out       |
| Toggle switch                | 250          | Spring (snappy)   |
| Window resize                | 200          | Ease In Out       |
| Toolbar show/hide            | 250          | Ease In Out       |
| Tab switching                | 200          | Ease In Out       |
| Scroll deceleration          | varies       | Ease Out          |
| Hover state                  | 100          | Ease Out          |

## Hit Target Sizes

macOS has smaller hit targets than iOS since it uses pointer input.

| Control                  | Min Width (pt) | Min Height (pt) | Notes                            |
|--------------------------|---------------|-----------------|-----------------------------------|
| Push button              | 48            | 22              | Regular size                      |
| Push button (large)      | 48            | 28              |                                   |
| Push button (small)      | 32            | 19              |                                   |
| Push button (mini)       | 26            | 16              |                                   |
| Toolbar button           | 28            | 22              |                                   |
| Checkbox                 | 14            | 14              | Hit area extends to label         |
| Radio button             | 16            | 16              | Hit area extends to label         |
| Toggle (switch)          | 38            | 22              |                                   |
| Slider thumb             | 18            | 18              | Circular knob                     |
| Close/minimize/zoom      | 12            | 12              | Traffic light buttons             |
| Segmented control cell   | 28            | 22              | Regular size                      |
| Tab                      | 28            | 22              |                                   |
| Sidebar row              | full width    | 24              |                                   |
| Table row                | full width    | 24              | Default row height                |
| Menu item                | full width    | 22              |                                   |
| Popup button             | 48            | 22              |                                   |
| Stepper button           | 13            | 11              | Each increment/decrement button   |
| Scroll bar (hover)       | 8             | 8               | Expands on hover from 6 pt        |

### Control Size Matrix

AppKit provides four control sizes via `NSControl.ControlSize`:

| Size      | Font Size (pt) | Control Height (pt) | Since      |
|-----------|---------------|---------------------|------------|
| Mini      | 9             | 16                  | macOS 10.0 |
| Small     | 11            | 19                  | macOS 10.0 |
| Regular   | 13            | 22                  | macOS 10.0 |
| Large     | 15 (system)   | 28                  | macOS 11   |
