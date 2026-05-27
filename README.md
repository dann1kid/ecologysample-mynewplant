# Ecology Sample — MyNewPlant

Minimal **Vintage Story content mod** (no C#, no custom textures) showing how to register plants with **[Ecosystem - Flora](https://mods.vintagestory.at/ecosystemflora)** via JSON attributes (`ecologyParticipant`).

Use this repo as a **template**: copy blocktypes into your mod, replace `ecologysample` with your modid, add your art and growth logic.

> **Requires** [Ecosystem - Flora](https://mods.vintagestory.at/ecosystemflora) **3.1+** and `EnableThirdPartyParticipants: true` (default).

## Install (test in-game)

1. Install **ecosystemflora** from ModDB.
2. Copy this repository folder into `Mods/` (folder name can be `ecologysample-mynewplant` or `ecologysample`).
3. Launch the game → Creative → tab **Ecology sample** (or General).

## Three blocktypes

| File | Block code | Pattern |
|------|------------|---------|
| `plant-mynewplant-simple.json` | `ecologysample:plant-mynewplant-simple` | One block; spread places **the same** block. |
| `plant-mynewplant-mature.json` | `ecologysample:plant-mynewplant-mature` | Mature parent; spread places sprout. **`ecologyMatureBlock` must point to self.** |
| `plant-mynewplant-sprout.json` | `ecologysample:plant-mynewplant-sprout` | Sprout from spread; `ecologyMatureBlock` → mature. |

Shapes/textures use **vanilla cornflower** paths so the mod loads without your own assets.

**Growth sprout → mature is not implemented here** (no BlockEntity). In your mod, replace the sprout block when it matures; until then spread from that cell stays disabled.

## Docs in this repo

- **[ECOSYSTEM_INTEGRATION.md](ECOSYSTEM_INTEGRATION.md)** — attribute reference for Ecosystem - Flora.
- **[PUBLISHING.md](PUBLISHING.md)** — only if you maintain a fork; how to sync from a private monorepo.

## Copy into your mod

1. Copy `assets/ecologysample/blocktypes/plant/*.json` → `assets/<your-modid>/blocktypes/...`
2. Replace modid / block codes / `ecologySpecies`.
3. Add textures, shapes, and sprout→mature logic (BE or behaviors).

## Quick test (mature + sprout)

1. Place **mature** on meadow-like ground (temp/rain within attrs).
2. Wait for wild spread (or enable `VerboseLogging` + `ReproduceDebug` in `ecosystemflora.json`).
3. **Sprout** should appear nearby.
4. Manually set sprout to mature to verify spread from that tile, or implement growth in your mod.

## License

MIT — see [LICENSE](LICENSE). Ecosystem - Flora itself is distributed separately on ModDB.
