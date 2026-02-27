# iOS — Badge (Notification Badge)

Source: UITabBarItem.badgeValue, UIBarButtonItem, SwiftUI `.badge()`

iOS badges are red notification indicators displayed on tab bar items, app icons, and list rows. There is no standalone UIBadge class; badges are built into specific components.

## Tab Bar Badge

The most common badge in iOS — a red circle with a count on a tab bar item.

### Appearance

| Property | Value |
|----------|-------|
| Background | systemRed (`#FF3B30` / `#FF453A`) |
| Text color | white |
| Font | SF Pro Regular, 13pt |
| Font weight | Regular (some sources show Medium) |
| Corner radius | Fully rounded (pill/capsule) |
| Border | 1pt white border (separates from icon) |

### Sizing

| Content | Width | Height |
|---------|-------|--------|
| Empty (dot) | 6pt | 6pt |
| Single digit (1-9) | 18pt | 18pt |
| Double digit (10-99) | Dynamic (~24pt) | 18pt |
| Triple digit+ (100+) | Dynamic (~30pt) | 18pt |
| Text ("New") | Dynamic | 18pt |

| Property | Value |
|----------|-------|
| Minimum width | 18pt (for single character) |
| Horizontal padding | 5pt each side (when content wider than circle) |
| Maximum characters | No hard limit, but typically 1-4 (e.g., "999+") |

### Position

| Property | Value |
|----------|-------|
| Anchor | Top-right of the tab bar icon |
| Offset | ~(-8, -4)pt from top-right corner of icon bounds |
| Z-order | Above icon, above tab bar content |
| Clipping | Badge extends beyond tab bar item bounds (not clipped) |

## App Icon Badge (Home Screen)

| Property | Value |
|----------|-------|
| Background | systemRed |
| Text color | white |
| Font | SF Pro Bold, ~14pt |
| Size | 24pt diameter (single digit), pill for multi-digit |
| Horizontal padding | 6pt (multi-digit) |
| Position | Top-right corner of app icon |
| Border | 2pt white border |
| Max display | "99+" or "999+" (system-managed truncation) |
| Shadow | Subtle, offset(0, 1) blur 2, black @ 0.2 |

## List Row Badge (SwiftUI)

SwiftUI `.badge()` on List rows:

| Property | Value |
|----------|-------|
| Background | systemRed (numeric) or systemGray2 (text) |
| Text color | white (numeric), secondaryLabel (text) |
| Font | SF Pro Regular, 17pt (text badge), 17pt (count) |
| Shape | Pill (numeric), plain text (string) |
| Position | Trailing edge of row, before accessories |
| Corner radius | Fully rounded (numeric pill) |
| Padding | 5pt horizontal, 2pt vertical |

Note: In List/sidebar context, text badges may appear as plain secondary text rather than colored pills.

## Custom Badge Colors

`UITabBarItem.badgeColor` allows custom background colors:

| Property | Default |
|----------|---------|
| `badgeColor` | systemRed |
| `badgeTextAttributes` | White, SF Pro 13pt (customizable per state) |

## Animation

| Transition | Duration | Effect |
|-----------|----------|--------|
| Badge appear | 0.3s | Scale from 0 to 1 + fade in (spring, bounce 0.3) |
| Badge disappear | 0.2s | Scale from 1 to 0 + fade out |
| Badge update (value change) | 0.2s | Scale bounce (1.0 -> 1.2 -> 1.0) |
| First appearance | 0.3s spring | Slight overshoot |

## Metrics (Summary)

```
Tab bar item with badge:

      ┌───┐
      │ 3 │  ← badge (18pt circle, red, white text)
   ┌──┴───┘
   │  🏠  │  ← icon (25pt SF Symbol)
   │ Home │  ← label (10pt)
   └──────┘
```

## Badge Dot (Empty Badge)

When no count is needed, just a notification indicator:

| Property | Value |
|----------|-------|
| Diameter | 6pt |
| Color | systemRed |
| Border | 1pt white |
| Position | Same as numbered badge |
| Total visual size | ~8pt with border |

## Accessibility

| Property | Value |
|----------|-------|
| VoiceOver (tab) | "[Tab label], [badge value] items, tab" |
| VoiceOver (app icon) | "[App name], [badge value] notifications" |
| VoiceOver (list) | "[Row label], badge, [badge value]" |
| Empty badge | "Has unread notifications" or similar |
