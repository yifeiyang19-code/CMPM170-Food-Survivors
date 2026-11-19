# Food Survivors Playtest Report

## November 17, 2026 · 180-second QA trials

One run per prototype on the deployed GitHub Pages build ([commit `41eb8ba`](https://github.com/yifeiyang19-code/CMPM170-Food-Survivors/commit/41eb8ba7d0362c8984e024bd6e2760aed7ef069a)). Both runs used **10,000 starting HP** and reached **180.0 seconds** with the end reason `Trial complete`. The exports identify the test with `qa: "survival"` and `startingHealth: 10000`.

The operator deliberately exercised mode switches and each skill. These two runs verify time-limit settlement and telemetry. The raised health, planned inputs, and one run per mode limit what the data can say about standard-health survival, player preferences, or balance.

## P1 · Aim or Auto-fire

| Firing mode | Time | Share of trial | Shots | Hits | Kills | HP lost |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Manual | 56.9 s | 31.6% | 64 | 60 | 24 | 508 |
| Auto-fire | 123.1 s | 68.4% | 274 | 272 | 94 | 1,577 |
| Total | 180.0 s | 100% | 338 | 332 | 118 | 2,085 |

The run started in Manual and recorded **11 switches**, six to Auto-fire and five back to Manual. The first switch was at **14.77 s** with 11 enemies on the field. The final switch was at **86.27 s** with 73 enemies, after which Auto-fire stayed active for the final 93.73 s. That final stretch accounts for most of the time difference between the modes. The mode times add to 180 s, the attributed kills add to 118, and the chef finished with 7,915 HP.

[Download P1 source JSON](playtest-data/food-survivors-p1-180s-qa.json)

## P2 · Kitchen Skills

| Skill | Casts | Kills | Empty casts |
| --- | ---: | ---: | ---: |
| Knife Sweep | 1 | 1 | 0 of 1 |
| Flying Fork | 5 | 2 | 4 of 5 |
| Whisk Cyclone | 1 | 5 | 0 of 1 |
| Total | 7 | 8 | 4 of 7 |

- **Knife Sweep** killed one enemy at **3.99 s**, with one enemy within 120 px at cast time.
- **Flying Fork** was the most-used skill. The first four casts recorded zero kills. The fifth, at **38.25 s**, killed two enemies with 38 on the field and six within 120 px.
- **Whisk Cyclone** recorded five kills from the cast at **6.88 s**, the highest yield of any cast in this run. The three-second escape proxy was false for all seven casts.

All seven casts occurred in the first 38.3 seconds. The per-cast kills sum to eight and agree with the skill and settlement totals. The chef took 2,137 HP damage over 216 hits and finished with 7,863 HP.

[Download P2 source JSON](playtest-data/food-survivors-p2-180s-qa.json)

## Issues observed during playtesting

| Status | Issue | Evidence and follow-up |
| --- | --- | --- |
| Fixed and reverified | Fatal hits overstated HP lost | Two 100-HP runs reported 102 and 105 damage. The fix caps each damage event at remaining HP and uses that value in the totals. Two subsequent lethal runs each reported exactly 100 HP lost. [Fix commit](https://github.com/yifeiyang19-code/CMPM170-Food-Survivors/commit/aaa9dd60105d036dd341d4aa847c0a37848fa622) |
| Observed in earlier QA | Early deaths at standard health | An online P1 run ended at 65.9 s. A P2 run with at least one kill from each skill ended at 29.0 s. These are operator-run examples. In standard-health player sessions, compare survival time and when repeated contact damage begins. |
| Observed in full-length QA | Flying Fork frequently yielded zero kills | Four of five casts yielded zero kills and the fifth killed two enemies. Ask players where they expected the fork to travel, then compare their answer with the actual facing and hit area. |
| Observed during browser testing | Countdown slowed when the game was in the background or minimized | Progress resumed at close to normal pace once the tab was kept in the foreground. Reproduce with a timed desktop run that switches tabs and then returns, and compare elapsed wall time with the in-game timer. |

## Potential issues to verify

- **P1 · Switching may reflect habit or accidental input.** Manual is the starting mode, and Tab doubles as a switch key during play. Let participants choose when to switch, note accidental switches, and ask what prompted each intentional switch. The 11 QA switches were scheduled to exercise the control.
- **P1 · Raw kills can mislead when exposure differs.** Mode time, enemy count, and pressure changed over the run. For balance comparisons, look at kills per active minute in comparable wave windows and pair the numbers with player comments.
- **P2 · Facing and skill coverage may be hard to read while dodging.** Facing follows the last movement, so a sidestep can redirect a sweep or fork. Watch whether players notice the direction marker and can line up the fork’s 26 px strip before casting.
- **P2 · Zero kills and the escape proxy can miss useful casts.** A zero-kill result cannot explain the aim or timing error, and the three-second radius check can miss a brief escape or count enemies that approach afterward. Compare these fields with observed movement and player explanations.
- **Both modes · Later waves need standard-health coverage.** The full-length runs used 10,000 HP, and the P2 operator stopped casting after 38.3 s. Observe players in the first, middle, and final minutes to see when survivability and skill choices change.

## November 19, 2026 · Aim guides and ordinary-health pressure

The revised gameplay was deployed in [commit `8a03909`](https://github.com/yifeiyang19-code/CMPM170-Food-Survivors/commit/8a03909cd053c0a1a7b138cb1f2a7aaf3e010b81), with export build version `2026-11-19-aim-and-pressure`. Both new online runs started at **100 HP**, with no survival-QA flag. One new run per prototype was played through settlement and downloaded. This section compares them with the archived November 17 standard-health examples.

### Implemented changes

| Area | Earlier build | November 19 build |
| --- | --- | --- |
| P2 facing | Last movement sets facing | Mouse position sets aim independently of movement after the first pointer movement. Movement supplies initial keyboard-only facing. |
| P2 coverage | A facing dot before casting and a brief effect after casting | Persistent facing arrow, 120°/110 px knife sector, 500 × 26 px fork lane, and 55 px cyclone ring. Ready targets for the selected skill receive a bright outline. A cast key or hovering a skill card selects its target preview. |
| P2 collision and cooldowns | Knife 120°/110 px/6 s, fork 500 × 26 px/8 s, cyclone 55 px/2.5 s/15 s | Same dimensions and cooldowns. Target highlighting and cast collision share one geometry function. |
| Both trials, enemy generation | 0.9 s interval at start, approximately 0.47 s at 180 s, plus possible extra spawns after 65 s | 1.5 s interval at start, 0.96 s at 180 s, with 36 enemies maximum in P1 and 28 in P2 |
| Both trials, enemy movement | Pickle/egg/hotdog at 80/62/55 px/s | 60/46.5/41.25 px/s |
| Both trials, contact pressure | 7/10/12 damage and 0.7 s protection after a hit | 4/5/6 damage and 1.2 s protection after a hit |
| Export context | Earlier standard-health exports omit starting HP and build | All new exports include starting HP, build version, encounter settings, and P2 per-cast mouse/movement aim source |

### Online results at 100 starting HP

| Metric | P1 before | P1 after | P2 before | P2 after |
| --- | ---: | ---: | ---: | ---: |
| Survival | 65.9 s | 180.0 s | 29.0 s | 154.2 s |
| End reason | Chef overwhelmed | Trial complete | Chef overwhelmed | Chef overwhelmed |
| Kills | 41 | 124 | 10 | 93 |
| Remaining HP | 0 | 24 | 0 | 0 |
| HP lost | 100 | 76 | 100 | 100 |
| P1 mode switches | 7 | 3 | — | — |

The new P1 run reached the time limit at ordinary health. Its 124 kills came from Auto-fire, used for 178.6 s. Manual was exercised for 1.4 s, including switching and shooting. This provides a regression check of the P1 controls and revised shared encounter pressure.

The new P2 run lasted 125.3 s longer than the archived standard-health example and reached the final minute. It ended after 21 contact hits. Mouse aiming remained active during all 49 casts. A separate visible check confirmed that the lane rotates toward the mouse while the chef strafes sideways.

| P2 skill | Before casts | Before kills | Before empty casts | After casts | After kills | After empty casts |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Knife Sweep | 4 | 3 | 2 (50.0%) | 22 | 26 | 6 (27.3%) |
| Flying Fork | 3 | 1 | 2 (66.7%) | 18 | 46 | 0 (0.0%) |
| Whisk Cyclone | 2 | 6 | 0 (0.0%) | 9 | 21 | 2 (22.2%) |

Flying Fork had at least one kill on every cast in the new run. The lane and independent mouse aim supported lining up enemies while moving. The 26 px collision strip was retained, so the new result supports keeping the aiming changes for further player testing.

### Verification and remaining questions

Downloaded exports agree with the settlement displays. Checks reconciled duration, remaining HP, damage-event totals, P1 mode times and switches, and P2 per-cast versus per-skill kills and empty-cast counts. Local checks covered strafing with mouse aim, exact fork boundaries, cooldown rejection, cyclone immunity, the enemy cap, 180-second export, QA starting health, P1 toggling, and clearing old summary text on restart.

These runs use different inputs, enemy randomness, and wave exposure. Aiming and difficulty changed together, so their individual effects require further testing. The earlier 10,000-HP trials remain documented separately above. The new P2 run still ended before 180 seconds, and two cyclone casts produced zero kills. Next player sessions should check whether the three simultaneous range guides are easy to read, whether players understand which skill controls target highlighting, and whether the last minute remains manageable at 100 HP.

Source exports are archived with the report.

- [P1 before](playtest-data/p1-2026-11-17-normal-before.json)
- [P1 after](playtest-data/p1-2026-11-19-normal-after.json)
- [P2 before](playtest-data/p2-2026-11-17-normal-before.json)
- [P2 after](playtest-data/p2-2026-11-19-normal-after.json)
