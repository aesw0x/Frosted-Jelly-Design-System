# Frosted Jelly foundations

## Color: monochrome foundation with media color

The base theme is intentionally near-monochrome:

- Light mode: warm near-white page and surface layers, dark text, black primary actions, and gray secondary roles.
- Dark mode: true-black page background (`#000000`), raised near-black surfaces from `#0D0D0D` through `#282828`, soft white text and restrained gray outlines.
- Semantic error colors remain separate from the neutral foundation.
- Material 3 color roles are used as the API shape; Frosted Jelly specifies the neutral role values. Arc Music implements these values, and artwork-derived accents are controlled separately from Android dynamic color.

**Frosted Jelly principle:** keep chrome, data visualization and basic controls neutral; let artwork supply the occasional accent. In immersive pages, sample the cover's dominant and vibrant swatches, cache them by image URL (LRU capacity 128), and use the result for the background, accent, mini-player tint and scrims. Artwork requests are downsampled to 128px for palette extraction. Bright artwork is limited to HSL lightness 0.40 before the dark-theme adjustment; dark mode nudges bright colors toward black. Accent selection avoids a color too close to the page background and has a contrast fallback.

Arc Music implementation example: `app/src/main/java/com/aeswox/arcmusic/ui/theme/Color.kt`, `Theme.kt`, and `app/src/main/java/com/aeswox/arcmusic/ReusableComponents.kt` (`PaletteCache`, `rememberDominantColor`, `rememberVibrantColor`, `immersiveBackground`, `darkenTowardBlack`).

## Typography

Frosted Jelly's typeface is **Inter**, with Normal, Medium, SemiBold, Bold and ExtraBold weights. The shared roles include:

| Role | Frosted Jelly reference |
| --- | --- |
| Display Large | 52sp / 62sp, ExtraBold, −0.02sp tracking |
| Headline Large | 34sp / 40sp, Bold |
| Headline Medium | 24sp / 32sp, SemiBold |
| Body Large | 16sp / 24sp, Medium |
| Body Medium | 14sp / 20sp, Normal |
| Label Small | 12sp / 16sp, SemiBold |

Other Material typography roles are assigned Inter as their family. Feature compositions deliberately override shared sizes: for example, the Home hero title is 30sp and immersive detail titles are 40sp with 46sp line height. Preserve those as component-level styles. Arc Music implements the type system in `app/src/main/java/com/aeswox/arcmusic/ui/theme/Type.kt`, plus `MainActivity.kt`, `AlbumDetailsScreen.kt` and `ArtistDetailsScreen.kt`.

## Shape and spacing

The Frosted Jelly large surface radius is **32dp** (`radius.surface.large`). The geometry hierarchy is:

| Use | Reference geometry |
| --- | --- |
| General large surface / mini-player | 32dp radius |
| Capsules and round controls | Circle / 50% radius; common button height 56dp |
| Home hero and album artwork | 36dp radius |
| Non-immersive artist hero artwork | 48dp radius |
| Common page gutter | 24dp |
| Artwork tiles on Home | 160dp square, 24dp radius |

These are system reference values, not an exhaustive list of every component-specific shape. Arc Music may use additional product-specific dimensions; retain the hierarchy and document meaningful exceptions when applying the system.

## Frosted glass rendering recipe

The shared `glassEffect` chooses a path based on OS support. The component shape clips the effect; the tint and noise are inputs so surfaces can be tuned consistently.

| Platform/path | Arc Music behavior |
| --- | --- |
| Android 14+ (API 34+) with Haze state | Haze child; 24dp blur; caller-provided tint and noise factor; supplied shape. |
| Android 14+ without Haze state | Theme-aware tinted shape, without blur. |
| Android 12–13 (API 31–33), backdrop available and shape corner-based | Arc custom `LayerBackdrop` renderer; backdrop scale 0.5; blur radius is calculated as half of 24dp; translucent tint is drawn on top. |
| Android 12–13 without a usable backdrop | Tinted background fallback. |
| Earlier fallback | Tinted background without backdrop blur. |

Default mini-player inputs are tint transparency **0.4** and noise factor **0.06**. In dark mode the tint alpha is increased by 0.3 and capped at 0.85. The mini-player's immersive tint is the sampled page color blended 18% toward white; its glass tint, alpha and text colors transition over 600ms. The mini-player is 76dp high, has 24dp horizontal page margins, a 32dp radius and 16dp horizontal internal padding; cover art is 48dp with 16dp corners.

`applyHazeAndBackdrop` attaches Haze on API 34+ or Arc's layer backdrop on API 31–33. `glassEffect` applies the blur/tint/noise recipe. The custom `backdrop` package also contains lens, highlight, runtime-shader and shadow capabilities; those capabilities should not be mistaken for effects currently applied by every `glassEffect` call.

Arc Music implementation example: `app/src/main/java/com/aeswox/arcmusic/ReusableComponents.kt` and `app/src/main/java/com/aeswox/arcmusic/MainActivity.kt`; renderer implementation: `app/src/main/java/com/aeswox/arcmusic/backdrop/`.

## Ambient artwork glow

`FrostedArtworkGlow` is the design-system name for Arc's `AnimatedGlowBackground` recipe:

- 1000dp circular radial field, scaled to 1.2× horizontally and 1.8× vertically (nominally 1200×1800dp).
- Center drifts from −30dp to +30dp horizontally over 6 seconds and −20dp to +20dp vertically over 7.5 seconds.
- Alpha cycles between 75% and 100% of the caller's `glowIntensity` over 4 seconds.
- Gradient stops use the animated alpha, 60% of that alpha, then transparent.
- Color changes tween over 1 second. Default color is `#5E90A7`; Home may use the current artwork's dominant color when dynamic artwork colors are enabled.
- The intensity comes from settings/callers; there is no single universal intensity value.

Arc Music implementation example: `ReusableComponents.kt`; visible in Home, the welcome overlay, Canvas settings and playlist creation.

## Interaction baseline

Arc disables Material ripple and default overscroll in its theme. Reusable Jelly press feedback and the custom physics bounce provide the characteristic touch response. On future platforms, offer an accessible reduced-motion path and retain a clear pressed/selected state even when movement is reduced.
