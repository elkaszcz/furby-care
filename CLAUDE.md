# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Furby Care is a single-file HTML5 tamagotchi-style game where players take care of a virtual Furby pet. The entire application lives in `index.html` — no build tools, no dependencies, no bundler.

## Running

Open `index.html` in a browser. No build step required.

## Architecture

Everything is in one self-contained `index.html` with three embedded sections:

1. **CSS** — Styling, animations (bob, bounce, wiggle, squish, leave, potty-walk), and state-driven visibility toggling via classes on `#furby-wrap`
2. **Inline SVG** — The Furby character sourced from an Illustrator SVG file (multicolor variant). Key parts have IDs for animation: `#left-ear`, `#right-ear`, `#hair`, `.eye-open`, `.eye-closed`, `#sad-eyes`, `#angry-brows`, `#mouth-closed`, `#mouth-open`, `#pet-hearts`, `#suitcase-group`, `#toilet-screen`
3. **JavaScript** — Game loop, state management, audio engine, UI updates

### Game State & Mechanics

- **Stats**: `food`, `thirst`, `love` (decay over time), plus `bladderPressure` (fills when food+thirst are high)
- **Mood system**: derived from stats — `happy` / `neutral` / `sad` / `angry` — drives visual expression via CSS classes (`sad-mood`, `angry-mood`)
- **Toilet break**: when bladder exceeds 85%, Furby walks off-screen, a bathroom door appears, then Furby returns relieved
- **Leaving mechanic**: if all three main stats stay below 25% for 30s, Furby packs a suitcase and leaves (game over)

### Animation Approach

Furby state is controlled by toggling CSS classes on `#furby-wrap` (e.g., `.idle`, `.bounce`, `.eating`, `.blink`, `.sad-mood`, `.potty-walk`, `.leaving`). The SVG elements show/hide based on these parent classes — no canvas rendering.

### Audio

Synthesized via Web Audio API (`playTone` helper). Each action/mood has its own sound function (`furbyBabble`, `furbyEatSound`, `furbyDrinkSound`, `furbyPetSound`, `furbySadSound`, `furbyLeaveSound`, `furbyToiletSound`, etc.). AudioContext is lazily initialized on first user interaction.
