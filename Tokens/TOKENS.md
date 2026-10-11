# Frosted Jelly tokens

This page is the quick reference for Frosted Jelly's named visual values. Use these as the system defaults, and preserve the hierarchy and contrast behavior when a product needs a documented variation.

## Color and typography

| Token family | Frosted Jelly reference |
| --- | --- |
| Base palette | Near-white surfaces and dark text in light mode; `#000000` page background, `#0D0D0D`–`#282828` raised surfaces and soft white text in dark mode. Semantic error colors stay separate. |
| Display Large | Inter ExtraBold, 52sp / 62sp, −0.02sp tracking. |
| Headline Large | Inter Bold, 34sp / 40sp. |
| Headline Medium | Inter SemiBold, 24sp / 32sp. |
| Body Large | Inter Medium, 16sp / 24sp. |
| Body Medium | Inter Normal, 14sp / 20sp. |
| Label Small | Inter SemiBold, 12sp / 16sp. |
| Immersive detail title | 40sp / 46sp; component override. |
| Home feature title | 30sp; component override. |

The source theme defines a Material 3 role palette. These selected values make the neutral foundation concrete; use semantic roles (such as `surface`, `onSurface`, `outline` and `error`) in components instead of hardcoding hex values. Artwork-derived color is an accent input, not a replacement for text and status roles.

| Semantic role | Light reference | Dark reference |
| --- | --- | --- |
| Page/background | `#FCF8F9` | `#000000` |
| Surface | `#FCF8F9` | `#0D0D0D` |
| Surface container | `#F1EDED` | `#141414` |
| Surface container high | `#EBE7E8` | `#1E1E1E` |
| Surface container highest | `#E5E1E2` | `#282828` |
| Primary action | `#000000` | `#FFFFFF` |
| Main text | `#1C1B1C` | `#E8E8E8` |
| Secondary text | `#47464B` | `#AAAAAA` |
| Outline | `#78767C` | `#444444` |
| Error | `#BA1A1A` | `#FF6B6B` |

These palette values are implemented in Arc Music's `ui/theme/Color.kt`. They are the system's neutral foundation, but are not a full contrast-tested palette for every use. Always validate the final foreground/background pair, especially over artwork and translucent surfaces.

Source and color behavior: [Foundations](../Foundations/FOUNDATIONS.md#color-monochrome-foundation-with-media-color) and `app/src/main/java/com/aeswox/arcmusic/ui/theme/`.

## Shape, spacing and sizes

| Token | Frosted Jelly reference | Typical use |
| --- | --- | --- |
| `radius.surface.large` | 32dp | General large surfaces and mini-player. |
| `radius.artwork.home` | 36dp | Home feature artwork and album artwork. |
| `radius.artwork.artist` | 48dp | Non-immersive artist hero artwork. |
| `radius.capsule` | 50% / fully rounded | Pills, capsules and round controls. |
| `space.page.gutter` | 24dp | Common horizontal page margin. |
| `size.action.primary.height` | 56dp | Common primary action button. |
| `size.artwork.home` | 160dp square | Home artwork tile. |
| `size.player.mini.height` | 76dp | Mini-player row. |
| `size.player.mini.artwork` | 48dp square | Mini-player artwork, 16dp corners. |

The spacing scale standardizes common layout increments. Use component-specific values only when the documented composition calls for them. See [Foundations: shape and spacing](../Foundations/FOUNDATIONS.md#shape-and-spacing).

**Frosted Jelly spacing scale:** `4, 8, 12, 16, 20, 24, 32, 40, 48, 64dp`. Use these increments for new layouts; retain component-specific exceptions only when the composition needs them.

**Interaction size:** use a minimum **48 × 48dp** hit area for interactive controls, even when the visible icon is smaller. See [Accessibility](../Accessibility/ACCESSIBILITY.md#interaction-targets).

## Glass and artwork atmosphere

| Token / behavior | Frosted Jelly reference |
| --- | --- |
| `effect.glass.blur` | 24dp nominal blur for API 34+ Haze and the Android 12–13 backdrop path. |
| `effect.glass.miniPlayer.tintAlpha` | 0.4 light-mode base; dark mode adds 0.3, capped at 0.85. |
| `effect.glass.noise` | 0.06 default mini-player noise factor. |
| `effect.glass.immersiveTintBlend` | Artwork page color blended 18% toward white. |
| `motion.glass.tintTransition` | 600ms for mini-player tint, alpha and text color. |
| `effect.artworkGlow.field` | 1000dp circle scaled 1.2× × 1.8× (nominal 1200×1800dp). |
| `motion.artworkGlow.drift` | ±30dp X over 6s; ±20dp Y over 7.5s. |
| `motion.artworkGlow.breathe` | 75%–100% of caller intensity over 4s. |
| `motion.artworkGlow.color` | 1s color tween; default `#5E90A7`. |

The rendering paths and fallbacks are specified in [Platform guidance](../Platform/PLATFORM.md). Full recipes and source pointers are in [Foundations](../Foundations/FOUNDATIONS.md#frosted-glass-rendering-recipe).

## Component-specific reference values

| Component | Frosted Jelly reference |
| --- | --- |
| `FrostedHomeFeatureCard` | 1.3:1 image ratio, 36dp corners, 16dp shadow. |
| `FrostedNavigationBar` | 70dp bar; selected capsule 64×44dp. |
| `FrostedQuietCard` | 32dp corners; surface-container fill at 55% alpha; no backdrop blur. |
| `FrostedListeningTimeReadout` | 180dp glass pager card. |
| `FrostedActivityChart` | 256dp glass card. |
| `FrostedCollectionScoreRing` | 240dp ring, 12dp rounded stroke, 64sp score. |
| `FrostedCollectionStoryCard` | 300dp height, 24dp corners. |
| `FrostedGenreSpotlight` | 28dp corners; 52sp / 62sp title. |

See the [component catalog](../Components/COMPONENTS.md) and [layout patterns](../Patterns/LAYOUTS_AND_SCRIMS.md) for the full visual contracts.

## Motion constants

| Token | Frosted Jelly reference |
| --- | --- |
| `motion.jelly.pressScale` | 0.95 default; some controls use 0.92 or 0.88. |
| `motion.physicsBounce` | Mass 0.2, stiffness 100, damping ratio 0.25, amplitude 1, gravity 9.81. |
| `motion.stats.characterStagger` | 40ms between characters; 350ms duration. |
| `motion.stats.chartGrow` | 1000ms. |
| `motion.skeleton.sweep` | 1200ms shared shimmer; Collection Growth uses its own 1000ms sweep. |

The full choreography and named transitions live in the [motion catalog](../Motion/MOTION.md).

For reduced-motion behavior, read the [accessibility guidance](../Accessibility/ACCESSIBILITY.md#motion-and-effects).
