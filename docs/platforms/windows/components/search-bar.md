# Windows — AutoSuggestBox (Search Bar)

Source: WinUI 3 AutoSuggestBox control

## Appearance

An input field with a query icon and a dropdown suggestion list. Looks like a TextBox with search functionality.

### Input Field

Same visual treatment as TextBox, with additional query icon.

| Property | Value |
|----------|-------|
| Height | 32px |
| Background | ControlFillColorDefault |
| Border | 1px ControlStrokeColorDefault + darker bottom stroke |
| Corner radius | 4px (controlCornerRadius) |
| Padding | 11px left, 5px top, 36px right (space for icons), 6px bottom |
| Font | 14px, Regular (400) |
| Placeholder | TextFillColorTertiary |
| Placeholder text | "Search" (localizable) |

### Query Icon

| Property | Value |
|----------|-------|
| Icon | `&#xE721;` (Search / magnifying glass) |
| Size | 12x12px glyph |
| Hit area | 32x32px |
| Position | Right side of input |
| Color | TextFillColorSecondary |
| Background | Transparent (subtle on hover) |

### Clear Button

| Property | Value |
|----------|-------|
| Icon | `&#xE10A;` (X / Cancel) |
| Size | 12x12px glyph |
| Visibility | Shown when text is present |
| Position | Right side, left of query icon |
| Hit area | 30x32px |

## Input States

| State | Background | Border | Bottom stroke |
|-------|-----------|--------|---------------|
| Rest | ControlFillColorDefault | ControlStrokeColorDefault | ControlStrokeColorSecondary |
| Hover | ControlFillColorSecondary | ControlStrokeColorDefault | ControlStrokeColorSecondary |
| Focused | ControlFillColorInputActive | ControlStrokeColorDefault | AccentColor (2px) |
| Disabled | ControlFillColorDisabled | ControlStrokeColorDefault (reduced) | None |

Same bottom accent stroke animation as TextBox on focus.

## Suggestion Dropdown

### Container

| Property | Value |
|----------|-------|
| Background | Acrylic (Background type) |
| Corner radius | 8px (layerCornerRadius) |
| Border | 1px SurfaceStrokeColorFlyout |
| Shadow | Shadow 8 |
| Padding | 4px vertical |
| Gap from input | 4px |
| Max height | 384px (scrollable) |
| Min width | Same as input field width |

### Suggestion Item

| Property | Value |
|----------|-------|
| Height | 36px |
| Padding | 12px horizontal |
| Corner radius | 4px (with 2px horizontal margin) |
| Font | 14px, Regular |
| Icon size | 16x16px (optional leading icon) |
| Icon-to-text gap | 12px |

### Suggestion Item States

| State | Background | Text |
|-------|-----------|------|
| Rest | Transparent | TextFillColorPrimary |
| Hover | SubtleFillColorSecondary | TextFillColorPrimary |
| Selected (keyboard) | SubtleFillColorSecondary | TextFillColorPrimary |
| Pressed | SubtleFillColorTertiary | TextFillColorSecondary |

### No Results

| Property | Value |
|----------|-------|
| Message | "No results found" or custom |
| Font | 14px, Regular |
| Color | TextFillColorSecondary |
| Padding | 12px |
| Alignment | Center |

## Structure

```
┌──────────────────────────────────┐
│ [search text]          [X] [🔍] │  ← Input field
└──────────────────────────────────┘
  ┌──────────────────────────────┐
  │ Suggestion item 1            │  ← Dropdown
  │ Suggestion item 2            │
  │ Suggestion item 3 (selected) │
  │ ...                          │
  └──────────────────────────────┘
```

## Events / API

| Event | When |
|-------|------|
| TextChanged | User types or clears text |
| SuggestionChosen | User selects a suggestion (tap or keyboard enter) |
| QuerySubmitted | User presses Enter or taps the query icon |

## Keyboard Navigation

| Key | Action |
|-----|--------|
| Down arrow | Move to first/next suggestion |
| Up arrow | Move to previous suggestion |
| Enter | Submit query or select highlighted suggestion |
| Escape | Close dropdown, clear selection |
| Tab | Move focus to next control (closes dropdown) |

## Animation

| Transition | Duration | Easing |
|-----------|----------|--------|
| Dropdown open | 200ms | Decelerate |
| Dropdown close | 150ms | Accelerate |
| Suggestion hover fill | 100ms | Control fast |
| Bottom accent stroke (focus) | 200ms | Decelerate |
| Input background transition | 100ms | Control fast |
