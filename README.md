# The Fact Warren

A multiplication facts trainer themed around anthropomorphic forest animals and high fantasy (in the spirit of *Redwall* and *The Green Ember*). Built as a single self-contained HTML file — no build step, no backend, no dependencies.

---

> ## ⚠️ Do not rename the localStorage keys
>
> All saved progress lives under these three keys:
>
> ```
> factWarren_profiles_v1     — all recruit profiles and their fact data
> factWarren_settings_v1     — device-level settings (sound, etc.)
> factWarren_v1              — legacy single-profile save, migrated on first load
> ```
>
> Renaming any of these orphans every existing recruit's progress. It will look like a bug — recruits simply gone, ranks reset — but nothing is recoverable, because the old data is still sitting in the browser under a key nothing reads anymore.
>
> If a key ever genuinely must change, write a migration that reads the old key first. Never a straight rename.

---

## Why this exists

Built for a 4th grader who knew *most* of his times tables but had gaps in a handful of facts (especially doubles like 6×6, 7×7, 8×8). He compensated by working around them — solving 6×6 as 6×7−6 — which gets the right answer but costs seconds. On timed double-digit problems like 46×16, those seconds compound.

So this app isn't a general multiplication tutor. It's built to **find the specific facts that are slow or missing, and drill those to instant recall** while keeping mastered facts in rotation so it still plays like a game.

## How it works

**Character select** — Pick a species and name a recruit joining the Oakstone Guard. Multiple recruit profiles are supported, so both boys can each have their own progress.

**The Trial of Names (diagnostic)** — A first-run pass through the full 1–12 fact set. Every answer is logged for *both* correctness and response time. Getting it right slowly is treated differently from getting it right instantly — that distinction is the whole point.

**Training** — Adaptive practice that weights toward facts that were missed, answered slowly, or haven't been seen recently, while interleaving mastered facts so it doesn't feel like remedial drilling. A fact only graduates to "sworn strike" after repeated fast, correct answers.

**Boss rounds** — Timed rapid-fire rounds against raiders. This is the transfer skill: performing under clock pressure, the way a real timed test works.

**Elder's Riddle** — Double-digit problems broken into partial products, connecting the memorized facts back to the actual schoolwork.

**Territory map** — A 12×12 grid of every fact, color-coded from unclaimed to mastered, so progress is visible at a glance.

**Ranks, acorns, unlockables** — Points for correct answers with speed bonuses, streak multipliers, rank progression (Kit → Scout → Blade-Sworn → Guard → Warden → Legend of the Warren), and a store for companions and cloaks.

## The Warden's Ledger (parent view)

Tucked away from the main game flow. Shows the full fact grid with per-fact status and average response time, overall session stats, and an explicit list of the weakest facts — the ones actually worth a few minutes at the kitchen table.

It also holds the reset control, which permanently erases a recruit. That one is intentionally buried and confirmation-gated.

## Running it

Open the `.html` file in a browser. That's it.

For a stable setup, host it (GitHub Pages works well) and bookmark the URL rather than opening the file from disk.

## How saved progress works

Progress lives in the browser's `localStorage`, under the keys listed at the top of this file. Practical consequences beyond the rename warning:

- Progress is tied to the **origin** — the specific file path or URL it was opened from. Move or rename the file, or switch browsers, and it will look like a fresh install.
- Clearing browser data for that site wipes it.
- There is no server. Nothing syncs between devices.

If the app grows an export/import feature, that becomes the real backup path. Until then, the above is the whole story.

## Privacy

The app makes no network requests of any kind — no analytics, no remote fonts, no CDN. Everything is in the one file.

The only personal data is the recruit name typed at character select, which stays in `localStorage` on that one device and is never transmitted anywhere.

## Design constraints worth preserving

A few choices here are deliberate and easy to accidentally undo:

- **Speed over spectacle.** No artificial delays, no unskippable animations. The target player is impatient and will abandon anything sluggish.
- **Keyboard-first.** Number keys answer directly, Enter submits, Backspace corrects. The on-screen numpad is a fallback, not the primary path.
- **Sound is muted by default**, with a visible toggle and the preference remembered.
- **Tone is noble, not babyish.** Redwall-flavored copy, treating the player as capable. Condescension gets noticed instantly.
- **Misses aren't punished.** A broken streak says "hold fast" and moves on. The goal is that he opens it voluntarily.

## Stack

Vanilla HTML, CSS, and JavaScript in one file. Web Audio API for sound. No frameworks, no package manager, no build.