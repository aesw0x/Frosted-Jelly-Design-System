# Frosted Jelly accessibility

Frosted Jelly keeps its soft surfaces, artwork color and tactile motion, while making every screen usable without relying on color, blur, small text or animation. The values below are implementation guidance for products adopting the system; they are not claims that Arc Music has been audited or meets a conformance level.

## Interaction targets

- Give every touch action at least a **48 × 48dp interactive area**, including visually small Jelly icon buttons. Keep adjacent targets far enough apart to avoid overlap.
- Keep visible focus clear for keyboard, switch and D-pad navigation. Focus must remain distinct from selected, pressed and disabled states; do not communicate it with scale alone.
- Custom press feedback may replace ripple, but must still show a clear pressed state and must work with keyboard activation and accessibility actions.
- Every control needs a concise action label and the correct role/state. Announce toggle and playback state changes (for example, Play/Pause, Favorite/Remove favorite, selected tab) rather than describing the decorative icon.
- Treat decorative artwork, glows, noise and duplicate icons as decorative. Give meaningful artwork an appropriate text alternative; do not make a screen reader announce the same title twice.

## Reading and layout

- Respect the user's system font scaling. Let labels wrap or reflow; avoid fixed-height text containers and clipping. If a product offers an additional in-app text-size setting, it supplements rather than silently overrides system preferences.
- Preserve information when text grows: allow cards, rows, dialogs and bottom sheets to expand and scroll. Avoid shrinking text to preserve a fixed composition.
- Use text and icon/shape cues in addition to semantic color. Warning, success, error, selected and locked states must remain understandable in grayscale and for color-vision differences.
- Check foreground and control contrast over the final composited surface, including sampled artwork, scrims and glass. A blur or tint fallback must preserve the same readable contrast. Do not assume a translucent white/black tint guarantees contrast over every image.
- Charts and score rings need a text summary or equivalent accessible value; do not expose chart meaning only through hue, bar height or animation.

## Motion and effects

- Provide a reduced-motion path that removes or greatly reduces ambient drift, breathing glows, parallax, overscroll bounce, large travel and spring overshoot. Keep state changes immediate and understandable.
- Stop repeating animation when its surface is hidden or off-screen. Never require waiting for an animation to finish before a control works.
- Keep blur and noise nonessential. Supply an opaque or sufficiently tinted fallback, and avoid rapid flashes or high-contrast shimmer.

## Content and custom controls

- Sliders expose a label, current value, range and increment/decrement actions; support keyboard and accessibility adjustment as well as dragging.
- Play/pause, favorite, selection marks and navigation expose their current state, not only a changing glyph or color.
- Lyrics, timed words, queue changes and progress updates should not cause excessive repeated announcements. Expose the currently meaningful line/state and let the user control reading position.
- Loading skeletons are decorative. Pair them with a concise loading status when the wait is meaningful; provide empty, error and success states with a clear next action where relevant.

## Verification checklist

Before shipping an implementation, verify representative screens with:

1. TalkBack and accessibility services: labels, roles, state, traversal order, custom drawing, modal focus and announcements.
2. Keyboard, D-pad or switch navigation: every action is reachable, activation works, and focus is visible.
3. Large system text and display scaling: no clipping, hidden actions or unusable fixed-height surfaces.
4. Grayscale and high-contrast artwork: text, controls, focus, chart values and semantic states remain clear.
5. Reduced motion enabled: no essential information depends on movement; ambient loops and bounce are reduced.
6. Glass unavailable: fallback surfaces preserve component shape and legibility.

Compose supplies useful default semantics and minimum touch-target behavior for standard controls, but custom Canvas controls and custom gestures need explicit semantics and actions. See [Android Compose accessibility semantics](https://developer.android.com/develop/ui/compose/accessibility/semantics), [API accessibility defaults](https://developer.android.com/develop/ui/compose/accessibility/api-defaults) and [focus targets](https://developer.android.com/develop/ui/compose/touch-input/focus/focus-target).

## Arc Music implementation notes

Arc Music implements Frosted Jelly's Jelly press feedback and disables Material ripple and default overscroll in its shared theme. It also contains an experimental developer setting that overrides font scale. Treat that setting as an app-specific debug/testing affordance; the accessibility requirements above remain the system guidance.
