# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Single-file static web app (`index.html`) — a hot-seat two-player dinosaur trivia game called "Dino Duel". Players share one device; a privacy "handoff" screen hides Player 1's pick before Player 2 answers. No build system, no dependencies, no tests, no package manifest.

## Running it

Open `index.html` directly in a browser, or serve the directory with any static server (e.g. `python3 -m http.server`). There is no build, lint, or test command — visual verification in a browser is the only check.

## Architecture (everything lives in `index.html`)

Markup, inline `<style>`, and inline `<script>` share IDs and CSS hooks — read the three sections together when changing behavior.

- **Question pool** — `POOL` const (~100 items), each `{q, a:<correct>, w:[3 wrong distractors]}`. `buildGame(n)` shuffles the pool, takes `n` items, then shuffles the four options per question so the correct index varies per round.
- **Game state** — single `state` object: `names`, `scores`, `qi` (question index), `phase`, `picks`, and the per-game `questions` array. `QUESTIONS_PER_GAME` (default 15) controls round length.
- **Phase machine** — `phase` cycles `p1 → handoff → p2 → reveal` per question. Transitions toggle four `<section>` cards (`#intro`, `#game`, `#handoff`, `#results`) via the `hidden` class. Critically, `renderOptions()` is re-called when handing off to P2 — this rebuilds the `<button>` elements so the DOM carries no trace of P1's pick (the "no peeking" guarantee). Do not optimize this away.
- **CSS player theming** — `data-p="1"|"2"` attributes on score/turn-banner/final cards drive per-player colors (`--p1` amber, `--p2` teal). The active player's card gets `.active` for glow styling.
- **Keyboard** — global `keydown` maps `A/B/C/D` (or `1-4`) to options and `Enter` to advance past handoff/reveal.

## When adding questions

Append to `POOL` with the exact `{q, a, w:[w1,w2,w3]}` shape — one correct answer string and three distractor strings. Don't pre-shuffle; `buildGame` handles randomization and computes the correct index after shuffling.

## Spec Kit workflow

The repo is initialized for [Spec Kit](https://github.com/github/spec-kit) — see `.specify/` and the `/speckit-*` skills. Feature work flows: `/speckit-specify` → `/speckit-plan` → `/speckit-tasks` → `/speckit-implement`. The project constitution at `.specify/memory/constitution.md` is still an unfilled template; populate it with `/speckit-constitution` before relying on `/speckit-analyze` consistency checks.
