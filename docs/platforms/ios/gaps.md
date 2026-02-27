# iOS — Dija Gaps

What Dija needs to fully replicate iOS native look.

## Effect System Gaps

| iOS visual | EffectKind needed | Status |
|-----------|------------------|--------|
| Solid fill | `Background(Color)` | Have it |
| Rounded corners | `BorderRadius(f32)` | Have it |
| Squircle (continuous corners) | `BorderRadiusContinuous(f32)` | **Missing** |
| Padding | `PaddingAll/PaddingEdges` | Have it |
| Border | `BorderColor/BorderWidth` | Have it |
| Box shadow | `BoxShadow(...)` | Have it in DrawCommand |
| Opacity | `Opacity(f32)` | Have it |
| Font size/weight | `FontSize/FontWeight` | Have it |
| Text color | `TextColor` | Have it |
| Backdrop blur | Exists as DrawCommand | **Need as EffectKind** |
| Color tint overlay | `Overlay(Color)` | **Missing** |
| Saturation boost | `Saturate(f32)` | **Missing** |
| Material (composite) | `Material(MaterialKind)` | **Missing** |
| Gradient fill | `BackgroundGradient(Gradient)` | Missing from effects (exists in DrawCommand) |
| Spring animation | Transition config in Variants | **Not yet designed** |
| Scale transform | `Scale(f32)` | **Missing** |
| Clip to bounds | `ClipToBounds(bool)` | **Missing** |
| Vibrancy blend mode | `Vibrancy(VibrancyLevel)` | **Missing** |
| Dimming overlay | `DimmingOverlay(f32)` | **Missing** (can composite manually) |
| Background scale-down | `Scale3D(f32, f32, f32)` or context | **Missing** |

## Critical: Squircle

Apple's corner radius is a superellipse. The SDF shader needs a different formula.
This is what makes iOS components look "Apple" vs "web".

Implementation path:
- `CALayer.cornerCurve = .continuous` equivalent
- SDF: `smoothContinuousRoundedRect(p, size, radius)` — superellipse with n~4.5
- Need per-corner radius support too (top-only rounding for sheets)

## Critical: Materials

The single biggest differentiator for an iOS look. Could be:
- A compound `EffectKind::Material(MaterialKind)` that expands to multiple draw commands
- Or individual effects composed manually

### Material Implementation Requirements

1. **Backdrop capture** — read pixels behind the view (requires render pipeline support)
2. **Gaussian blur** — configurable sigma (10–40pt range)
3. **Saturation filter** — boost ~1.8x on blurred result
4. **Tint overlay** — semi-transparent color layer
5. **Vibrancy** — blend modes for content rendered on materials (plus-lighter / multiply)
6. **Fallback** — opaque fill when blur unavailable or `reduceTransparency` is on

### Material Rendering Pipeline

```
Opaque background
  └─ Backdrop capture (offscreen texture)
       └─ Gaussian blur pass (downsample + blur + upsample)
            └─ Saturation adjustment pass
                 └─ Tint overlay composite
                      └─ Content (with vibrancy blend if needed)
```

## Critical: Spring Animations

iOS uses spring physics for nearly all interactive transitions. Dija needs:

1. **Spring timing model** — mass/stiffness/damping or duration/bounce (iOS 17+ API)
2. **Interruptible animations** — iOS animations can be interrupted and redirected mid-flight
3. **Velocity inheritance** — gesture velocity feeds into animation initial velocity
4. **Per-property springs** — different spring curves for position vs. opacity vs. scale

### Spring Presets Needed

| Preset | Duration | Bounce | Usage |
|--------|----------|--------|-------|
| Snappy | 0.3s | 0.15 | Button taps, small UI feedback |
| Smooth | 0.5s | 0.0 | Sheet presentation, navigation |
| Bouncy | 0.5s | 0.3 | Playful elements, switch toggle |
| Interactive | 0.3s | 0.0 | Gesture-driven transitions |

## Rendering Pipeline Gaps

| Feature | What's Needed | Status |
|---------|--------------|--------|
| Multi-pass compositing | Render-to-texture for blur input | **Not yet designed** |
| Gaussian blur shader | Separable blur with configurable radius | **Missing** |
| Saturation shader | HSL saturation adjustment | **Missing** |
| Blend modes | Plus-lighter, multiply for vibrancy | **Missing** |
| Offscreen render targets | For backdrop capture | Depends on GPU backend |
| Texture readback | For software backend blur | **Missing** |

## Layout Gaps

| Feature | What's Needed | Status |
|---------|--------------|--------|
| Safe area insets | Status bar, home indicator, notch | **Missing** (platform bridge) |
| Dynamic Type scaling | Font size preference from system | **Missing** (platform bridge) |
| Trait collection | Size class, display scale, layout direction | **Missing** |
| Preferred content size | Accessibility text size multiplier | **Missing** |

## Interaction Gaps

| Feature | What's Needed | Status |
|---------|--------------|--------|
| Haptic feedback | UIImpactFeedbackGenerator, UISelectionFeedbackGenerator | **Missing** (platform bridge) |
| Context menu (long press) | Preview + menu with spring animation | **Missing** |
| Swipe actions | Table row swipe with colored action buttons | **Missing** |
| Pull to refresh | Scroll overscroll -> spinner -> callback | **Missing** |
| Rubber-band scrolling | Elastic overscroll physics | **Missing** |
| Momentum scrolling | Deceleration rate (normal: 0.998, fast: 0.99) | **Missing** |
| Keyboard avoidance | Content inset adjustment when keyboard appears | **Missing** |
| Page sheet dismissal | Interactive drag-to-dismiss with spring snap | **Missing** |

## Accessibility Gaps

| Feature | What's Needed | Status |
|---------|--------------|--------|
| Reduce Transparency | Disable materials, use opaque fallbacks | **Missing** (need platform query) |
| Increase Contrast | Switch to high-contrast color variants | **Missing** (color palette exists) |
| Bold Text | Increase all font weights by ~1 step | **Missing** |
| Reduce Motion | Replace spring animations with fade/dissolve | **Missing** |
| VoiceOver | Accessibility tree, labels, hints, traits | **Not yet designed** |
| Dynamic Type | Scale all text with user preference | **Missing** (layout pipeline needed) |

## Priority Order for iOS Skin Fidelity

1. **Squircle corners** — visual fingerprint of iOS, affects every component
2. **Typography** — SF Pro metrics, Dynamic Type scale, font weight mappings
3. **System colors** — full semantic color palette (label, fill, separator, background)
4. **Materials + blur** — navigation bar, tab bar, alerts (defines the iOS "feel")
5. **Spring animations** — switch, sheet, navigation (defines the iOS "motion")
6. **Vibrancy** — text on materials (polish, not critical for v1)
7. **Haptics** — feedback for taps, selection changes (platform bridge)
8. **Safe areas** — device-specific insets (platform bridge)
