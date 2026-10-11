# Arc Music implementation map

Arc Music is an app built with Frosted Jelly. Use this guide to inspect how the system is applied in a working product. The design-system docs define the visual contracts; paths below locate their Arc Music implementations. Feature behavior and music-specific data are outside the design-system contract.

| What to inspect | Arc Music location | What it demonstrates |
| --- | --- | --- |
| Theme, font and monochrome base | `app/src/main/java/com/aeswox/arcmusic/ui/theme/Color.kt`, `Theme.kt`, `Type.kt` | Fixed light/dark color roles, Inter weights, ripple/overscroll baseline. |
| Shared visual helpers | `app/src/main/java/com/aeswox/arcmusic/ReusableComponents.kt` | Adaptive palettes, immersive header, glass, glow, mini-player, nav and common controls. |
| Custom shimmer and feedback | `app/src/main/java/com/aeswox/arcmusic/AnimationUtils.kt` | Stagger, shimmer, skeleton crossfade, checkbox, badge and bottom scrim. |
| Jelly buttons and press modifier | `app/src/main/java/com/aeswox/arcmusic/ui/components/JellyButtons.kt`, `ui/animations/JellyClickModifier.kt` | No-ripple tactile scale interaction. |
| Physics overscroll | `app/src/main/java/com/aeswox/arcmusic/ui/animations/PhysicsBounceOverscrollFactory.kt` | Configurable Compose bounce; inspect album, artist and stats pages for use. |
| Android View bounce | `app/src/main/java/com/aeswox/arcmusic/ui/animations/PhysicsBounceAnimator.kt` | View-based counterpart. |
| Custom blur fallback | `app/src/main/java/com/aeswox/arcmusic/backdrop/` plus `MainActivity.kt` | Layer backdrop, scaled rendering and custom effect/shader support for older blur path. |
| Home layout, navigation and Home hero | `app/src/main/java/com/aeswox/arcmusic/MainActivity.kt` | Monochrome page composition, feature card pager and playback scrim, bottom chrome and tab motion. |
| Additional Home/Search patterns | `app/src/main/java/com/aeswox/arcmusic/MainActivity.kt` | Translucent `GlassCard`, search mode tint, result gradients, section cards and summary widgets. |
| Album page | `app/src/main/java/com/aeswox/arcmusic/AlbumDetailsScreen.kt` | Full-bleed immersive header, Play/Shuffle capsules, tracks and shimmer skeleton. |
| Artist page | `app/src/main/java/com/aeswox/arcmusic/ArtistDetailsScreen.kt` | Immersive and conventional hero variants, artist lists and skeleton states. |
| Playlist page | `app/src/main/java/com/aeswox/arcmusic/PlaylistDetailsScreen.kt` | Shared immersive header pattern plus playlist-specific layout. |
| Listening Stats | `app/src/main/java/com/aeswox/arcmusic/ListeningStatsScreen.kt` | Per-character period readout, animated bar chart, blurred artist refresh and genre/personality cards. |
| Collection tools | `app/src/main/java/com/aeswox/arcmusic/CollectionHealthScreen.kt`, `CollectionGrowthScreen.kt` | Neutral score ring, semantic status rows, artwork-led story cards and a separate size-aware skeleton shimmer. |
| Library and selection | `app/src/main/java/com/aeswox/arcmusic/LibraryComponents.kt` | Pager dots, animated title, library item selection and action dock. |
| Appearance and update | `app/src/main/java/com/aeswox/arcmusic/AppIconScreen.kt`, `components/UpdaterCard.kt` | App icon selection feedback and update overlay/card transitions. |
| Search, genre and playlist actions | `app/src/main/java/com/aeswox/arcmusic/GenreHubScreen.kt`, `AddToPlaylistSheet.kt` | Genre spotlight panel and in-sheet transition from choosing to creating a playlist. |
| Now Playing and lyrics | `app/src/main/java/com/aeswox/arcmusic/ArcNowPlayingScreen.kt`, `ArcLyricEngine.kt` | Waveform, color transitions, timed lyric drawing and viewport fades. |
| Now Playing recipe | [Now Playing visual system](../Patterns/NOW_PLAYING.md) | Source-verified artwork blur, palette sampling, masks, scrims, lyrics/queue transition and wave seekbar values. |
| Mini-to-full player | `app/src/main/java/com/aeswox/arcmusic/ui/components/PlayerBottomSheet.kt` | Drag-linked media surface states. |
| Menu and morphing glyphs | `ui/components/MorphingMenu.kt`, `PlayPauseMorphIcon.kt`, `FavoriteHeartIcon.kt` | Anchor morph, Canvas morph and favorite feedback. |
| Modal panel reveal | `ui/components/ArcModalBottomSheet.kt` | Rounded modal surface, dark scrim, content slide/fade and blur. |
| Global status pill | `app/src/main/java/com/aeswox/arcmusic/ui/components/GlobalProgressOverlay.kt` | Expanding compact status surface and detail presentation. |
| Global status pill motion | [Motion](../Motion/MOTION.md#frosted-progress-island-morph) | Compact/expanded dimensions, radius/color morph, entry/exit, detail content and jelly squash-pop. |
| App mark and animated artwork | `ui/components/AnimatedSplashScreen.kt`, `CanvasArtworkPlayer.kt` | Drawn splash mark and artwork video treatment. |
| Share/receive motion | `app/src/main/java/com/aeswox/arcmusic/sharing/ShareScreen.kt`, `ReceiveScreen.kt` | Device scan rings, status/progress transitions and receive card states. |
| Secondary feature motion | `app/src/main/java/com/aeswox/arcmusic/SleepTimerSheet.kt`, `ui/screens/OnboardingScreen.kt` | Timer selections, changing timer content and onboarding page indicators. |
| Additional pattern catalog | [Additional visual patterns](../Patterns/ADDITIONAL_PATTERNS.md) | Secondary visual components and behaviors discovered in the second source audit. |

## Read-me-first walkthrough

1. Start at Home: inspect the monochrome scaffold, 24dp gutters, Home feature card, sampled artwork glow and bottom chrome.
2. Open an album or artist, then scroll: inspect the artwork-to-color fade, Back/More retreat, title detent and custom overscroll.
3. Open Listening Stats and switch periods: inspect the staggered readout and chart growth; scroll to see the other statistics cards.
4. Start playback: inspect the mini-player, playback scrim, lyrics and sheet expansion.
5. Inspect a loading detail page to see the shimmer and skeleton geometry.

## Scope and extraction note

Frosted Jelly is the visual specification; Arc Music is one implementation of it. The app may include product-specific choices and inline values in addition to the system tokens. Use this map to find examples, and use the design-system catalogs to resolve reusable visual contracts. This folder is documentation, not a code extraction or dependency module.
