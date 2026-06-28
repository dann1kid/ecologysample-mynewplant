# Ecology profile — `mynewplant`

This sample uses a **meadow colonizer** profile aligned with vanilla **cornflower** (`game:flower-cornflower-*`). Shapes are cornflower placeholders; ecology values are documented here and mirrored in block JSON attributes.

Third-party species are **not** in Ecosystem - Flora’s 65-species contract CSV. Balance lives on the **block type** (`ecology*` + climate attrs). The files in `species/*.reference.csv` show the equivalent row you would get for a built-in flower — useful when comparing with [`SPECIES_ECOLOGY_CSV.md`](https://github.com/dann1kid/vs-wildfarming/blob/main/docs/SPECIES_ECOLOGY_CSV.md) in the main mod.

---

## Block attributes (runtime)

| Attribute | `mynewplant` value | Notes |
|-----------|-------------------|--------|
| `ecologyParticipant` | `true` | Required |
| `ecologySpecies` | `mynewplant` | Registry / spacing id |
| `ecologyHabitat` | `Terrestrial` | Meadow flower |
| `ecologySpreadBlock` | sprout or self | See blocktypes below |
| `ecologyMatureBlock` | mature code | Sprout + mature pattern only |
| `ecologyReproduce` | `false` on **sprout** only | Sprouts do not spread until you mature them |
| `minTemp` / `maxTemp` | `3` / `23` | °C envelope |
| `minRain` / `maxRain` | `0.35` / `0.75` | Worldgen rainfall 0–1 |
| `minForest` / `maxForest` | `0.1` / `0.45` | Local forest cover |
| `ecologySpreadRate` | `1.55` | Relative vigor (× global `SpeciesSpreadRateScale` in JSON config) |
| `ecologySameSpeciesSpacing` | `2` | Chebyshev blocks |
| `ecologyOtherSpeciesSpacing` | `1` | Default vs other species |
| `ecologyMinGroundFertility` | `100` | Block fertility floor |
| `ecologyMaxGroundFertility` | `180` | Block fertility ceiling |
| `ecologyMeadowHarvest` | `whole` | Knife/scythe → drygrass when `EnableFlowerDrygrass` is on |

Per-neighbor spacing overrides (`wilddaisy=3|catmint=3`) exist only in the **contract CSV** for vanilla species — third-party mods set `ecologySameSpeciesSpacing` / `ecologyOtherSpeciesSpacing` only.

---

## Reference CSV (informational)

| File | Role |
|------|------|
| [`species/ecology.mynewplant.reference.csv`](species/ecology.mynewplant.reference.csv) | Ecology row equivalent to cornflower |
| [`species/season.mynewplant.reference.csv`](species/season.mynewplant.reference.csv) | Monthly spread/stress curves (meadow summer peak) |

These files are **not loaded** by the game. They document how a built-in species row maps to block attrs.

---

## What Ecosystem - Flora adds automatically

With default config, third-party meadow flowers still get:

- Global spread pacing from `ecosystemflora.json` (`ReproduceAttemptsPerYear`, `SpeciesSpreadRateScale`, …)
- Default meadow soil template when species is unknown to `WildPlantSoil`
- Generic seasonal spread/stress (`WildSpeciesSeason` default profile — not the cornflower-specific curve unless species id matches a built-in table)
- Competition, spacing, stress death, land claims

They do **not** get vanilla flower phenology / spread maturation unless you use a built-in `ecologySpecies` id or implement growth + mature registration yourself.

---

## Handbook

`assets/ecologysample/patches/handbook-ecology.json` adds `ecosystemHandbook` when **ecosystemflora** is present — creative inventory shows climate, spread rate, and hold hints from block attrs.

---

## Tuning checklist

1. Set climate + `ecologySpreadRate` on every reproductive block type.
2. On **sprout**: `ecologyReproduce: false`, `ecologyMatureBlock` → mature code.
3. On **mature**: `ecologySpreadBlock` → sprout (or self), `ecologyMatureBlock` → self.
4. Test on meadow soil within temp/rain; use **I** inspect or handbook with ecosystemflora loaded.
5. Compare reference CSV with vanilla `cornflower` in `assets/ecosystemflora/species/` when calibrating feel.
