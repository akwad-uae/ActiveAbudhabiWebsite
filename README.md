# Active Abu Dhabi — Demo Website

Mobile-first web app built to the **Avtive App.ai** Illustrator design
(1125 × 5148 px artboard), with a 3-second splash screen and a working booking
flow.

## Run it

```bash
python -m http.server 8000     # or: npx serve .
```

Then open <http://localhost:8000>. Double-clicking `index.html` also works —
everything is inlined, there is no build step and no external stylesheet or
script. The font is served from `assets/fonts/`, so it works offline too.

## Structure

```
DemoWebsite/
├── index.html              markup + CSS + JS in one file
└── assets/
    ├── README.md           which image goes where
    ├── fonts/              Acumin Variable Concept (variable OTF)
    └── images/             photos, logos and icons exported from the .ai
```

## Pages

The app is a hash-router SPA, so every screen has its own URL and the browser
back button works. The bottom navigation (Home · Events · Classes · Rewards ·
Challenges · Profile) is always visible and highlights the current section.

| Route | Screen |
|---|---|
| `#/` | Home — logo, greeting, hero slider, What's On, Classes, Venues, Partner Challenges, Rewards |
| `#/events` | What's On — all events |
| `#/event/:id` | Event detail |
| `#/classes` | All classes as a **3 × 3 scrollable grid** with sport filters |
| `#/class/:id` | Class detail — about, what's included, provider, coach, book |
| `#/venues` | All bookable venues |
| `#/venue/:id` | **Venue booking** — see below |
| `#/challenges` | All partner challenges with progress bars |
| `#/challenge/:id` | Challenge detail — goal, how it works, terms, join / leave |
| `#/rewards` | Points balance, rewards and how points work |
| `#/reward/:id` | Single reward |
| `#/profile` | Profile |

## Venue booking flow

`#/venue/:id` is the full flow:

1. **Horizontal scrollable calendar** — the next 21 days, today first.
2. **Duration** — 30 / 60 / 180 minutes.
3. **Time slots** — 30-minute increments from 06:00 to 23:30 in a scrollable
   grid. A slot is only offered when *every* 30-minute block it needs is free.
   Past slots are greyed out on today.
4. **Live summary** — venue, date, time range, duration and total.
5. **Confirm** — issues a booking reference in a confirmation sheet.

Availability is deterministic (hashed from venue + date + slot), so the same
date always shows the same free slots.

## Design notes

- **The Illustrator artboard is the source of truth.** Its 1125 px width maps
  to the 440 px phone frame, so every size in the CSS is the artboard value
  ÷ 2.556 — 60 pt section titles become 23.5 px, 36 pt body copy 14 px, and
  so on. The side gutter is tighter than the artboard's (18 px instead of 29 px).
- **Desktop** (≥ 768 px) shows the same frame inside a 440 × 953 phone shell
  (19.5:9, the artboard's proportions) that scrolls internally with the bottom
  nav pinned. If the window is shorter than the phone, the whole shell scales
  down so it always keeps its phone shape.
- **Splash** shows the ACTIVE lockup on the light background for 3 s, then
  fades (pure-CSS fallback if scripts are blocked).

### Tokens (`<style>` → `:root`)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#efefef` | page background (sampled from the .ai) |
| `--card` | `#ffffff` | cards and rows |
| `--text` | `#333333` | headings and body |
| `--muted` | `#a1a1a1` | descriptions, idle nav, dividers |
| `--accent` | `#ec6337` | brand orange — buttons, arrows, "See all", active nav |
| `--dot` | `#808080` | inactive slider dots |
| `--frame` | `440px` | phone frame width |
| `--gutter` | `18px` | side margin (14 px on screens under 360 px) |

### Typography

One font: **Acumin Variable Concept** (`assets/fonts/AcuminVariableConcept.otf`),
exactly as listed in the Illustrator package report. Weights used:

| Weight | Where |
|---|---|
| 200 ExtraLight | "Move. Live. Belong." |
| 300 Light | greeting, section subtitles, descriptions |
| 400 Regular | titles on tiles and cards, nav labels, "See all" |
| 500 Medium | hero copy, ratings |
| 600 Semibold | "Ready to move today?", "Classes In Abu Dhabi", "Venues", buttons |
| 700 Bold | name, "WHAT'S ON", "PARTNER CHALLENGES", "REWARDS", points |

## Changing the data

All content lives in plain arrays at the top of the `<script>` block:
`EVENTS`, `CLASSES`, `VENUES`, `CHALLENGES`, `REWARDS` and `USER`. Add an
object to `CLASSES` and it appears on the home rail, the 3 × 3 grid and the
filters automatically.
