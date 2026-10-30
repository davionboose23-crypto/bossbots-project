# BossBots Project

A single-file, in-browser **simulator** for Stake-style dice autoplay strategies. It searches for strategy cards (bet size, win chance, Stake autoplay conditions), scores them on simulated sessions, and gives you the exact settings to type into Stake ("Copy for Stake").

**Live app:** https://davionboose23-crypto.github.io/bossbots-project/ (works on phones; you can add it to your home screen)

## Important

- This is only a simulator. **No strategy can beat the house edge.** Every card pays the house edge (about 1%) on every dollar wagered. A card that ranks well just loses money more slowly or more smoothly, or finishes ahead more often over short sessions. It does not make an expected profit.
- Results are from simulated (or replayed) dice rolls. Real sessions vary.
- Everything runs locally in your browser. Learned memory is saved in your browser's localStorage and nothing is uploaded.

## What's new in v17.1 — only valid cards shown, goal limits kept, side cards simplified

Same benchmark as v17 (`bench/v17`: 8 seeds, 300,000 sessions per search, every result scored by the frozen v17 scorer on 3,000 fixed sessions; notes in `bench/v17.1/PROGRESS.md`).

| | v17 | v17.1 |
|---|---|---|
| $10 / 1%: final score (sd) | 1.256 (0.009) | 1.254 (0.015), paired −0.002 ± 0.004: same |
| $40 / 5%: final score (sd) | 0.695 (0.006) | 0.695 (0.004), same |
| Shown cards (list, board, elites, side list; one 20-generation run) that fail a 1,000-session Stake check | 34 of 1,125 | 4 of 955 |
| Risky-action cards among them | 175 | 26 (unchecked ones wait off the list) |
| Mutated / crossed cards with a target or stop-loss out of range, duplicated or below another condition | 3.5% | 0% |
| Wall time per search ($10 / $40) | 113 s / 57 s | 118 s / 71 s |

1. **Validity gate for every shown card.** Cards with a risky action (add to / subtract from win chance, lower the bet) pass a quick 8-session check while searching; about 15% of those failed the longer 200-session check that the detail panel uses, and they could still appear in the list, the Goals board, the family elites or the side list. They are now re-checked on 200 sessions before they are shown (the list spends at most one new long check every 4 generations, best-ranked first, so it does not slow the search much; unchecked risky cards just wait).
2. **Auto-Simplify for side cards.** One Goals-board or side-list card is simplified every 25 generations with the same rules as the top card (never fired / made no difference), kept only if it is as good on 120 fresh paired sessions with no more ruin, breach or 95th-percentile drop. The detail panel shows what was removed. Every 10 generations cost about +50% wall time at $40 / 5%, so it is throttled.
3. **Target / stop-loss limits survive mutation.** After every mutate, cross and nudge, a profit target and stop-loss stay inside their ranges, whole cents, one of each, at the top.
4. **Multiplier shown the way Stake shows it**: 4 decimals, cut not rounded (7% → 14.1428×).

Tried and not shipped (no gain beyond noise): a smooth drop-penalty ramp instead of the +0.5 cliff (`K.DROP_SMOOTH` knob, default off: k = 8 gave +0.002 / +0.003, k = 25 gave −0.006 / +0.002, all under one standard error); Min gain 0.25% or 1% instead of 0.5% (−0.003 / +0.001 and 0.000 / −0.001); twice as many Cushion cards (+0.002 / +0.001, under one se). None of this beats the house edge: net per session is unchanged (−$1.03 at $10 / 1%).

## What's new in v17

- **Extended holdout**: a card that beats the record on 60 fresh sessions now has to keep beating it over up to 420 paired sessions before the 5,000-session deep check. Lucky winners get dropped early, deep-check failures are down by more than half, and the search gets about 40% more generations for the same work.
- **Cushion cards**: a new Stake-valid family. It plays a lively win chance, switches to a safe win chance (usually 98%) once the session is down more than a set amount, and switches back when it recovers. In the benchmark at $10 / 1%, the average search result went from 1.17 to 1.26 (Last + green $), with 100% of bets played and 33% of sessions finishing green instead of 27%. The money lost per session is unchanged: **it does not beat the house edge**.
- **Plateau / ceiling messages** explain why no new record is showing up (e.g. at $40 / 5% the house price uses about the whole 50% Max drop).
- A first bet under $0.01 is now a red error instead of a silent $0.01 bet. Import ranks cards by Last + green $ and respects the current settings.

## Files

- `index.html`: the whole app (HTML, CSS, search engine and Web Worker code in one file)
- `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png`: home-screen icon and manifest
