# Guess the Number — Product Spec

## Overview
A simple single-page game where the player tries to guess a secret number
that the computer picks at random from a range the player defines. Numbers
in the range are shown on screen; each guess removes a number until the
player finds the winning one.

## Goals
- Fun, fast, zero-instruction game anyone can play in under a minute.
- Visual feedback: the player sees the search space shrink with every guess.

## Non-Goals
- No accounts, no leaderboards, no networking (v1 is local/offline).
- No multiplayer turn-syncing across devices.

## Core Gameplay Loop
1. **Set the range.** The player enters a minimum and maximum value
   (e.g. 1–50).
2. **Computer picks.** The computer secretly chooses a random integer
   within the range (inclusive). This number is the winning number.
3. **Board renders.** Every number in the range is displayed on screen as a
   grid of selectable tiles.
4. **Player guesses.** On each turn the player clicks one number.
   - If it's **wrong**, that tile is removed from the board and the game
     gives a hint ("too high" / "too low").
   - If it's **right**, the player wins and the round ends.
5. **Repeat** until the winning number is guessed.

## Requirements

### Functional
- **FR1** — Player can input a numeric range (min and max).
- **FR2** — Computer generates a uniformly random integer in `[min, max]`.
- **FR3** — All numbers in the range render as a grid of tiles.
- **FR4** — Clicking a tile counts as one guess (one number per turn).
- **FR5** — A wrong guess removes the tile from the board.
- **FR6** — A wrong guess shows a directional hint (higher / lower).
- **FR7** — A correct guess shows a win state and the number of guesses used.
- **FR8** — Player can start a new round (re-pick number, reset board).

### Input Validation
- Min and max must be integers, with `min < max`.
- Reject empty, non-numeric, or reversed ranges with a clear message.
- (Optional) Cap the max range size to keep the board readable
  (e.g. ≤ 200 tiles).

### Non-Functional
- Runs in any modern browser, no install.
- Board updates feel instant (< 100ms per guess).
- Responsive layout: tiles reflow on smaller screens.

## UI / Screens
- **Setup screen** — two inputs (min, max) + "Start Game" button.
- **Game board** — grid of number tiles, a guess counter, and a hint banner.
- **Win state** — celebratory message, guess count, and "Play Again".

## States
| State    | Description                                          |
|----------|------------------------------------------------------|
| Setup    | Waiting for the player to define the range.           |
| Playing  | Board is active; player is guessing.                  |
| Won      | Correct number found; round over.                     |

## Success Metrics
- Player completes a full round (range set → number found).
- Average guesses trend toward an efficient strategy over repeat plays.

## Future Ideas (Out of Scope for v1)
- Guess limit / "lives" mode.
- Score based on fewest guesses.
- Difficulty presets (small / medium / large range).
- Two-player hot-seat mode.
