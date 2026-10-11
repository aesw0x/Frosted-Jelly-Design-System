# Frosted Jelly platform guidance

Frosted Jelly describes a visual language; its effects need platform-aware rendering. Arc Music uses Jetpack Compose and Material 3 as an implementation foundation, with app-specific visual treatment layered on top. This document records observed rendering paths, not a required implementation for other platforms.

## Frosted glass rendering

| Platform/path | Arc Music behavior |
| --- | --- |
| Android 14+ (API 34+) with Haze state | Haze child; 24dp blur; caller-provided tint and noise factor; supplied shape. |
| Android 14+ without Haze state | Theme-aware tinted shape, without blur. |
| Android 12–13 (API 31–33), backdrop available and shape corner-based | Arc custom `LayerBackdrop` renderer; backdrop scale 0.5; blur radius calculated as half of 24dp; translucent tint drawn on top. |
| Android 12–13 without a usable backdrop | Tinted background fallback. |
| Earlier fallback | Tinted background without backdrop blur. |

`applyHazeAndBackdrop` attaches Haze on API 34+ or Arc's layer backdrop on API 31–33. `glassEffect` applies blur, tint and noise. The custom `backdrop` package also contains lens, highlight, runtime-shader and shadow capabilities; those capabilities are not applied by every `glassEffect` call.

Default mini-player inputs are tint transparency 0.4 and noise factor 0.06. Dark mode adds 0.3 to tint alpha, capped at 0.85. The immersive tint is the sampled page color blended 18% toward white. Tint, alpha and text colors transition over 600ms. For the shared token summary, see [Tokens](../Tokens/TOKENS.md#glass-and-artwork-atmosphere); for implementation pointers, see [Foundations](../Foundations/FOUNDATIONS.md#frosted-glass-rendering-recipe).

## Visual fallbacks and resilience

- Preserve the intended foreground/background contrast when a blur or backdrop is unavailable; a tinted surface is the graceful fallback.
- Keep shape clipping consistent across platform paths so a fallback does not change the component silhouette.
- Treat noise as a subtle surface treatment and retain it only where the rendering path supports it cleanly.
- Keep artwork color adaptive, but clamp or neutralize swatches when they would reduce control or text contrast.
- Avoid assuming advanced backdrop capabilities are present because a helper package contains them; follow the actual component recipe.

## Compose and Material 3 boundary

Material 3 provides underlying roles and some component primitives. Frosted Jelly's identity comes from its chosen values, bespoke glass and glow, rounded compositions, artwork treatment, custom drawing and transitions. Some pieces wrap Material components; others are custom Canvas or Compose compositions. Arc Music is one implementation example; retain the visual contract while adapting product-specific behavior.

## Motion and accessibility

Offer reduced-motion behavior in future implementations: retain state clarity and legibility while reducing bounce, parallax and repeated ambient loops. Stop or reduce ambient effects when their surface is not visible. See the [motion guardrails](../Motion/MOTION.md#motion-guardrails-for-future-apps).

For concrete control semantics, target sizes, text scaling and a verification checklist, see [Accessibility](../Accessibility/ACCESSIBILITY.md). For window-size behavior and layout adaptation, see [Responsive layouts](../Responsive/RESPONSIVE.md).
