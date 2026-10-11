# Frosted Jelly component catalog

Names in the first column are **design-system names** for future reuse. They are not claims that Arc Music already exposes composables with those exact names. The final column maps each recipe to the existing demo implementation.

## Surfaces, navigation and media

| Frosted Jelly name | Visual contract | Arc Music implementation / where to see it |
| --- | --- | --- |
| **FrostedGlassSurface** | Rounded translucent surface; API-aware blur path; theme tint and controlled noise; tint fallback when blur is unavailable. | `ReusableComponents.kt`: `glassEffect`; Home bottom controls, mini-player and other glass surfaces. |
| **FrostedQuietCard** | A quiet translucent card using a 32dp shape and surface-container color at 55% alpha. It does not blur the content behind it; distinguish it from `FrostedGlassSurface`. | `MainActivity.kt`: `GlassCard`; stats, collection and info cards. |
| **FrostedArtworkGlow** | Oversized low-contrast radial glow with slow drift, breathing opacity and artwork-aware color. | `ReusableComponents.kt`: `AnimatedGlowBackground`; Home, welcome overlay, Canvas settings, playlist creation. |
| **FrostedNavigationBar** | Floating glass bar; moving selected capsule; filled/outline icon transition; tactile press and show/hide. | `ReusableComponents.kt`: `BottomNavigation`; `MainActivity.kt`: bottom of main destinations. |
| **FrostedMiniPlayer** | 76dp rounded frosted row with 48dp artwork, title/artist, playback actions, optional swipe-to-dismiss, immersive raised tint. | `ReusableComponents.kt`: `MiniPlayer`; appears above the bottom navigation across app screens. |
| **FrostedPlayerSheet** | Drag-linked mini/expanded/full player states; corner, position and content transitions follow expansion. | `ui/components/PlayerBottomSheet.kt`; Now Playing flow. |
| **FrostedHomeFeatureCard** | 1.3:1 full-image pager; 36dp corners; 16dp shadow; bottom text/scrim; suggestion metadata or now-playing lyrics. | `MainActivity.kt`: `HeroSection`; Home screen. |
| **FrostedImmersiveArtworkHeader** | Square full-bleed cover/photo, palette-tinted background, parallax/fade, overlaid title and actions, collapse snap. Not a separate raised card. | `ReusableComponents.kt`: immersive helpers; album, artist and playlist details screens. |
| **FrostedImmersiveActionButton** | Round Back/More controls with neutral or translucent artwork-colored background; scroll-direction visibility. | Album, artist and playlist detail headers in their respective screen files. |
| **FrostedMorphingOverflowMenu** | More icon expands from its own anchor into a rounded menu surface; rows support destructive treatment. | `ui/components/MorphingMenu.kt`; detail-page More action. |
| **FrostedModalSheet** | Arc-styled Material modal sheet with large top corners, custom reveal/blur treatment and content transition. | `ui/components/ArcModalBottomSheet.kt`; sheets throughout app. |
| **FrostedCanvasArtwork** | Square-cropped video artwork played in a zooming texture surface and faded in when ready. | `ui/components/CanvasArtworkPlayer.kt`; now-playing artwork mode. |
| **FrostedProgressIsland** | Compact global status pill that expands into details while preserving a connected surface and state transition. | `ui/components/GlobalProgressOverlay.kt`; global transfer/connection overlay. |

## Controls and content patterns

| Frosted Jelly name | Visual contract | Arc Music implementation / where to see it |
| --- | --- | --- |
| **JellyActionButton** | Material button foundation with Arc's press scale/rebound instead of ripple; use capsule geometry for primary actions. | `ui/components/JellyButtons.kt`, `ReusableComponents.kt` (`AppPrimaryButton`); Home hero, detail pages, dialogs. |
| **JellyIconButton** | Compact icon action with tactile press and app icon language. | `ui/components/JellyButtons.kt`; Back/More, player and stats controls. |
| **FrostedArtworkTile** | Cropped square artwork with rounded corners and jelly tap response. | Home artwork lists and album/artist recommendation rows. |
| **FrostedTrackRow** | Compact track information row, optional cover/number/quality state and immersive colors. | Album, artist, playlist track lists. |
| **FrostedMediaSlider** | Canvas-drawn capsule track, custom thumb and direct pointer interaction; horizontal and vertical variants. | `ui/components/CustomHorizontalSlider.kt`, `CustomVerticalSlider.kt`; player, settings/equalizer surfaces. |
| **FrostedPlayPauseGlyph** | Canvas/path morph between play and pause forms. | `ui/components/PlayPauseMorphIcon.kt`; playback controls where selected. |
| **FrostedFavoriteControl** | Heart icon with color change, glyph crossfade and small anticipatory pop. | `ui/components/FavoriteHeartIcon.kt`; artist/album favorites. |
| **FrostedSelectionMark** | Circular animated checkbox with fill, border and check transition. | `AnimationUtils.kt`; multi-select list interactions. |
| **FrostedCountBadge** | Count content with a brief growth pulse when the count increases. | `AnimationUtils.kt`; count-bearing UI where used. |
| **FrostedTrackSkeleton** | 56dp cover or number block plus two text placeholders. | `ReusableComponents.kt`; track loading states. |
| **FrostedArtworkSkeleton** | 120dp artwork placeholder with title/subtitle bars. | `ReusableComponents.kt`; grid loading states. |
| **FrostedShimmer** | Diagonal low-contrast sweep over themed skeleton placeholders. | `AnimationUtils.kt`; album, artist, playlist and share loading views. |
| **FrostedListeningTimeReadout** | Glass-card period selector and staggered character-by-character time change. | `ListeningStatsScreen.kt`: `TotalListeningTimeCard` / `PopInText`; Listening Stats. |
| **FrostedActivityChart** | Neutral capsule bars grow to represent period activity; horizontal scrolling when data is dense. | `ListeningStatsScreen.kt`: `TimelineActivitySection`; Listening Stats. |
| **FrostedArtistStatTile** | Circular artist image, name and listening time; refreshed row fades in with blur resolving away. | `ListeningStatsScreen.kt`: `TopArtistsSection`; Listening Stats. |
| **FrostedGenreCard** | Paired information cards with mapped icons and cycling Material-role container colors. | `ListeningStatsScreen.kt`: `TopGenresSection`; Listening Stats. |
| **FrostedLyricDisplay** | Playback-synchronized line and word reveal, active-line scale/glow and soft edge fades. | `ArcLyricEngine.kt`, `ArcNowPlayingScreen.kt`; Now Playing and Home hero playback state. |
| **FrostedScanPulse** | Expanding scan rings and animated device/progress states around the nearby-sharing UI. | `sharing/ShareScreen.kt`; send/share device discovery. |
| **FrostedReceiveProgressCard** | Receive-state card whose size/content/progress changes with the current receiving step. | `sharing/ReceiveScreen.kt`; receive flow. |
| **FrostedOnboardingPager** | Page content transition plus animated progress dots that widen for the selected page. | `ui/screens/OnboardingScreen.kt`; onboarding. |
| **FrostedTimerPresetControl** | Preset and end-of-track states change through animated content, selected fills and an expanding timer indicator. | `SleepTimerSheet.kt`; sleep timer. |
| **FrostedSearchField** | Rounded search field that changes its surface and icon tint when AI search mode is active; clear and AI actions use Jelly feedback. | `MainActivity.kt`: `SearchBar`; Search. |
| **FrostedLibraryPagerMarker** | Small active/inactive page dots with animated size and tint; library title changes with a vertical fade/slide. | `LibraryComponents.kt`; Library tabs. |
| **FrostedSelectionDock** | Context-aware rounded action dock for selected library items, with icon/label actions and destructive state color. | `LibraryComponents.kt`: `SelectionBottomBar`; multi-select mode. |
| **FrostedCollectionScoreRing** | Large circular health indicator with a rounded 12dp stroke, neutral track, centered score and label. | `CollectionHealthScreen.kt`; Collection Health. |
| **FrostedCollectionStoryCard** | Photo-led 300dp card with 24dp corners, top dismiss affordance and a bottom surface gradient behind copy/actions. | `CollectionGrowthScreen.kt`; New Releases, Complete Collection and Trending. |
| **FrostedPersonalityCard** | Subtle tinted glass card with a personality-specific low-alpha gradient and border; locked state has an 8dp progress track. | `ListeningStatsScreen.kt`; Listening Personality in Listening Stats. |
| **FrostedGenreSpotlight** | Large 28dp outlined panel, compact category chip, oversized title and capsule shuffle action. | `GenreHubScreen.kt`; genre detail. |
| **FrostedAppIconChoice** | Preview row with softly tinted selected background, gradient border and small selected scale. | `AppIconScreen.kt`; app appearance settings. |
| **FrostedUpdateDialog** | Centered rounded update card over a dim layer; card grows with state content. | `components/UpdaterCard.kt`; update prompt/download. |

## Arc Music visual evidence

For a screen-by-screen tour and source map, see [Arc Music reference map](../Reference/ARC_MUSIC_REFERENCE.md). Shared tokens and recipes live mainly in `app/src/main/java/com/aeswox/arcmusic/ReusableComponents.kt`, `AnimationUtils.kt`, `ui/theme/`, and `ui/components/`. Screen compositions intentionally remain app-specific; extract their reusable visual contracts, not music-domain behavior. For common dimensions and values, see the [token guide](../Tokens/TOKENS.md).

## State contract for future components

When extracting a recipe for another product, document the states that apply to it instead of specifying only its resting appearance:

| State | Required treatment |
| --- | --- |
| Resting | Surface, hierarchy, label/icon and contrast on both themes. |
| Pressed | Jelly compression/rebound plus a visible state cue; keep it clear without relying on motion alone. |
| Focused | Persistent visible focus treatment, distinct from selected and pressed. |
| Selected / active | Stable shape, text or icon cue with semantic state exposed to assistive technology. |
| Disabled | Lower emphasis without making the label unreadable; no misleading press response. |
| Loading | Preserve context and announce meaningful waits; do not make skeleton shimmer carry information. |
| Error / success | Use semantic color with a text or icon cue and a clear next step where relevant. |

Not every component needs every state. Mark inapplicable states as such and specify the interaction semantics, minimum target and expanded-text behavior for interactive controls. Follow the [accessibility guidance](../Accessibility/ACCESSIBILITY.md) for system-wide requirements.
