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
