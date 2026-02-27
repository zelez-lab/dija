# Android — Dija Gaps

What Dija needs to fully replicate M3 (Material Design 3) native look.

## Effect System Gaps

| M3 visual | EffectKind needed | Status |
|-----------|------------------|--------|
| Solid fill | `Background(Color)` | Have it |
| Rounded corners | `BorderRadius(f32)` | Have it |
| Padding | `PaddingAll/PaddingEdges` | Have it |
| Border | `BorderColor/BorderWidth` | Have it |
| Box shadow | `BoxShadow(...)` | Have it in DrawCommand |
| Opacity | `Opacity(f32)` | Have it |
| Font size/weight | `FontSize/FontWeight` | Have it |
| Text color | `TextColor` | Have it |
| Tonal elevation | `TonalElevation(Level)` | **Missing** |
| State layer overlay | `StateLayer(Color, f32)` | **Missing** |
| Ripple effect | `Ripple(origin, color)` | **Missing** |
| Dynamic color | Runtime palette injection | **Missing** |
| Shape morphing | Animated corner radius | **Missing** |
| Gradient fill | `BackgroundGradient(Gradient)` | Missing from effects |
| Scale transform | `Scale(f32)` | **Missing** |
| Clip to bounds | `ClipToBounds(bool)` | **Missing** |

## Critical: Tonal Elevation

The defining M3 visual. Surface color shifts toward primary based on elevation level.
Unlike shadows, this is a **color computation**:

```
result = blend(surface_token, primary, tint_alpha[level])
```

Implementation options:
1. `EffectKind::TonalElevation(u8)` that resolves to a computed background color at render time
2. Precompute tinted surface colors per elevation level in the theme
3. Let the skin compute it explicitly (current approach with manual color calc)

Option 2 is simplest: theme provides `surface_at_elevation(level) -> Color`.

## Critical: State Layers (Ripple)

M3's interaction feedback is a **state layer** — a semi-transparent overlay using the
content color at specific opacities (hover 8%, focus 10%, pressed 10%, dragged 16%).

The **ripple effect** is a radial animation from the touch point that grows to fill
the component bounds, then fades. This is more complex than CSS `:hover` or `:active`:

- Needs touch coordinates (origin point)
- Needs animated radial expansion
- Needs opacity fade-in/fade-out
- Runs concurrently with state layer

Implementation path:
1. `EffectKind::StateLayer { color: Color, opacity: f32 }` for static state layers
2. `RippleEffect { origin: (f32, f32), color: Color, radius: f32, opacity: f32 }` as
   an animated draw command layered on top of the component
3. Ripple animator in the gesture system that drives radius + opacity over time

## Critical: Dynamic Color

On Android 12+, the system extracts a color palette from the wallpaper and provides
it as `dynamicLightColorScheme()` / `dynamicDarkColorScheme()`. Every M3 app is expected
to adopt this.

What Dija needs:
- Platform API to query the system's dynamic color palette (Android only)
- Runtime theme mutation: swap all color role tokens without rebuilding the tree
- Fallback to static baseline theme on older Android / other platforms

## Shape Morphing

M3 uses animated corner radius transitions:
- FAB press: corners smooth from 16dp to 28dp
- Container transform: source shape morphs to destination shape
- Bottom sheet expand: top corners animate from 28dp to 0dp

Needs:
- Animatable `border_radius` property (not just static)
- Transition system that interpolates between shape states
- Per-corner radius control (top-left, top-right, bottom-left, bottom-right)

## Container Transform

M3's signature shared-element transition where a component (e.g., card) smoothly
morphs into a full-screen surface. Involves simultaneous animation of:
- Position and size
- Corner radius (e.g., 12dp card -> 0dp full-screen)
- Elevation
- Content cross-fade

This is the most complex M3 animation and may need:
- `SharedElementTransition` coordinator
- Layout animation engine (animate between two layout states)
- Z-index management during animation

## Comparison: iOS vs M3 Gaps

| Gap | iOS priority | M3 priority |
|-----|-------------|-------------|
| Squircle corners | Critical | Not needed |
| Backdrop blur | Critical | Not needed |
| Materials (translucency) | Critical | Not needed |
| Tonal elevation | Not needed | Critical |
| State layer / ripple | Not needed | Critical |
| Dynamic color | Not needed | Critical |
| Shape morphing | Low | High |
| Spring animation | Critical | Medium (M3 uses cubic bezier) |
| Container transform | Low | High |

## Implementation Priority

1. **State layers** — without these, no M3 component looks right (every interactive element uses them)
2. **Tonal elevation** — surface container tokens handle most cases, but computed tint needed for custom elevation
3. **Ripple effect** — the most recognizable M3 interaction pattern
4. **Dynamic color** — platform-specific, can fallback to static theme
5. **Shape morphing** — important for polish, not blocking for basic components
6. **Container transform** — advanced, defer to post-v0.1
