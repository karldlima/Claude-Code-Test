# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Git workflow

Commit and push work to GitHub regularly as tasks are completed. After any meaningful change, stage the relevant files, create a focused commit, and push to the remote. For larger features or fixes, open a PR rather than pushing directly to `main`.

## Running the games

Both games are standalone HTML files — open them directly in a browser. No build step, no dependencies, no server required.

```
open tictactoe.html
open shooter.html
```

## Architecture

The repo contains two self-contained browser games, each a single HTML file with inline CSS and JS.

**`tictactoe.html`** — Classic two-player Tic Tac Toe. State is three module-level variables (`board`, `current`, `over`) plus a `scores` object. All logic lives in a `checkWin()` function and click listeners on `.cell` elements. `init()` resets the board without resetting scores.

**`shooter.html`** — Top-down arena shooter rendered on a `<canvas>` (800×600). Uses a fixed-timestep `requestAnimationFrame` loop with a `gameState` string (`MENU | PLAYING | LEVEL_COMPLETE | GAME_OVER`) as the top-level state machine. Entities are ES6 classes (`Player`, `Enemy`, `Bullet`, `Particle`) that each have `update(dt)` and `draw()` methods. `ENEMY_DEFS` defines the three enemy archetypes; `LEVELS` defines wave composition per level — beyond the last defined level, enemy counts scale via an `extra` multiplier. Dead entities are removed each frame by filtering the arrays in-place. Screen shake, invincibility frames, and particle effects are driven by timers decremented by `dt`.
