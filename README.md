# BossBots Project

A single-file, in-browser **simulator** for Stake-style dice autoplay strategies. It searches for strategy cards (bet size, win chance, Stake autoplay conditions), scores them on simulated sessions, and gives you the exact settings to type into Stake ("Copy for Stake").

**Live app:** https://davionboose23-crypto.github.io/bossbots-project/ (works on phones; you can add it to your home screen)

## Important

- This is only a simulator. **No strategy can beat the house edge.** Every card pays the house edge (about 1%) on every dollar wagered. A card that ranks well just loses money more slowly or more smoothly, or finishes ahead more often over short sessions. It does not make an expected profit.
- Results are from simulated (or replayed) dice rolls. Real sessions vary.
- Everything runs locally in your browser. Learned memory is saved in your browser's localStorage and nothing is uploaded.

## What's new in v17

- **Extended holdout**: a card that beats the record on 60 fresh sessions now has to keep beating it over up to 420 paired sessions before the 5,000-session deep check. Lucky winners get dropped early, deep-check failures are down by more than half, and the search gets about 40% more generations for the same work.
- **Cushion cards**: a new Stake-valid family. It plays a lively win chance, switches to a safe win chance (usually 98%) once the session is down more than a set amount, and switches back when it recovers. In the benchmark at $10 / 1%, the average search result went from 1.17 to 1.26 (Last + green $), with 100% of bets played and 33% of sessions finishing green instead of 27%. The money lost per session is unchanged: **it does not beat the house edge**.
- **Plateau / ceiling messages** explain why no new record is showing up (e.g. at $40 / 5% the house price uses about the whole 50% Max drop).
- A first bet under $0.01 is now a red error instead of a silent $0.01 bet. Import ranks cards by Last + green $ and respects the current settings.

## Files

- `index.html`: the whole app (HTML, CSS, search engine and Web Worker code in one file)
- `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png`: home-screen icon and manifest
