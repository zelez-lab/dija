# iOS — Design Tokens

Source: Apple Human Interface Guidelines (iOS 17+)

## Corner Radii

| Context | Value | Shape |
|---------|-------|-------|
| Small (buttons, text fields, search bars) | 10pt | Superellipse (squircle) |
| Segmented control (outer) | 9pt | Superellipse |
| Segmented control (segment) | 7pt | Superellipse |
| Medium (cards, grouped cells) | 13pt | Superellipse |
| Alerts, action sheets | 14pt | Superellipse |
| Large (sheets, modals) | 16–20pt | Superellipse |
| Context menu preview | 16pt | Superellipse |
| App icons (home screen) | ~18% of icon width | Superellipse |

Apple's corners are NOT standard `border-radius`. They use a **superellipse** (squircle)
where the curve starts earlier and is smoother:
`|x/a|^n + |y/b|^n = 1` where `n ~ 4–5` (vs `n = infinity` for standard rounded rect).

The system calls this "continuous corners" (`CALayer.cornerCurve = .continuous`).

## Shadows

| Context | Offset (x, y) | Blur | Spread | Color |
|---------|---------------|------|--------|-------|
| Cards | (0, 2) | 8 | 0 | black @ 0.15 |
| Navigation bar (scroll shadow) | (0, 0.33) | 0 | 0 | separator color |
| Segmented control (selected) | (0, 3) blur 8 + (0, 3) blur 1 | — | — | black @ 0.04 + black @ 0.12 |
| Switch thumb | (0, 3) | 8 | 0 | black @ 0.15 |
| Slider thumb | (0, 0.5) blur 4 + (0, 0.5) blur 1 | — | — | black @ 0.12 + black @ 0.04 |
| Modals / alerts | (0, 10) | 40 | 0 | black @ 0.3 |
| Bottom sheets | (0, -10) | 40 | 0 | black @ 0.2 |
| Context menu preview | (0, 10) | 30 | 0 | black @ 0.2 |

## Typography

### Font Families

| Family | Usage |
|--------|-------|
| SF Pro Text | System text at 19pt and below (wider letter spacing, heavier strokes) |
| SF Pro Display | System text at 20pt and above (tighter spacing, refined strokes) |
| SF Pro Rounded | Playful contexts, timers, rounded UI |
| SF Mono | Code, monospaced content |
| New York | Serif, editorial content |

Note: The system automatically switches between Text and Display optical sizes at the 20pt boundary.

### Font Weights

| Weight Name | CSS Weight | SF Pro Variable Weight |
|-------------|-----------|----------------------|
| Ultralight | 100 | 30.925 |
| Thin | 200 | 110.725 |
| Light | 300 | 274.315 |
| Regular | 400 | 400 |
| Medium | 500 | 510 |
| Semibold | 600 | 590 |
| Bold | 700 | 700 |
| Heavy | 800 | 860 |
| Black | 900 | 1000 |

### Dynamic Type Scale (Default "Large" Size Category)

| Text Style | Size (pt) | Weight | Leading (pt) |
|------------|-----------|--------|--------------|
| Large Title | 34 | Regular | 41 |
| Title 1 | 28 | Regular | 34 |
| Title 2 | 22 | Regular | 28 |
| Title 3 | 20 | Regular | 25 |
| Headline | 17 | Semibold | 22 |
| Body | 17 | Regular | 22 |
| Callout | 16 | Regular | 21 |
| Subheadline | 15 | Regular | 20 |
| Footnote | 13 | Regular | 18 |
| Caption 1 | 12 | Regular | 16 |
| Caption 2 | 11 | Regular | 13 |

The minimum text size at the smallest Dynamic Type setting is **11pt** (Caption 2 floor).

### Common Component Typography

| Usage | Size (pt) | Weight |
|-------|-----------|--------|
| Navigation bar (standard title) | 17 | Semibold |
| Navigation bar (large title) | 34 | Bold |
| Button (default) | 17 | Semibold |
| Tab bar label | 10 | Medium |
| Alert title | 17 | Semibold |
| Alert message | 13 | Regular |
| Action sheet action | 20 | Regular |
| Action sheet cancel | 20 | Semibold |
| Table cell title | 17 | Regular |
| Table cell subtitle | 15 | Regular |
| Segmented control | 13 | Medium |
| Badge number | 13 | Regular |
| Search bar placeholder | 17 | Regular |

## Spacing

**8pt grid system** with half-step support:

| Token | Value |
|-------|-------|
| xxs | 2pt |
| xs | 4pt |
| sm | 8pt |
| md | 12pt |
| lg | 16pt |
| xl | 20pt |
| 2xl | 24pt |
| 3xl | 32pt |
| 4xl | 40pt |
| 5xl | 48pt |

### Common Spacing Values

| Context | Value |
|---------|-------|
| Table cell left inset | 20pt (16pt on compact) |
| Section header top/bottom padding | 22pt / 8pt |
| Grouped table section spacing | 35pt (header to header) |
| Content margins (default) | 16pt (compact), 20pt (regular) |
| Navigation bar button spacing | 8pt |
| Action sheet gap (actions to cancel) | 8pt |
| List row separator inset (left) | 20pt |

## Hit Target Sizes

| Element | Minimum Size |
|---------|-------------|
| All tappable elements | 44 x 44pt |
| Buttons (recommended) | 44 x 44pt (actual content can be smaller, hit area padded) |
| Navigation bar buttons | 44 x 44pt |
| Tab bar items | 49pt tall, equally distributed width |
| Slider thumb | 44 x 44pt (visual: 28pt, hit area padded) |
| Switch | 31 x 51pt (already meets minimum) |

Apple requires a **minimum tappable area of 44 x 44pt** even if the visual element is smaller. Elements smaller than this cause 25%+ tap error rates.

## Opacity Levels

| Usage | Alpha |
|-------|-------|
| Disabled controls | 0.3 |
| Pressed state (plain buttons) | 0.3 (text alpha) |
| Secondary label | 0.6 |
| Tertiary label | 0.3 |
| Quaternary label | 0.18 |
| Placeholder text | 0.3 (of label base) |
| Separator (non-opaque) | 0.29 (light), 0.33 (dark) |
| Dimming overlay (behind sheets/alerts) | black @ 0.4 |
| System fill | 0.2 (light), 0.36 (dark) |

## Animations

### System Animation Durations

| Animation | Duration | Curve |
|-----------|----------|-------|
| Default UIView animation | 0.25s | ease-in-out (0.42, 0, 0.58, 1.0) |
| Navigation push/pop | 0.35s | ease-in-out |
| Modal present/dismiss | 0.35s | ease-in-out (+ spring for present) |
| Keyboard show/hide | 0.25s | custom curve (curve 7) |
| Alert appear | 0.25s | spring (damping ~0.75) |
| Alert disappear | 0.2s | ease-in |
| Action sheet present | 0.3s | spring |
| Tab switch | immediate (no animation) |
| Fade transitions | 0.2s | ease-in-out |

### Spring Animation Parameters

| Context | Duration | Damping Ratio | Initial Velocity |
|---------|----------|--------------|-----------------|
| Switch toggle | 0.3s | 0.75 | 0 |
| Sheet snap to detent | 0.5s | 0.8 | velocity-dependent |
| Keyboard spring | 0.5s | mass=3, stiffness=1000, damping=500 | 0 |
| Context menu appear | 0.4s | 0.7 | 0 |
| Button scale (pressed) | 0.15s | 0.6 | 0 |
| Segmented control slide | 0.3s | 0.75 | 0 |

### Standard Easing Curves

| Name | Control Points | Usage |
|------|---------------|-------|
| ease-in | (0.42, 0, 1, 1) | Elements leaving screen |
| ease-out | (0, 0, 0.58, 1) | Elements entering screen |
| ease-in-out | (0.42, 0, 0.58, 1) | Default for most transitions |
| linear | (0, 0, 1, 1) | Progress bars, continuous animations |

### iOS 17+ Spring API

iOS 17 introduced simplified spring parameters:

| Parameter | Description | Range |
|-----------|-------------|-------|
| duration | Settling duration | > 0 (typical: 0.3–0.8s) |
| bounce | Bounciness | -1.0 (overdamped) to 1.0 (underdamped), 0 = critically damped |

Common presets:
- **Snappy**: duration 0.3, bounce 0.15
- **Smooth**: duration 0.5, bounce 0.0
- **Bouncy**: duration 0.5, bounce 0.3
- **Interactive**: duration 0.3, bounce 0.0

## Border Widths

| Context | Value |
|---------|-------|
| Separator (non-retina) | 1pt |
| Separator (retina / hairline) | 0.33pt (1px on 3x) |
| Text field border (when used) | 0.5pt |
| Button border (bordered style) | 1pt |
| Segmented control separator | 1pt (internal dividers) |

## Safe Areas

| Region | Inset |
|--------|-------|
| Status bar height | 54pt (Dynamic Island), 47pt (notch), 20pt (legacy) |
| Navigation bar height (standard title) | 44pt |
| Navigation bar height (large title) | 96pt (collapsed: 44pt) |
| Tab bar height | 49pt (83pt with bottom safe area) |
| Home indicator height | 34pt (bottom safe area on Face ID devices) |
| Keyboard height (portrait) | ~291pt (varies by device) |
