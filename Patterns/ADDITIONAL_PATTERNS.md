# Additional Frosted Jelly patterns

This is the second-pass catalog of distinct visual recipes found beyond the global theme, glass, navigation, hero, stats and player systems. These screen-level patterns can be reused selectively; their app-specific content should not be mistaken for universal controls.

**Implementation note:** Frosted Jelly defines the visual contracts. Arc Music implements some with custom drawing (for example, the wave seekbar and overscroll) and others by styling or composing Material 3 components (for example, the collection score ring and update card). Unmodified Material defaults are not part of this catalog.

## Home, search and library

### Frosted Quiet Card

Arc's shared `GlassCard` is not a blur surface: it uses `surfaceContainer` at **55% alpha**, clipped to the shared **32dp** radius. Use this for quiet content groupings where the page shows through slightly. Keep the blur-backed `FrostedGlassSurface` separate so naming communicates the rendering behavior. Reference: `MainActivity.kt`, `GlassCard`; used by Listening Stats and collection widgets.

### Frosted Search Field

The search field has **32dp corners**, **24dp horizontal internal padding**, 4dp vertical container padding, and a 12dp icon-to-text gap. AI mode transitions the background and icon tint over **300ms** and swaps the leading search glyph for a sparkle. The clear and AI actions use Jelly press feedback. Reference: `MainActivity.kt`, `SearchBar`.

### Frosted Library Pager and Selection Dock

Library page markers are 4dp inactive and 6dp selected, with animated color and a low-stiffness scale change. The section title changes with a vertical fade/slide. Multi-select exposes a context-sensitive bottom action dock: 36dp corners, 24dp outer gutters, neutral raised surface, icon above a small uppercase label; destructive actions use the error color. Reference: `LibraryComponents.kt`.

### Frosted Search Result Treatments

Search uses Frosted Jelly song, album, artist and playlist rows/cards with artwork, optional selected-state controls, quality/explicit badges, and a custom top-result artwork gradient. These compose the search experience from shared visual patterns; they are not all shared primitives. Arc Music implementation: `MainActivity.kt`, `TopResultSection`, `SongResultItem` and result item components.

## Collection and discovery

### Frosted Collection Score Ring

Collection Health centers a **64sp** score inside a **240dp** Material progress indicator. Arc specifies a neutral on-surface progress stroke at **12dp** with rounded caps and a muted track. The surrounding breakdown is a quiet card with tappable **48dp** icon discs. Warning/success indicators use semantic color while the score visualization stays monochrome. Reference: `CollectionHealthScreen.kt`.

### Frosted Collection Story Card

Collection Growth uses photo-led **300dp-high** cards with **24dp** corners, a round dismiss affordance at top-right and a bottom gradient from transparent through surface at 80% to solid surface. Text and action sit in a 20dp inset. This is a reusable editorial/recommendation card pattern for image-led content. Reference: `CollectionGrowthScreen.kt`.

### Frosted Collection Growth Skeleton

This page has its own card-sized shimmer instead of the shared shimmer helper: gradient stops use the highest surface container at 40/80/40% opacity, and the sweep moves from −2× to +2× the measured card width over **1000ms**. Skeleton cards preserve the image, dismiss button, title, subtitle and action geometry under the same bottom gradient. Reference: `CollectionGrowthScreen.kt`, `SkeletonCollectionGrowth` and `shimmerEffect`.

### Frosted Genre Spotlight

Genre detail begins with a 28dp rounded, low-outline panel, 32dp vertical and 24dp horizontal padding, a small capsule eyebrow, oversized display title, short supporting line and capsule shuffle action. It reads monochrome and editorial rather than like an artwork card. Reference: `GenreHubScreen.kt`, `GenreHeroSection`.

### Frosted Listening Personality

Stats personality is an intentional exception to the neutral palette: a translucent card receives a low-alpha personalized gradient and a thin gradient border; the icon has a 56dp circular tinted/bordered backing. Its locked state uses an **8dp** rounded progress rail with a primary-to-tertiary gradient fill. Reference: `ListeningStatsScreen.kt`, `NightOwlPersonalityCard` and `PersonalityLockedCard`.

## Appearance, utilities and feedback

### Frosted App Icon Choice

Selection scales the option from 0.97 to 1.0 and reveals a 2dp primary-to-tertiary gradient outline over a rounded neutral card. The fill increases subtly when selected. Reference: `AppIconScreen.kt`, `AppIconOption`.

### Frosted Playlist Creation Canvas

Playlist creation places a **0.6-intensity** radial artwork-colored glow under a multi-step form. The selection state highlights chosen rows with primary at 15% alpha; the track search is a rounded translucent field. It is a feature-specific full-screen composition, not the reusable modal-sheet recipe. Reference: `CreatePlaylistFlow.kt`.

### Frosted Volume Fill Slider

The Samsung volume control is a custom 64dp capsule. A fill layer grows to the current value and clips a high-contrast volume icon at the fill edge; the track and icon colors invert appropriately for light/dark system mode. This is a distinct slider motif from the standard Frosted Media Slider. Reference: `DeviceSheet.kt`, `SamsungVolumeSlider`.

### Frosted Artist Image Fallback

Missing artist imagery resolves to a surface-variant block with a centered person glyph at half the component size. Keep the fallback within the image component so circular, square and hero crops all use consistent placeholder content. Reference: `ui/components/ArtistImage.kt`.

### Frosted Update Dialog Arrival

The update overlay dims the full screen with black at 25%, fades in over 300ms, and brings a Material card upward from a quarter-screen offset with a medium-bouncy spring. Card size animates as checking, available, downloading and ready content changes. Reference: `components/UpdaterCard.kt`.

### Frosted Modal Panel Reveal

The shared custom modal wrapper gives the Material modal sheet a 36dp top radius, black scrim at 40%, 32×4dp drag handle and a content panel capped at 75% of screen height. Its content slides 93.5dp and fades in over 400ms; on close it reverses over 350ms. A 2dp content blur resolves to zero on entry; inner content crossfades/resizes over 300ms. Reference: `ui/components/ArcModalBottomSheet.kt`.

## Image and brand motion

### Frosted Splash Mark Draw

The app mark is drawn on a **120dp** canvas from a 108-unit grid, using an open arc whose stroke width varies like a waveform. The sweep uses 1200 samples and draws then erases as progress advances. Reference: `ui/components/AnimatedSplashScreen.kt`; mark geometry is coordinated with the launcher icon asset.

### Frosted Canvas Artwork

Video art uses a zoom-cropped square texture surface. The visual alpha stays zero until the video is ready, then fades in over 600ms; Now Playing slightly overscales it over static art. Reference: `ui/components/CanvasArtworkPlayer.kt`, `ArcNowPlayingScreen.kt`.

## Reuse boundary

Global patterns (palette, surfaces, typography, corners, jelly feedback, glass and navigation) belong in the shared system. Collection cards, personality gradients, artist fallbacks, search result rows and Now Playing masks are **composed patterns**: document them for reuse, but let future products choose their content, colors and data behavior.
