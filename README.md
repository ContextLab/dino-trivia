# Dino Duel 🦖

A two-player, hot-seat dinosaur trivia game. Take turns on a single device — each round, Player 1 locks in their pick, hands the device over (a "no peeking" handoff screen hides their answer), then Player 2 answers. Fifteen questions drawn fresh from a pool of 100+ for a different dig every game.

**▶ Play it: <https://context-lab.com/dino-trivia/>**

## How to play

1. Enter both players' names and tap **Begin the Dig**.
2. Player 1 picks an answer.
3. Hand the device to Player 2 — their pick is hidden behind a lock screen.
4. Player 2 picks. Both answers are revealed and scores update.
5. After 15 questions, the player with the most correct wins. Ties get dual crowns.

Keyboard shortcuts: `A` `B` `C` `D` (or `1` `2` `3` `4`) to answer, `Enter` to advance past the handoff and reveal screens.

## Running locally

It's a single static HTML file with no dependencies and no build step.

```sh
# Easiest — just open it
open index.html

# Or serve it (Google Fonts preconnect behaves better over http://)
python3 -m http.server
# then visit http://localhost:8000
```

## Adding questions

Append entries to the `POOL` array in [`index.html`](index.html) using this shape:

```js
{ q: "Your question text", a: "Correct answer", w: ["Wrong 1", "Wrong 2", "Wrong 3"] }
```

The game shuffles the pool, draws 15 per round, and randomizes option order — no need to pre-shuffle or vary the correct slot.

## Tech

Vanilla HTML, CSS, and JavaScript. No frameworks, no bundler, no dependencies. Hosted on GitHub Pages directly from `main`.

## License

[MIT](LICENSE) © Contextual Dynamics Laboratory
