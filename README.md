# Food Survivors

**UCSC CMPM 170 · Team 24**  
Two three-minute experiments in a shared top-down survival arena.

## Play online

The project uses a self-contained HTML5 Canvas page at [index.html](index.html). After enabling GitHub Pages for `main` / root, play at: https://yifeiyang19-code.github.io/CMPM170-Food-Survivors/

To play locally, open `index.html` in a desktop browser. No dependencies or build step required.

Choose a trial on the home screen. The direct links are [P1](https://yifeiyang19-code.github.io/CMPM170-Food-Survivors/?mode=p1) and [P2](https://yifeiyang19-code.github.io/CMPM170-Food-Survivors/?mode=p2). Both trials end at 3:00 or when the chef runs out of health.

## P1 · Aim or Auto-fire

### Controls

- **WASD / Arrow keys:** move
- **Mouse:** aim
- **Hold left mouse button / Space:** shoot in Manual mode
- **M / Tab:** toggle between Manual and Auto-fire
- **Start / Restart button:** begin a new three-minute playtest

Manual mode shoots faster and deals more damage but requires aiming. Auto-fire targets the nearest enemy without player input, but shoots slower and deals less damage.

### Research question

**When and why will players switch between precision aiming and movement-focused auto-fire?**

The modes intentionally differ in power and control. These are starting hypotheses for testing, **not established balance**. Record whether players switch naturally, and whether they can identify the mode and its cost/benefits.

### Playtesting procedure

1. Brief players on movement, shooting, and the toggle; do not prescribe a preferred strategy.
2. Have them play a session (up to three minutes).
3. Export JSON results at the end. Note mode time, switches, shots, hits, kills, and damage taken.
4. Ask when they switched and why, which mode seemed more useful, and whether the HUD was clear.
5. Summarize surprising results and changes for the next prototype.

## P2 · Kitchen Skills

**Research question:** How do skill shapes affect where players move, how they face, how they group enemies, and when they cast?

Move with WASD or the arrow keys. Your last movement sets your facing, shown by the dot beside the chef. All three skills start ready. Cooldowns begin on cast.

| Key | Skill | Effect | Cooldown |
| --- | --- | --- | --- |
| 1 | Knife Sweep | Clears enemy centers inside a 120° forward sector with a 110 px radius | 6 s |
| 2 | Flying Fork | Pierces enemies whose centers lie in a 500 px long, 26 px wide forward strip | 8 s |
| 3 | Whisk Cyclone | Moves with the chef for 2.5 s, clearing enemies that overlap the 55 px radius and granting contact immunity | 15 s |

P2 uses skill-only combat. At the end, download the mode-labeled JSON for per-skill counts and each cast's position, facing, enemy count, kills, and follow-up pressure. P1 exports the original per-fire-mode statistics and switch events.

See the [playtest plan](docs/PLAYTEST_PLAN.md) for facilitator instructions and telemetry definitions.

## Team

- Lijin Feng — Gameplay Programming; Level Design
- Enming Li — Gameplay Programming; Playtesting
- Yifei Yang — Visual / UI Design; Sound Design

## Design references

**Gauntlet:** top-down movement, combat, and continuous enemy spawning.  
**BurgerTime:** colorful food-themed arcade aesthetics.  
All art included here is simple original placeholder rendering.

## Prototype scope

This is an exploratory gameplay test, not a complete game. Both experiments use one continuous arena, simple enemies, and an end-of-run telemetry summary. Sound and advanced visual polish are intentionally deferred.
