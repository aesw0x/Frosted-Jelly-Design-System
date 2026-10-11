# Frosted Jelly layouts and scrims

These compositions are Frosted Jelly layout recipes that make the parts feel like one app. Arc Music demonstrates them in use. Measurements are system defaults; adapt for other device sizes while preserving the visual hierarchy.

## Home screen composition

The main Home content is a vertically scrolling sequence with 24dp top padding, 32dp between major sections and commonly 24dp horizontal gutters. The order is header, feature card, recently played, recommendations, collection health and a Listening Stats summary. The mini-player and navigation reserve bottom space as they appear. Scrolling uses the custom physics bounce.

### Home feature card (`FrostedHomeFeatureCard`)

- Horizontal pager with **1.3:1 aspect ratio**, **36dp corner radius**, **16dp shadow**, cropped full-bleed image.
- Side padding is 24dp. The lower copy block uses 24dp left/right, 24dp top and 12dp bottom padding.
- Title is 30sp; subtitle is body-large; 4dp separates them and 16dp precedes the action row.
- Neighboring pages scale/fade according to page offset. Suggestions advance after 4.5 seconds when not showing playback.
- Playback state overlays a surface-colored vertical scrim. The title and artist remain at the bottom; synchronized lyrics occupy the region above them.

## Immersive detail composition

Album, artist and playlist pages can switch from conventional detail layout into an immersive, artwork-led composition.

- The hero occupies a square region. Artwork sits behind the scrolling content; title and two 56dp capsule actions are aligned at the lower edge with 24dp side insets.
- Artwork is cropped to fill, shifts upward at 0.6× scroll, and dissolves as the header collapses. A 260dp bottom gradient lands on the sampled immersive background to avoid a color seam.
- The detail list is full-width while immersive; its sections regain 24dp horizontal padding. The hero/action group is separated from following content by a 52dp spacer.
- The dominant cover color becomes the page background after luminance/HSL limiting. A selected vibrant accent colors actions; text and cards use translucent white treatments over the immersive background.
- Back and More actions respond to scroll direction and can disappear while the title snaps to the action row's alignment point.

In standard detail mode, pages return to inset content. Album artwork is 280dp square with 36dp corners; artist imagery uses a 4:3 ratio and 48dp corners. Album/artist/playlist details share the general visual pattern but retain their feature-specific content.

## Bottom chrome layout

The navigation surface is 70dp tall. The main screen places it with 24dp horizontal margins and 12dp bottom spacing plus the system inset. Where a mini-player is present, the two surfaces are separated by 16dp. Bottom content padding grows with visibility so scroll content can clear the chrome.

The bottom scrim's target height is derived from visible chrome: navigation contributes 70dp, mini-player contributes 80dp to the gradient calculation, and layout breathing room is added; system bottom inset is included. Height uses a no-bounce spring, alpha fades over 220ms. The reusable gradient stops are transparent → background at 28% → background at 76% → opaque background.

## Listening Stats composition

The stats page is a physics-bounce vertical list with **24dp top/bottom breathing room** and **32dp vertical spacing** between major cards/sections. Its period readout is a 180dp glass pager card; the activity chart is a 256dp glass card. Artist images use circular 112dp crops; the period-specific chart uses neutral pill bars and horizontal scrolling when columns need more room.

The generic `GlassCard` used here is a **quiet translucent fill** (`surfaceContainer` at 55% alpha, 32dp corners), not a backdrop-blurred pane. Reserve the word “glass” in component specs for either the broad family or explicitly say which treatment is used: blur-backed glass and translucent quiet cards are different recipes in this app.

Stats includes two deliberate color exceptions to the monochrome framework: Listening Personality uses a low-alpha personality-specific gradient and border; the locked card uses a primary-to-tertiary gradient progress fill. Collection Health uses semantic status colors for warning/success rows while keeping its score ring neutral.

## Other recurring content layouts

- **Collection Growth story cards:** 300dp-tall, 24dp-rounded artwork cards. A top-right circular dismiss affordance floats above a vertical fade from transparent through surface at 80% to solid surface; title, owned/total detail and action sit in a 20dp bottom inset.
- **Genre Spotlight:** a 28dp rounded panel with a 1dp low-alpha outline, 32dp vertical / 24dp horizontal padding, small capsule eyebrow, large 52/62sp genre title and primary shuffle capsule.
- **Library multi-select:** a context-dependent bottom action dock uses 36dp corners, 24dp outer horizontal gutters, neutral raised fill, and icon-over-label actions; destructive action takes the semantic error color.
- **Search:** 32dp rounded field, 24dp internal side padding and 12dp gap from icon to input. AI mode is a 300ms color transition using a low-alpha primary fill and accent icon tint.
- **Collection Health score:** 240dp ring with a 12dp rounded stroke around a 64sp score; neutral foreground and a soft neutral track preserve the monochrome feel.

## Scrim recipes

| Name | Recipe | Purpose / Arc Music location |
| --- | --- | --- |
| **FrostedArtworkBlendScrim** | 260dp vertical blend from transparent sampled page color to opaque sampled page color. | Seamlessly lands immersive artwork onto its palette background; shared detail backdrop. |
| **FrostedStatusEdgeScrim** | At top: page color; at 45% height: same color at 72% alpha; at bottom: transparent. Whole layer alpha follows header collapse. | Keeps status icons legible after art retreats; immersive detail pages. |
| **FrostedPlaybackScrim** | Surface color with animated top alpha 0→0.4, middle alpha 0→0.8 and stop 0.35→0.6; bottom stop is opaque. | Separates Home hero playback text/lyrics from artwork. |
| **FrostedBottomChromeScrim** | Stops at 0% transparent, 25% background/0.28, 62% background/0.76 and 100% opaque. Height follows nav/mini-player visibility; alpha transition 220ms. | Supports bottom navigation and mini-player over scrolling content. |
| **FrostedPortraitFade** | Transparent at image top into opaque page background at the bottom. | Non-immersive artist hero title readability. |
| **FrostedLyricViewportFade** | Black mask fades lyrics at the top and bottom edges of the viewport. | Softens lyric lines as they scroll off-screen. |

There are also feature-specific gradients in stats cards, collection growth, update states and receive/share flows. Document those with their screen when reusing them; do not treat every vertical gradient as the same scrim token.
