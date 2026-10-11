# Frosted Jelly Now Playing visual system

The Now Playing screen is its own composition system. It uses sampled artwork to color both the sharp artwork and the surrounding atmosphere, then layers scrims and content modes over it. These are design recipes, not playback behavior.

## Artwork atmosphere

1. A full-screen cover image is enlarged to fill and blurred by **80dp** behind the controls.
2. Arc samples the bottom 20% of the current cover and averages its pixels. That boundary color drives the accent and page tint. If the sampled strip is very bright (luminance above 0.65), the accent is neutralized to `#666666` so pale art does not wash out white controls.
3. Accent, light/dark background tint and text colors transition over **1400ms** using a Fast Out Slow In curve.
4. A darkening color layer overlays the blur. Typical alpha is 0.5; for near-white art it rises to 0.92.
5. Sharp artwork occupies a top-centered **0.9:1 aspect ratio** surface with **32dp corners**. A destination-in mask keeps a central band crisp while fading its top and bottom into the blurred field. Video Canvas art may sit **1.05×** over the still; it fades in after becoming ready.

Arc Music reference: `ArcNowPlayingScreen.kt` and `ui/components/CanvasArtworkPlayer.kt`.

## Now Playing scrims

There are several coordinated overlays on this screen:

- **Top legibility wash:** a gradient from background tint at the top to transparent. Its top alpha is normally 0.4 and rises to 0.88 in Lyrics or Queue mode.
- **Bottom text wash:** occupies the bottom 70% of the screen and fades from transparent through background tint to a stronger background tint. Typical stops use 0.4 and 0.8 alpha; bright cover strips use 0.85 and 1.0.
- **Lyrics/Queue dim layer:** black overlay alpha animates from zero to 0.38 over 600ms.
- **Artwork mask:** a transparent/black/transparent vertical mask makes the sharp cover image blend into the blurred background and controls. It is a content mask, distinct from the color scrims above.

Do not merge these into one generic gradient. Each has a different purpose and is driven by different state. Source: `ArcNowPlayingScreen.kt`.

## Lyrics and queue mode transition

Normal content and Lyrics/Queue content share the same full-screen container. Entering a mode brings the overlay up from 45% of its height with a spring and 280ms fade; normal content fades out over 180ms. Returning slides the overlay down by 35% of its height, then fades out over 220ms while normal controls return. Lyrics ↔ Queue uses a 200ms crossfade. The size transform does not clip the transition.

The lyrics presentation itself has an edge-faded viewport, active-line emphasis and timed word drawing. Home's hero has a simpler lyric preview; this full lyric engine is the Now Playing experience. Source: `ArcNowPlayingScreen.kt`, `ArcLyricEngine.kt`.

## Frosted Wave Seekbar

The progress control is a custom Canvas, not a stock slider:

- **36dp** high, tap- and drag-seekable, with elapsed and duration labels below.
- The played area has a solid baseline and an upward-only animated wave along its top edge. Its wave crests taper toward both ends of the played region.
- A second phase-shifted, lower-opacity wave sits behind the primary wave as a soft shadow.
- Wave phase loops every **1800ms** while the composable is active. Amplitude transitions between flat and playing state over the configured bloom duration; seeking suppresses the motion.
- Track baseline, wave amplitude, cycle length, shadow offset/opacity, primary opacity, thumb radius, unplayed stroke and bloom duration are read from settings, so the recipe is intentionally tunable.

Arc Music reference: `ArcNowPlayingScreen.kt`, `ScrubberAndTimer`.

## Other Now Playing transitions

- Current and previous artwork can coexist during a track change so the blur/cover replacement does not expose an empty frame.
- Sharp image alpha fades in over 800ms once loaded.
- Canvas artwork video fades in over 600ms after ready and slightly overscales the still art.
- The player sheet uses a different drag-linked transition; see [Motion](../Motion/MOTION.md) and `ui/components/PlayerBottomSheet.kt`.
- Artwork-derived accent, background and text colors transition together over **1400ms**. The blurred backdrop fades in over **800ms**, retaining the previous blurred image while a replacement loads.
