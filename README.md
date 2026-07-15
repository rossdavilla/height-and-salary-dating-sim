# Height & Salary Dating Simulator

An interactive, single-page educational web app that visualizes how **height** and **income**
relate to dating-app messaging outcomes. It's a self-contained `index.html` — no build step, no
dependencies — with polished 3D-style artwork and animations.

## Features

- **Touch-friendly controls** — adjust height (5'5"–6'2") and annual salary ($20k–$300k) with
  large −/+ stepper buttons (tap or hold to repeat).
- **Reactive character** — a 3D avatar scales with height and shows one of 8 expressions
  (from sobbing to heart-eyes) based on the result.
- **Wealth that levels up** — the cash pile grows and upgrades from loose **bills → banded stacks
  → gold** as income rises, filling the phone screen.
- **Animated results** — character hop, confetti burst, falling-heart rain, and an animated
  count-up of the "messages per month" score.
- **Responsive** — works on desktop and mobile.

## Run it

Open `index.html` in any modern browser. That's it.

## Project structure

| Path | What it is |
|---|---|
| `index.html` | The entire app — HTML, CSS, and JavaScript in one file |
| `img/` | Image assets: character expressions, money tiers, hearts, logo, backgrounds |
| `DESIGN_GUIDE.md` / `.docx` | The art-direction spec used to generate the image assets |

## A note on the model

The "messages per month" figure comes from a simple illustrative formula, **not real-world data**.
This is a teaching/demonstration tool, not a statistical claim.
