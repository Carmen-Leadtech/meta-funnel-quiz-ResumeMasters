# Meta Funnel Quiz — production build

Self-contained quiz landing page (27→26 screens, S01–S26). Vanilla HTML/CSS/JS,
no framework, no build step. Full width / full height on mobile — no phone
frame, no design-review navigation.

## Files

- `index.html` — the whole page (markup, styles, and JS runtime inline).
- `assets/` — the 24 images/svg the page references (relative paths).

Drop both into the same folder on any static host and open `index.html`.

## Before this goes live

Three things are intentionally left as placeholders — see the `<!-- ... -->`
comment block at the very top of `index.html` for full detail:

1. **Environment (master vs stage).** Confirm which one this targets, then
   (master only) add the GTM `<noscript>` fallback right after `<body>`
   (the exact snippet is commented out at that spot).
2. **`init.js` cache-busting timestamp.** Bump the `?v=` query param on the
   first `<script>` tag in `<head>` to the current `yyyyMMddHHmmss` when you
   deploy.
3. **Final CTA destination.** Search the file for `FINAL_CTA_HREF` (near the
   top of the `<script>` block) and replace the placeholder with the real
   signup/registration URL. Also sanity-check `FINAL_CTA_NAME`, the
   `cta_name` slug Amplitude will record.

Tracking (Amplitude `view_landing` / `click_cta` / custom `view_quiz_step` /
`answer` events, the `whenAmplitudeReady` guard, no page-level click listener
on the CTA) is already wired per the team's `QUIZ_FUNNEL_SPEC.md`.

## Routing convention (per QUIZ_FUNNEL_SPEC.md)

This file is meant to be deployed at `/qz/<funnel-slug>/index.html` on
`www.resumecoach.com` (master) or `stagewww.resumecoach.com` (stage).
