# Windows — Dija Gaps

What Dija needs to fully replicate Windows 11 Fluent 2 native look.

## Effect System Gaps

| Fluent visual | EffectKind needed | Status |
|--------------|------------------|--------|
| Solid fill | `Background(Color)` | Have it |
| Rounded corners (standard) | `BorderRadius(f32)` | Have it |
| Padding | `PaddingAll/PaddingEdges` | Have it |
| Border | `BorderColor/BorderWidth` | Have it |
| Box shadow (key + ambient) | `BoxShadow(...)` | Have it in DrawCommand |
| Opacity | `Opacity(f32)` | Have it |
| Font size/weight | `FontSize/FontWeight` | Have it |
| Text color | `TextColor` | Have it |
| Mica material | `Mica(MicaKind)` | **Missing** |
| Acrylic material (in-app blur) | `AcrylicInApp(...)` | **Missing** |
| Acrylic material (background blur) | `AcrylicBackground(...)` | **Missing** |
| Noise texture overlay | `NoiseOverlay(opacity)` | **Missing** |
| Reveal highlight (light follow) | `RevealHighlight(...)` | **Missing** |
| Smoke overlay (dimming) | `Overlay(Color)` | **Missing** |
| Focus visual (dual ring) | `FocusRing(outer, inner)` | **Missing** |
| Backdrop blur | Exists as DrawCommand | **Need as EffectKind** |
| Gradient fill | `BackgroundGradient(Gradient)` | Missing from effects (exists in DrawCommand) |
| Clip to bounds | `ClipToBounds(bool)` | **Missing** |
| Scale transform | `Scale(f32)` | **Missing** |
| Connected animation | Cross-node transition | **Not yet designed** |

## Critical: Mica Material

Mica is the defining visual of Windows 11 apps. Without it, apps look flat and non-native.

### Requirements

1. **Desktop wallpaper sampling** -- Mica reads the user's desktop wallpaper, blurs it, and uses it as a tinted background. This requires platform API access:
   - Win32: `DwmSetWindowAttribute` with `DWMWA_SYSTEMBACKDROP_TYPE = DWMSBT_MAINWINDOW`
   - WinRT: `MicaController` via `ICompositionSupportsSystemBackdrop`

2. **Fallback path** -- When Mica is unavailable (battery saver, remote desktop, Windows 10), fall back to `SolidBackgroundFillColorBase` (`#F3F3F3` light / `#202020` dark).

3. **Inactive window state** -- Mica should become a neutral solid when the window loses focus.

### Dija approach

Two strategies:
- **Delegate to OS** (preferred): Use `DwmSetWindowAttribute` to request Mica from the compositor. Zero rendering cost. Dija just sets the flag and uses a transparent window background.
- **Software emulation**: For platforms without Mica support, render a blurred wallpaper sample and apply tint. Only useful for cross-platform consistency testing.

## Critical: Acrylic Material

Acrylic (translucent blur) is used for all transient surfaces: menus, flyouts, context menus, command bars.

### Requirements

1. **In-App Acrylic** -- Blur of content behind the element within the app window. Requires render-to-texture of the background layers, then Gaussian blur (30px), tint overlay, luminosity clamp, and noise texture.

2. **Background Acrylic** -- Blur of content behind the app window (desktop, other windows). Requires:
   - Win32: `DwmSetWindowAttribute` with `DWMWA_SYSTEMBACKDROP_TYPE = DWMSBT_TRANSIENTWINDOW`
   - Or: `SetWindowCompositionAttribute` with accent policy

3. **Noise texture** -- 2% luminance noise overlay. Need a static noise texture (can be 64x64 tiling).

### Dija approach

- **In-App Acrylic**: Implement in dija-render. Render background to texture, blur pass, composite with tint + noise. This is a multi-pass GPU operation.
- **Background Acrylic**: Delegate to OS where possible. Software fallback = opaque tinted surface.

## Critical: Reveal Highlight

Reveal highlight is a light-following effect used on list items and interactive surfaces. A radial gradient of light follows the mouse pointer, illuminating borders near the cursor.

### Requirements

1. **Mouse-position-aware radial gradient** on borders -- the gradient center tracks the cursor position relative to the element.
2. **Propagation** -- the light effect bleeds across neighboring elements, creating a unified glow region.
3. **Performance** -- must be GPU-accelerated. CPU fallback would be too slow for large lists.

### Dija approach

- Implement as a shader effect in dija-render. Pass mouse position as a uniform. Each border pixel samples a radial falloff from the cursor.
- Only active on hover-capable devices (not touch).
- Can be disabled globally for performance-constrained environments.

## Important: Title Bar Integration

Windows 11 apps extend content into the title bar for a seamless appearance. The Mica material flows from the title bar into the app content area.

### Requirements

1. **`ExtendsContentIntoTitleBar`** equivalent -- Dija needs to support removing the default title bar and rendering content in the title bar region.
2. **Drag region management** -- Define which areas of the custom title bar are draggable vs interactive.
3. **Caption button area reservation** -- Reserve 138px on the right for system Close/Minimize/Maximize buttons, or implement custom caption buttons.
4. **Tall title bar** -- Support 48px height when a back navigation button is present.

### Dija approach

- Platform-specific window creation in dija-core: use `SetWindowLong` to remove standard title bar, handle `WM_NCCALCSIZE` and `WM_NCHITTEST` for custom hit testing.
- Expose a `TitleBar` component in dija-ui that handles drag regions and caption button spacing.

## Important: Focus Visuals (Dual Ring)

Fluent focus visuals use a two-ring system for maximum contrast against any background:
- **Outer ring**: 2px, high-contrast color (black in light mode, white in dark)
- **Inner ring**: 1px, contrasting color (white in light mode, black in dark)

### Requirements

- Render two concentric border rings around the focused element.
- The outer ring sits 2px outside the element bounds.
- The inner ring sits 1px outside the element bounds, between the element and the outer ring.
- Both rings must be visible regardless of the element's background color.

### Dija approach

- Implement as a `FocusVisual` effect in the style/effect system.
- When an element receives keyboard focus, the renderer adds the dual ring as an overlay.
- The ring should NOT affect layout (painted as an overlay, not as part of the box model).

## Nice-to-Have: Connected Animations

Fluent uses connected animations for page transitions where an element (e.g., a list item image) smoothly moves from one view to another.

### Requirements

- Cross-node animation: element A in view 1 morphs into element B in view 2 (position, size, corner radius interpolation).
- Requires a `TransitionLayer` (already have PhantomNode infrastructure from Step 011).

## Nice-to-Have: Teaching Tip Tail

TeachingTip has a triangular tail (arrow) pointing to the target element. The tail must not have a shadow (shadows cannot be applied to non-rectangular surfaces on Windows).

### Requirements

- Render a triangular tail on a popup surface.
- The tail should maintain a 12px margin from the edges of the tip.
- The tail should center on the target element when possible.

## Gap Priority

| Priority | Gap | Reason |
|----------|-----|--------|
| P0 | Mica material (OS delegation) | Defines Windows 11 identity |
| P0 | Acrylic material (in-app) | Required for all flyouts/menus |
| P0 | Focus visual (dual ring) | Accessibility requirement |
| P1 | Title bar integration | Expected in modern Windows apps |
| P1 | Smoke overlay | Required for ContentDialog |
| P1 | Acrylic material (background) | Needed for context menus |
| P2 | Reveal highlight | Polish, not strictly required |
| P2 | Noise texture | Acrylic detail |
| P2 | Connected animations | Page transition polish |
| P3 | Teaching tip tail | Niche component |
