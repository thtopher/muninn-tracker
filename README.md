# ODIN / Muninn — 30-Week Tracker

Live timeline tracker for **Project Muninn**, the semantic foundation initiative for ODIN at Starset Analytics.

**Live site:** https://thtopher.github.io/muninn-tracker/

## What This Is

A single-page dashboard that tracks the 30-week ODIN development plan from architecture through production launch. Built for screenshare meetings with David and Courtney — pull it up on a Friday call, see where we are, edit in place if priorities shift.

## Features

- **Date-aware** — auto-calculates current week, active phase, and countdown to launch
- **Countdown bar** — days left in current phase, days to launch, weeks remaining, % complete
- **Phase navigation** — P0 through P4, plus phase gates and risks views
- **Expandable week cards** — focus, tasks, and "True by Friday" gates with milestone / why / minimum bar / target
- **Live editing** — click any text field to edit in place, changes auto-save to localStorage
- **PDF export** — export any week as a clean, print-ready PDF
- **Fully static** — no build tools, no frameworks, no server. One HTML file.

## Phases

| Phase | Name | Weeks |
|-------|------|-------|
| P0 | Architecture & Guardrails | 1–4 |
| P1 | Semantic Foundation | 5–12 |
| P2 | Controlled Interaction | 13–16 |
| P3 | Platform Transition | 17–22 |
| P4 | Operationalization | 23–30 |

## Usage

Open `index.html` in a browser. That's it.

Edits persist in localStorage. Click "Reset All Edits" to revert to defaults.
