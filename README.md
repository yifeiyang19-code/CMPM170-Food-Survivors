# Food Survivors — Prototype #1

**UCSC CMPM 170 · Team 24**  
**Design experiment:** manual aiming versus automatic fire in a top-down arcade survival game.

## Play online

The project uses a self-contained HTML5 Canvas page at [index.html](index.html). After enabling GitHub Pages for `main` / root, play at: https://yifeiyang19-code.github.io/CMPM170-Food-Survivors/

To play locally, open `index.html` in a desktop browser. No dependencies or build step required.

## Controls

- **WASD / Arrow keys:** move
- **Mouse:** aim
- **Hold left mouse button / Space:** shoot in Manual mode
- **M / Tab:** toggle between Manual and Auto-fire
- **Start / Restart button:** begin a new three-minute playtest

Manual mode shoots faster and deals more damage but requires aiming. Auto-fire targets the nearest enemy without player input, but shoots slower and deals less damage.

## Research question

**When and why will players switch between precision aiming and movement-focused auto-fire?**

The modes intentionally differ in power and control. These are starting hypotheses for testing, **not established balance**. Record whether players switch naturally, and whether they can identify the mode and its cost/benefits.

## Playtesting procedure

1. Brief players on movement, shooting, and the toggle; do not prescribe a preferred strategy.
2. Have them play a session (up to three minutes).
3. Export JSON results at the end. Note mode time, switches, shots, hits, kills, and damage taken.
4. Ask when they switched and why, which mode seemed more useful, and whether the HUD was clear.
5. Summarize surprising results and changes for the next prototype.

See [Playtest plan](docs/PLAYTEST_PLAN.md).

## Team

- Lijin Feng — Gameplay Programming; Level Design
- Enming Li — Gameplay Programming; Playtesting
- Yifei Yang — Visual / UI Design; Sound Design

## Design references

**Gauntlet:** top-down movement, combat, and continuous enemy spawning.  
**BurgerTime:** colorful food-themed arcade aesthetics.  
All art included here is simple original placeholder rendering.

## Prototype scope

This is an exploratory gameplay test, not a complete game. The current version has one continuous arena, simple enemies, and an end-of-run telemetry summary. Sound and advanced visual polish are intentionally deferred.
