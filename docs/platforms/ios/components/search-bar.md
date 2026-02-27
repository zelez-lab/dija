# iOS — Search Bar (UISearchBar / UISearchController)

Source: UISearchBar, UISearchController, SwiftUI `.searchable`

## Appearance

| Property | Light | Dark |
|----------|-------|------|
| Background | tertiarySystemFill (`#767680` @ 0.12) | tertiarySystemFill (`#767680` @ 0.24) |
| Corner radius | 10pt | 10pt |
| Corner curve | `.continuous` (superellipse) | |
| Height | 36pt (search field), 56pt (with bar chrome) | |
| Border | None (flat fill) | |

## Search Field Metrics

| Property | Value |
|----------|-------|
| Left padding | 8pt (from left edge to search icon) |
| Search icon to text | 6pt |
| Text right padding | 28pt (space for clear button) |
| Font | SF Pro Regular, 17pt |
| Text color | label |
| Placeholder text | "Search" (localized) |
| Placeholder color | secondaryLabel |
| Cursor color | tintColor |

## Icons

| Icon | Symbol | Size | Color |
|------|--------|------|-------|
| Search (magnifying glass) | `magnifyingglass` | 14pt | secondaryLabel |
| Clear (x circle) | `xmark.circle.fill` | 17pt | tertiaryLabel |
| Bookmark (optional) | `book` | 14pt | secondaryLabel |
| Dictation (microphone) | `mic.fill` | 14pt | secondaryLabel |

## Cancel Button

| Property | Value |
|----------|-------|
| Text | "Cancel" |
| Font | SF Pro Regular, 17pt |
| Color | tintColor |
| Position | Right of search field |
| Spacing | 8pt from search field |
| Visibility | Hidden by default, slides in on focus |
| Animation | Slide in from right, 0.25s ease-in-out |

## States

| State | Search Field | Cancel |
|-------|-------------|--------|
| Inactive | Rounded rect, placeholder shown | Hidden |
| Focused (empty) | Cursor visible, cancel slides in | Visible |
| Focused (text) | Text shown, clear button visible | Visible |
| Results | Search field may stay focused or blur | May hide |

## Search Bar Styles

| Style | Description |
|-------|-------------|
| Prominent (default) | Translucent background bar with search field |
| Minimal | Only the search field, no background bar |

## Navigation Bar Integration

When embedded in a navigation bar via UISearchController:

| Property | Value |
|----------|-------|
| Position | Below large title, above content |
| Default visibility | Hidden (revealed on pull-down scroll) |
| Always visible | Optional (`hidesSearchBarWhenScrolling = false`) |
| Focus behavior | Navigation bar collapses, search bar pins to top |
| Scope bar | Optional segment control below search field |

### Scope Bar

| Property | Value |
|----------|-------|
| Style | Segmented control |
| Height | 32pt |
| Position | Below search bar |
| Background | Same as search bar background |
| Visibility | Shown when search is focused (configurable) |
| Animation | Slides down, 0.25s |

## Search Suggestions

iOS 16+ supports search suggestions displayed below the search bar:

| Property | Value |
|----------|-------|
| Suggestion row height | 44pt |
| Icon | SF Symbol, 22pt, tintColor |
| Text font | SF Pro Regular, 17pt |
| Text color | label |
| Background | systemBackground |
| Separator | Standard (0.33pt, 20pt inset) |

## Search Tokens

iOS 13+ supports search tokens (structured filter chips):

| Property | Value |
|----------|-------|
| Token height | ~24pt |
| Background | tintColor @ 0.15 |
| Corner radius | 6pt |
| Text font | SF Pro Regular, 15pt |
| Text color | tintColor |
| Icon size | 16pt |
| Padding | 4pt vertical, 8pt horizontal |
| Removable | Backspace deletes token |

## Animation

| Transition | Duration | Curve |
|-----------|----------|-------|
| Focus (cancel slides in) | 0.25s | ease-in-out |
| Blur (cancel slides out) | 0.2s | ease-in-out |
| Navigation collapse on focus | 0.25s | ease-in-out |
| Scope bar appear | 0.25s | ease-in-out |
| Clear button appear | 0.15s | fade |

## Accessibility

| Property | Value |
|----------|-------|
| Role | Search field |
| VoiceOver | "Search field, [placeholder or text]" |
| Cancel | "Cancel, button" |
| Clear | "Clear text, button" |
| Scope | "Scope bar, [selected], [N] of [total]" |
