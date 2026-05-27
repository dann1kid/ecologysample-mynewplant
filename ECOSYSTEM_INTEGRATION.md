# Ecosystem - Flora — integration for mod authors (v3.1)

This sample targets **[Ecosystem - Flora](https://mods.vintagestory.at/ecosystemflora)** (`ecosystemflora` modid, **3.1+**).

When **`EnableThirdPartyParticipants`** is `true` in `ModConfig/ecosystemflora.json` (default), block types can join wild spread via JSON **attributes** on the block type.

Vanilla `game:` plants use built-in path rules; third-party mode is **additive**.

## Required attributes

| Attribute | Type | Purpose |
|-----------|------|---------|
| `ecologyParticipant` | bool | Must be `true`. |
| `ecologySpecies` | string | Stable id for spacing, displacement, registry. Unique per species in your mod. |
| `ecologySpreadBlock` | string | Block placed on spread: `domain:path` or path relative to this block’s domain. |
| `ecologyHabitat` | string | `Terrestrial`, `TerrestrialTree`, `ReedNearWater`, `WaterSurface`, `UnderwaterColumn` (case-insensitive). |

## Optional attributes

| Attribute | Notes |
|-----------|--------|
| `ecologyMatureBlock` | **Required on the mature block** when `ecologySpreadBlock` is a different block (e.g. sprout). On sprout, point to the mature code. |
| `ecologyReproduce` | Default `true`; `false` opts out of spread while keeping other attrs. |
| `minTemp`, `maxTemp`, `minRain`, `maxRain`, `minForest`, `maxForest` | Climate (vanilla block attrs). |
| `ecologySpreadRate`, `ecologySpreadRadius` | Per-type tuning. |
| `ecologyMinSunlight` | Sunlight (terrestrial / tree). |
| `ecologySameSpeciesSpacing`, `ecologyOtherSpeciesSpacing` | Spacing in blocks. |
| `ecologyMinGroundFertility`, `ecologyMaxGroundFertility` | Soil fertility window. |
| `ecologyMaxWaterDepth`, `ecologyMinWaterDepth`, `ecologyVerticalBlocks`, `ecologyExactWaterDepth` | Aquatic / reed tuning. |

## Who does what

| Your mod | Ecosystem - Flora |
|----------|-------------------|
| Textures, shapes, BE, growth stages, fruit, harvest | Neighbor cell search, climate, spacing, competition, seasons |
| `SetBlock` sprout → mature | `SetBlock` of `ecologySpreadBlock` |

## Disable third-party mode

`EnableThirdPartyParticipants: false` in `ecosystemflora.json` — only vanilla hardcoded paths apply.
