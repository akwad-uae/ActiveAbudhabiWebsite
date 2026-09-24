# Assets

Everything the home screen shows was exported from **Avtive App.ai**
(the Illustrator file) — photos, partner logos, the ACTIVE lockup and every
line icon. Replace any file with your own, **keep the file name**, and the app
picks it up with no code change.

## Font — `assets/fonts/`

| File | Notes |
|---|---|
| `AcuminVariableConcept.otf` | Acumin Variable Concept, the font from the Illustrator package report. One variable file covers ExtraLight → Bold (`wght` 100–900) plus the width axis, so every weight in the design is available from the single file. Loaded by the `@font-face` rule at the top of `index.html`. |

## Brand & UI — `assets/images/`

| File | Used in | From |
|---|---|---|
| `logo.png` | Top of home, splash, confirmation sheets | ACTIVE / ABU DHABI lockup, vector in the .ai, exported with transparency |
| `icon-bell.png` | Notifications button | .ai |
| `nav-home.svg` `nav-events.svg` `nav-classes.svg` `nav-rewards.svg` `nav-challenges.svg` `nav-profile.svg` | Bottom navigation. The exact vector paths from the .ai, using `currentColor` so the same icon is grey (idle) or orange (active). They are also inlined in `index.html`; the files here are the editable copies. | .ai |
| `icon-steps.png` `icon-gift.png` `icon-star.png` `icon-points.png` | Rewards rows | .ai |
| `avatar-sajid.jpg` | Uploaded avatar — currently unused | your upload |
| `avatar-rashid.jpg` | Header avatar and profile page — the avatar from the .ai design | .ai |
| `favicon.png` `apple-touch-icon.png` `logo-mark.png` | Tab / home-screen icons | previous build |

## Photos — `assets/images/`

| File | Used in | Size |
|---|---|---|
| `hero-runner.jpg` | "Ready to move today?" slider (all three slides) | 850 × 374 |
| `event-comic-con.jpg` `event-supercup.jpg` `event-judo-grand-slam.jpg` | What's On tiles + event pages | ≤ 900 px |
| `class-swimming.jpg` `class-yoga.jpg` `class-grappling.jpg` | First three class tiles + class pages | ≤ 1000 px |
| `logo-ad-aquatics.png` `logo-the-bridge.png` `logo-uaejj.png` | Provider logos under Swimming / Yoga / Grappling | transparent |
| `venue-321-sports.jpg` `venue-adss.jpg` `venue-turf-cafe.jpg` | Venue cards + booking pages — your own photos of 321 Sports (Yas Marina Circuit), ADSS (ADNEC) and Turf Cafe | ≤ 1360 px |
| `venue-adnec.jpg` `venue-etihad-arena.jpg` `venue-mubadala-arena.jpg` | No longer used (the placeholder venues from the .ai) — kept in case you want them back | ≤ 1200 px |
| `challenge-huda.jpg` `challenge-adidas-strava.jpg` `challenge-kcal.jpg` | Partner Challenges tiles + challenge pages | ≤ 1000 px |
| `class-boxing.jpg` … `venue-corniche.jpg` | The older classes and venues that still appear on the *Classes* grid and *Venues* list | previous build |

The Illustrator file also holds larger originals (the yoga photo is 4668 px
wide, Etihad Arena 3000 px). They were downsized here so the demo loads fast;
re-export from the .ai at any size if you need sharper print assets.

## Changing the data

`EVENTS`, `CLASSES`, `VENUES`, `CHALLENGES` and `REWARDS` are plain arrays at
the top of the `<script>` block in `index.html`. Each entry's `img:` (and, for
classes, `logo:`) points at a file in this folder.
