# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A collection of browser-based games hosted on GitHub Pages at https://ebfeinstein.github.io/games/. Each game is a fully self-contained single HTML file — no build step, no dependencies, no bundler.

## Running locally

Open any `.html` file directly in a browser. No server required.

## Architecture

Each game is structured as a single `.html` file with three inline sections: CSS in `<style>`, markup in `<body>`, and JavaScript in a `<script>` block at the bottom. All game state lives in module-level `let` variables; UI is re-rendered by clearing and rebuilding the DOM on every state change.

### Game-specific notes

**hangman.html** — Word list is a hardcoded array at the top of the script. Six body parts map to `maxMistakes = 6`. SVG parts are toggled via `.visible` class. Supports physical keyboard input via `keydown`.

**tictactoe.html** — `WINS` is a hardcoded array of all 8 winning index combos on a flat 9-element board array. vs-Computer mode uses a full minimax AI (unbeatable). `scores` object persists across `init()` calls within a session.

**tictactoe3d.html** — 4×4×4 board stored as a flat 64-element array; `cell(l,r,c)` converts layer/row/col to index. 76 winning lines are generated once at load time from 13 direction vectors. vs-AI uses a heuristic scorer (not minimax — too expensive for 64 cells). AI difficulty is intentionally tuned so the player wins ~75% of the time: 30% random moves, win check skipped 50% of the time, block check skipped 75% of the time, heavy random noise (`Math.random() * 100`) added to cell scores.

## Style conventions

- Dark color themes using CSS custom properties (`--bg`, `--panel`, `--text`, `--accent`, etc.)
- No external fonts, icons, or libraries — everything is inline
- Responsive via CSS Grid and `@media` breakpoints
