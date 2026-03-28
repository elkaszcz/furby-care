# Furby Care

A tamagotchi-style virtual pet game where you take care of a Furby. Built as a single HTML file with no dependencies.

## Play

Open `index.html` in a browser. No build step or server required.

## How It Works

Feed, hydrate, and pet your Furby to keep it happy. Stats decay over time, so check in regularly.

- **Food, Thirst, Love** — three core stats that slowly decrease
- **Bladder** — fills up when food and thirst are high; Furby will excuse itself to the bathroom
- **Mood** — happy, neutral, sad, or angry depending on how well you care for it
- **Leaving** — if all stats stay critically low for too long, Furby packs a suitcase and leaves

## Tech

Everything lives in a single `index.html`:

- CSS animations for movement and expressions
- Inline SVG for the Furby character
- Web Audio API for synthesized sound effects
- No frameworks, no build tools, no external dependencies
