# iOS — Progress Bar (UIProgressView)

Source: UIProgressView, SwiftUI ProgressView

## Styles

| Style | Height | Usage |
|-------|--------|-------|
| Default | 4pt | General progress indication |
| Bar | 2.5pt | Toolbars, navigation bars (e.g., Safari loading) |

## Track

| Property | Default Style | Bar Style |
|----------|--------------|-----------|
| Height | 4pt | 2.5pt |
| Corner radius | 2pt (fully rounded) | 1.25pt (fully rounded) |
| Background (unfilled) | systemFill (`#787880` @ 0.20 / @ 0.36) | systemFill |
| Filled color | tintColor (systemBlue default) | tintColor |
| Width | Full width of container | Full width of container |

## Colors

| Property | Light | Dark |
|----------|-------|------|
| Progress tint (default) | systemBlue (`#007AFF`) | systemBlue (`#0A84FF`) |
| Track tint (unfilled) | systemFill (`#787880` @ 0.20) | systemFill (`#787880` @ 0.36) |

Both `progressTintColor` and `trackTintColor` are fully customizable.

## Progress Value

| Property | Value |
|----------|-------|
| Range | 0.0 to 1.0 (clamped) |
| Default | 0.0 |
| Animation (setProgress animated) | ~0.25s ease-in-out |

## Indeterminate Progress (SwiftUI)

SwiftUI's `ProgressView()` without a value shows an indeterminate indicator. On iOS, this renders as a spinning `UIActivityIndicatorView` (not a progress bar). For a linear indeterminate bar, custom implementation is needed.

## Custom Images

UIProgressView supports custom images for both the progress and track:

| Property | Description |
|----------|-------------|
| `progressImage` | UIImage for the filled portion (stretched) |
| `trackImage` | UIImage for the unfilled portion (stretched) |

Images are resizable and stretched to fill their respective regions.

## Metrics (Summary)

```
Default style:
├──────────────────━━━━━━━━━━━━━━━━━━━━━━━┤  ← 4pt height
  filled (tintColor)    unfilled (gray)
  ←────── progress ──────→←──── track ────→

Bar style:
├──────────━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┤  ← 2.5pt height
```

## Animation

| Transition | Duration | Curve |
|-----------|----------|-------|
| Progress update (animated) | 0.25s | ease-in-out |
| Progress update (not animated) | Instant | — |
| Fill direction | Left to right (LTR), right to left (RTL) | — |

## Observed Value (SwiftUI)

SwiftUI `ProgressView` supports automatic progress tracking:

```swift
ProgressView(value: downloaded, total: totalSize) {
    Text("Downloading...")
} currentValueLabel: {
    Text("\(Int(downloaded))MB / \(Int(totalSize))MB")
}
```

| Property | Value |
|----------|-------|
| Label font | SF Pro Regular, 17pt (body) |
| Current value label font | SF Pro Regular, 13pt (footnote) |
| Label color | label |
| Value label color | secondaryLabel |
| Spacing (label to bar) | 4pt |

## Accessibility

| Property | Value |
|----------|-------|
| Role | Progress indicator |
| VoiceOver | "[Label], [percentage]% complete" |
| Updates | VoiceOver announces significant changes |
