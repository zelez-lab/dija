# Windows — Design Tokens

Source: Microsoft Fluent 2 Design System, WinUI 3 (Windows App SDK 1.5+)

## Corner Radii

Windows 11 uses standard `border-radius` (NOT superellipse like iOS).

| Token | Value | Usage |
|-------|-------|-------|
| None | 0px | Square edges (legacy, high-contrast) |
| Small | 2px | Badges, small inline elements |
| Medium (controlCornerRadius) | 4px | Buttons, TextBox, CheckBox, ComboBox, ToggleSwitch |
| Large (layerCornerRadius) | 8px | Cards, flyouts, dialogs, tooltips, InfoBar |
| Extra Large (overlayCornerRadius) | 12px | TabView tabs, ContentDialog, teaching tips |
| Circular | 9999px | Pill shapes, ProgressRing, avatar circles |

The token `controlCornerRadius` (default 4px) can be overridden globally via XAML resources. Increasing it to 6px produces slightly rounder controls without breaking layout.

## Shadows / Elevation

Fluent shadows are always a **pair**: a sharp directional **key shadow** (light from above) and a soft diffused **ambient shadow** (general). Both use black with varying opacity.

### Light Theme Shadows

| Level | Key shadow | Ambient shadow | Usage |
|-------|-----------|----------------|-------|
| Shadow 2 | 0px 1px 1px rgba(0,0,0,0.08) | 0px 0px 2px rgba(0,0,0,0.06) | Cards at rest, tooltips |
| Shadow 4 | 0px 2px 2px rgba(0,0,0,0.08) | 0px 0px 4px rgba(0,0,0,0.06) | Cards on hover, command bar |
| Shadow 8 | 0px 4px 4px rgba(0,0,0,0.08) | 0px 0px 8px rgba(0,0,0,0.06) | Flyouts, menus, dropdowns |
| Shadow 16 | 0px 8px 8px rgba(0,0,0,0.08) | 0px 0px 16px rgba(0,0,0,0.06) | Teaching tips, dialogs |
| Shadow 28 | 0px 14px 14px rgba(0,0,0,0.13) | 0px 0px 28px rgba(0,0,0,0.11) | Content dialogs, full-screen overlays |
| Shadow 64 | 0px 32px 32px rgba(0,0,0,0.18) | 0px 0px 64px rgba(0,0,0,0.14) | Detached windows, elevated surfaces |

### Dark Theme Shadows

Dark theme uses the same structure but with higher opacity for visibility against dark backgrounds:

| Level | Key shadow | Ambient shadow |
|-------|-----------|----------------|
| Shadow 2 | 0px 1px 1px rgba(0,0,0,0.13) | 0px 0px 2px rgba(0,0,0,0.11) |
| Shadow 4 | 0px 2px 2px rgba(0,0,0,0.13) | 0px 0px 4px rgba(0,0,0,0.11) |
| Shadow 8 | 0px 4px 4px rgba(0,0,0,0.13) | 0px 0px 8px rgba(0,0,0,0.11) |
| Shadow 16 | 0px 8px 8px rgba(0,0,0,0.13) | 0px 0px 16px rgba(0,0,0,0.11) |
| Shadow 28 | 0px 14px 14px rgba(0,0,0,0.22) | 0px 0px 28px rgba(0,0,0,0.18) |
| Shadow 64 | 0px 32px 32px rgba(0,0,0,0.28) | 0px 0px 64px rgba(0,0,0,0.22) |

### Elevation Usage Map

| Surface | Shadow Level |
|---------|-------------|
| Cards at rest | Shadow 2 |
| Cards hovered | Shadow 4 |
| Flyout, MenuFlyout | Shadow 8 |
| CommandBarFlyout | Shadow 8 |
| TeachingTip | Shadow 16 |
| ContentDialog | Shadow 28 |
| Detached popout window | Shadow 64 |

## Typography

### Font Families

| Family | Usage |
|--------|-------|
| Segoe UI Variable Text | Body text (<=14px), optimized for legibility at small sizes |
| Segoe UI Variable Display | Headings (>=18px), refined letter shapes |
| Segoe UI Variable Small | Captions and tiny text (<12px) |
| Segoe Fluent Icons | Icon font for Fluent system icons |
| Cascadia Code / Cascadia Mono | Code, monospaced content |

Segoe UI Variable has two axes:
- **Weight** (`wght`): 100 (Thin) to 700 (Bold), continuous
- **Optical Size** (`opsz`): 8 to 36, auto-adjusts based on font size

The optical size axis automatically switches between Text (small) and Display (large) cuts. No manual switching needed.

### Type Ramp

| Style | Size (px) | Line Height (px) | Weight | Optical Size |
|-------|-----------|-------------------|--------|-------------|
| Caption | 12 | 16 | Regular (400) | Small |
| Body | 14 | 20 | Regular (400) | Text |
| Body Strong | 14 | 20 | Semibold (600) | Text |
| Body Large | 18 | 24 | Regular (400) | Text |
| Subtitle | 20 | 28 | Semibold (600) | Display |
| Title | 28 | 36 | Semibold (600) | Display |
| Title Large | 40 | 52 | Semibold (600) | Display |
| Display | 68 | 92 | Semibold (600) | Display |

### Font Weights

| Name | Value |
|------|-------|
| Thin | 100 |
| ExtraLight | 200 |
| Light | 300 |
| Regular | 400 |
| Medium | 500 |
| SemiBold | 600 |
| Bold | 700 |

### Common Component Typography

| Usage | Size (px) | Weight |
|-------|-----------|--------|
| Button text | 14 | SemiBold (600) |
| TextBox input | 14 | Regular (400) |
| TextBox placeholder | 14 | Regular (400) |
| NavigationView item | 14 | Regular (400) |
| NavigationView header | 14 | SemiBold (600) |
| MenuFlyout item | 14 | Regular (400) |
| ContentDialog title | 20 | SemiBold (600) |
| ContentDialog body | 14 | Regular (400) |
| InfoBar message | 14 | Regular (400) |
| Tab label | 14 | Regular (400) |
| ToolTip text | 12 | Regular (400) |
| Badge number | 11 | SemiBold (600) |

## Spacing

**4px grid system.** All dimensions, margins, and padding use multiples of 4 effective pixels (epx). Values 2, 6, and 10 exist for icon alignment adjustments.

| Token | Value |
|-------|-------|
| None | 0px |
| XXS | 2px |
| XS | 4px |
| S (sNudge) | 6px |
| S | 8px |
| M (mNudge) | 10px |
| M | 12px |
| L | 16px |
| XL | 20px |
| XXL | 24px |
| XXXL | 32px |

### Common Layout Spacing

| Context | Value |
|---------|-------|
| Page margin (compact) | 12px |
| Page margin (standard) | 24px |
| Card padding | 16px |
| Card gap | 8px |
| Stack item gap (default) | 8px |
| Content area margin (NavigationView minimal) | 12px |
| Content area margin (NavigationView expanded) | 24px |
| List item padding (vertical) | 8px |
| List item padding (horizontal) | 12px |

## Stroke Width

| Token | Value | Usage |
|-------|-------|-------|
| Thin | 1px | Default borders, separators |
| Thick | 2px | Focus indicators, active states |
| Thicker | 3px | TextBox bottom focus accent stroke |
| Thickest | 4px | Rarely used, emphasis strokes |

## Hit Target Sizes

| Element | Minimum Size |
|---------|-------------|
| All interactive elements | 32 x 32px (recommended) |
| Button (default height) | 32px |
| Touch target (tablet mode) | 40 x 40px |
| Compact mode controls | 24px height |
| Slider thumb hit area | 32 x 32px (visual: 20px) |

## Opacity Levels

| Usage | Alpha |
|-------|-------|
| Disabled controls | 0.4 (40%) |
| Disabled text | TextFillColorDisabled resource |
| Subtle fill (rest) | 0.0 (transparent) |
| Subtle fill (hover) | 0.05 |
| Subtle fill (pressed) | 0.03 |
| Secondary text | 0.61 |
| Tertiary text | 0.44 |
| Overlay smoke layer | black @ 0.30 (light), black @ 0.40 (dark) |

## Animations

### Standard Durations

| Duration Token | Value | Usage |
|----------------|-------|-------|
| Ultra fast | 50ms | Micro-interactions (checkbox check) |
| Faster | 100ms | Button press feedback, hover fills |
| Fast | 150ms | Fade out, small state changes |
| Normal | 200ms | Default transition duration |
| Slow | 300ms | Slide in, expand/collapse |
| Slower | 400ms | Page transitions, dialog open |
| Gentle | 500ms | Complex coordinated animations |

### Easing Curves

| Name | Cubic Bezier | Usage |
|------|-------------|-------|
| Ease (default) | cubic-bezier(0.8, 0, 0.2, 1) | Standard transitions |
| Accelerate (ease-in) | cubic-bezier(0.9, 0.1, 1, 0.2) | Elements leaving / fading out |
| Decelerate (ease-out) | cubic-bezier(0.1, 0.9, 0.2, 1) | Elements entering / fading in |
| Linear | cubic-bezier(0, 0, 1, 1) | Progress bars, continuous loops |
| Control fast (point-to-point) | cubic-bezier(0.17, 0.17, 0, 1) | Control state changes (hover, press) |
| Control normal | cubic-bezier(0.55, 0.55, 0, 1) | Expand/collapse transitions |

### Common Animation Recipes

| Animation | Duration | Easing |
|-----------|----------|--------|
| Button hover fill | 100ms | Control fast |
| Button press | 50ms | Linear |
| Flyout open | 200ms | Decelerate |
| Flyout close | 150ms | Accelerate |
| Dialog open | 300ms | Decelerate |
| Dialog close | 200ms | Accelerate |
| NavigationView pane expand | 300ms | Decelerate |
| NavigationView pane collapse | 200ms | Accelerate |
| Page enter (slide + fade) | 300ms | Decelerate |
| Page exit (slide + fade) | 150ms | Accelerate |
| ProgressBar indeterminate loop | 2000ms | Linear |
| ProgressRing indeterminate spin | 3000ms | Linear |
| ToggleSwitch knob slide | 200ms | Decelerate |
| Connected animation | 300ms | Decelerate |

## Border Widths

| Context | Value |
|---------|-------|
| Control border (default) | 1px |
| Focus visual (outer ring) | 2px |
| Focus visual (inner ring) | 1px (inset, contrasting) |
| TextBox bottom accent (focused) | 2px |
| Card border | 1px |
| Separator | 1px |
| Divider | 1px |
