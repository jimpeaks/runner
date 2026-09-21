# Runner

A running schedule training assistant. Tell it your 5K pace, how many days a week
you can run, what you are training for and anything that tends to flare up, and it
lays out every session between now and race day.

**Live:** https://jimpeaks.github.io/runner/ (or open `index.html` directly - nothing to build, nothing to install).

## What it does

- **Targets** — 5K, 10K, half, marathon, or any custom distance, aimed at either a
  race date or a time frame in weeks/months.
- **Your week** — pick 3–7 running days. Name specific weekdays or let Runner choose
  them, spaced for recovery. Weekend days are preferred for the long run.
- **Real prescriptions** — every session carries its blocks, target pace ranges
  derived from your 5K time via a VDOT model, and why it is in the plan.
- **Periodisation** — base → build → sharpen → taper, with recovery weeks and a
  volume ramp capped by your current weekly distance and longest recent run.
- **Ailment-aware** — flagged niggles change the structure of the plan, not just the
  warnings: capped weekly increases, hill work swapped out, speed work delayed, the
  day after the long run kept clear.
- **Today** — opens on today's session with its full prescription, alongside
  progress for the current week and the whole block.
- **Progress** — mark sessions complete; progress persists in `localStorage`.
- **Adjust and rebuild** — change any input and regenerate; your current plan
  stays untouched until you confirm.
- **Calendar export** — a standard `.ics` file with one event per session and a
  reminder on each.
- **Units** — km or miles, switchable at any time.
- Light and dark themes, sized for a phone first.

## Hosting on GitHub Pages

1. Push this folder to a repository.
2. Settings → Pages → Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
3. Open `https://<user>.github.io/<repo>/`.

`index.html` is entirely self-contained — one file, no dependencies, no build step.
The only external request is the Google Fonts stylesheet; the page falls back to
system fonts if that is blocked.

## Structure

Everything lives in `index.html`:

| Section | What it holds |
| --- | --- |
| `2. reference data` | Ailment rules, goal presets, session-type metadata |
| `3. pace model` | VDOT model (Daniels-Gilbert): training-pace bands and race predictions |
| `4. plan generation` | Volume ramp, day assignment, session builders |
| `5. state` | `localStorage` persistence |
| `7. rendering` | Setup, schedule, paces and settings views |
| `8. calendar export` | `.ics` generation |

`generatePlan(setup)` is pure and deterministic — the same inputs always produce the
same schedule, so only the setup and the completion ticks are stored.

## Note

Runner gives training guidance, not medical advice. Pain that does not settle within
a run needs a physio, not a plan.
