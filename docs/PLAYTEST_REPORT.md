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
