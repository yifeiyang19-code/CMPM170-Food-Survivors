# Food Survivors Playtesting

Record a participant code and trial order in your notes. Let players read the controls before starting. Run each trial separately for up to three minutes, then download its JSON before restarting or returning to the selector. If the same players run both trials, alternate which one they play first.

## P1 · Aim or Auto-fire

Research question: When and why do players switch between manual aiming and auto-fire?

Show movement, aim, manual fire, and the toggle. Let players decide when to switch. Record switching behavior, survival, accuracy, kills, damage, and player comments. The export tracks time in each mode and records enemy count and health at each switch. Shots, hits, and kills are credited to the mode that fired the shot.

Ask when they switched and why, which mode felt useful, and whether mode feedback was clear.

## P2 · Kitchen Skills

Show movement, the facing indicator, skill keys 1–3, and the cooldown display. Let each player decide how to use the skills. Observe adjustments to approach angle, attempts to line up or group enemies, and cyclone use under pressure.

1. Which skill did you use most, and why?
2. Which skill was easiest to understand? Which was hardest to use well?
3. Did you move, change your facing, or wait to set up a cast? Walk through an example.
4. When did you use the cyclone? Were you escaping, clearing enemies, or doing something else?
5. Did the three skills feel useful in different situations?

### Reading P2 telemetry

- Each cast records elapsed seconds, arena coordinates in pixels, facing in radians (0 points right, positive turns clockwise), total living enemies, nearby living enemies, health, and attributed kills.
- The three-second follow-up counts living enemy centers within 120 px of the chef. The escape proxy is true when a cast begins with at least one nearby enemy and the chef is alive with none nearby at the follow-up. A null follow-up means the trial ended before it could be observed. Use player comments and observations when interpreting this proxy.
- An empty cast is a completed cast with zero kills. A cyclone cut short by the trial end still counts toward casts and kills. The export gives its zero-based index in `incompleteCast` and excludes it from the empty-cast rate. A skill with zero completed casts has a null rate.
- The summary includes all skills tied for most casts, elapsed time, damage taken, and number of damage hits.

