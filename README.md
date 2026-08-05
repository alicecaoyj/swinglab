# ⛳ Swing Lab

A personal golf fitness & simulator training tracker — one single HTML file, zero dependencies, runs entirely in your browser.

> **Note:** This is a personal project. All rights reserved — see [License](#license).

## What it does

Swing Lab is a five-tab training companion for golf-specific fitness and practice:

**📋 Plan** — A weekly scorecard of gym (🏋️), simulator (🎯) and recovery (🧘) days, with today highlighted, set-completion counts, and a week-reset button.

**✅ Today** — Tap through each set of the day's workout with big checkboxes, weight & RPE fields on gym days, and 1–5 emoji feel ratings after every exercise and for the day overall. A fairway progress bar rolls a ball toward the pin as you complete sets.

**📈 Progress** — Everything analyzed:
- Per-club line graphs: total distance, carry, launch angle, launch direction (L−/R+), back spin, side spin (L−/R+), ball speed, club speed, smash factor
- Shot-shape distribution bar chart (Straight / Draw / Push / Slice / Push Slice / Fade / Pull / Hook / Pull Hook)
- 🛤️ **Shot Path Tracker** — top-down flight paths computed with pure physics from logged data (no AI), with distance arcs and tap-to-inspect shots
- 💪 Exercise Feel Tracker — every rating logged over time, worst-rated exercises surfaced first
- Editable profile (name, height, weight, goals)
- 🤖 AI Coach — sends all data to Claude to redesign next week's exercises while keeping the schedule fixed (with backup & undo)

**🥅 Putt** — Tap-to-log putting practice: set a start point, log 10 balls' finish positions on an SVG green with dashed 5/10/15/20-yd rings. Made putts nest into the cup. Rounds auto-save; export the green as PNG.

**🪁 Chip** — Same flow for chipping: plant a pin anywhere, the view pans to center it, then log 10 chips against dashed 10–50-yd rings.

**🎯 Simulator logging** — On sim days: club, distances, launch angle & direction (L/R), spins (L/R), ball/club speed with **auto-calculated smash factor** (ball ÷ club), shot shape picked from a clickable trajectory-fan graphic, plus 📸 photo capture that reads your launch-monitor screen with AI vision.

## Getting started

No build, no install:

1. Download `golf-tracker.html`
2. Open it in any modern browser (Chrome, Safari, Edge, Firefox — desktop or mobile)
3. Start training

To host it with **GitHub Pages**: Settings → Pages → deploy from `main`, then visit
`https://<username>.github.io/swinglab/golf-tracker.html`

## Data & privacy

- All data is stored in your browser's **localStorage** on your device under `golfTracker_*` keys — nothing is uploaded anywhere, except when you actively use the AI features.
- Data persists until you clear that browser's site data. It does **not** sync between devices or browsers.
- **Back up regularly** via the Progress tab: Export All Data (JSON) and Export Sim Shots (CSV, opens in Excel). The putting/chipping greens export as PNG images.

## AI features

The one-click **AI Coach** and **photo capture** buttons call the Anthropic API without a key, which only works when the app runs inside Claude.ai (as a published artifact). When the file is opened locally or hosted on GitHub Pages, those buttons degrade gracefully — use the built-in **Copy Prompt / Paste Reply** workflow instead: the app generates a complete prompt with all your data baked in, you paste it into any Claude chat, and paste the JSON reply back to apply it.

Everything else — tracking, graphs, path physics, putting/chipping, exports — works fully offline with no AI.

## Tech notes

- Single file: vanilla HTML + CSS + JavaScript, no external libraries, no build step
- All charts (line, bar, shot paths, greens) are hand-rolled SVG
- Shot paths use a deterministic top-down flight model: start line from launch direction, lateral curve ≈ `2.24e-7 × sideSpin(rpm) × carry(yds)²`, roll from total−carry or estimated from back spin & launch angle
- Destructive actions use a tap-twice confirmation (no `window.confirm`, which some sandboxes block)
- localStorage falls back to in-memory storage where it's unavailable, so the app never crashes

## License

Copyright © 2026 Alice Cao. **All rights reserved.**

This code is published for personal portfolio purposes only. No permission is granted to use, copy, modify, or distribute this software. See [LICENSE](LICENSE).
