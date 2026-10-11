# Frosted Jelly responsive layouts

Arc Music demonstrates Frosted Jelly in a phone-oriented layout. Preserve the system's visual hierarchy as the available **app window** changes; do not stretch a phone layout across a tablet or assume a device's physical screen equals the space the app receives.

## Layout rules

- Base layout choices on the current window width and height, including split-screen and resizable windows. Re-evaluate when the window or fold posture changes.
- Keep a readable content measure on wide windows. Center page content or use a bounded content column instead of stretching text, track rows and forms edge-to-edge.
- Use available width to show more useful content: for example, a persistent navigation rail and a list/detail or two-column collection layout. Keep detail content from becoming excessively wide.
- On compact windows, retain the established 24dp page gutter where it fits; reduce outer margins only when needed to preserve usable content width. Avoid horizontal scrolling for ordinary text and controls.
- Use a single-column flow when height is constrained, such as landscape phones or short split-screen windows. Make bottom controls and sheets scrollable or reposition them so they do not cover content.
- Keep artwork's intended crop and aspect ratio. Scale artwork containers to the layout; do not let fixed 160dp tiles, 300dp story cards or full-screen immersive headers dictate the overall breakpoint.
- Respect system insets, gesture navigation and fold hinges. Do not place a focal control or continuous artwork composition across a hinge.
- At larger text settings, allow the layout to reflow independently of its width class. Breakpoints do not replace content-driven sizing.

## Proposed width classes

Use Android window size classes as the starting points for Frosted Jelly's adaptive layout decisions:

| Available window width | Suggested composition |
| --- | --- |
| Compact: under 600dp | Phone composition; bottom navigation; one content column. |
| Medium: 600–839dp | Wider gutters and bounded content; consider navigation rail and two-pane layouts where the content benefits. |
| Expanded: 840dp and above | Navigation rail or permanent navigation; list/detail or multi-column collections; cap text and detail-column width. |

Choose layout changes based on whether the content remains usable, not on a device name. Height matters too: compact height should prioritize the current task and allow secondary content to scroll.

## Frosted Jelly patterns to adapt

- **Home:** retain the featured artwork hierarchy, but bound the page width and increase the number of collection columns as room allows.
- **Album/artist/playlist detail:** keep the large-artwork-to-content relationship. On wide layouts, place artwork and metadata alongside a bounded track list rather than enlarging the hero indefinitely.
- **Now Playing:** retain the cover as the focal point, but scale it to available height and place queue/lyrics beside it when there is enough width. Short windows need a compact control arrangement.
- **Navigation and mini-player:** use the floating bottom bar and mini-player on compact windows. On wider layouts, consider a rail and persistent side/bottom player region so content has room; preserve the same selection and playback hierarchy.
- **Sheets and dialogs:** constrain maximum width on wide windows and preserve modal focus. Reflow long actions rather than making a phone-width sheet fill a tablet.

## Verification matrix

Review at least a compact portrait window, compact landscape/short-height window, medium width, expanded width, and a resizable split-screen window. Repeat representative checks with large system text, a foldable hinge/posture, and the keyboard. Look for clipped text, stretched artwork, stranded actions, excessive line length, awkward empty space and controls hidden behind system insets.

Android's guidance bases adaptation on app-window size classes and calls out resizable windows and multi-window behavior. See [adaptive do's and don'ts](https://developer.android.com/develop/adaptive-apps/guides/adaptive-dos-and-donts) and [Compose window size classes](https://developer.android.com/develop/adaptive-apps/guides/use-window-size-classes).
