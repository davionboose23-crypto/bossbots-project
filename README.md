# BossBots Project

A single-file, in-browser **simulator** for Stake-style dice autoplay strategies. It searches for strategy cards (bet size, win chance, Stake autoplay conditions), scores them on simulated sessions, and gives you the exact settings to type into Stake ("Copy for Stake").

**Live app:** https://davionboose23-crypto.github.io/bossbots-project/ (works on phones; you can add it to your home screen)

## Important

- This is only a simulator. **No strategy can beat the house edge.** Every card pays the house edge (about 1%) on every dollar wagered. A card that ranks well just loses money more slowly or more smoothly, or finishes ahead more often over short sessions. It does not make an expected profit.
- Results are from simulated (or replayed) dice rolls. Real sessions vary.
- Everything runs locally in your browser. Learned memory is saved in your browser's localStorage and nothing is uploaded.

## Files

- `index.html`: the whole app (HTML, CSS, search engine and Web Worker code in one file)
- `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png`: home-screen icon and manifest
