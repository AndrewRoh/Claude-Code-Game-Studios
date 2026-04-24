---
name: REQUIEM FORMATION Asset Standards (Section 8)
description: Approved asset standards for art bible Section 8 — formats, naming, resolution tiers, sprite sheet philosophy, export settings, portrait specs
type: project
---

Section 8 of the art bible (Asset Standards) has been drafted and delivered for REQUIEM FORMATION.

**Why:** Establishes the production and import pipeline rules that enforce the visual identity statement "The 8-bit silhouette is law; everything else is permission."

**How to apply:** Reference this when reviewing outsourcer deliveries, specifying new asset categories, or coordinating with technical-artist on pipeline tooling.

## Key decisions recorded in Section 8

- `.aseprite` is the single source of truth for all raster art. No PSD, no Affinity, no Krita.
- Individual frame PNGs are the canonical disk state; Unity Sprite Atlas handles packing at build time.
- Five resolution tiers: T1=16px, T2=24/32px, T3=64/96px, T4=128×160px (portraits), T5=512px (env).
- No intermediate sizes. No upscaling beyond 2× native in engine.
- Export settings: 1× native, Nearest Neighbor resampling, sRGB, straight alpha, flattened layers.
- Palette validation is a gate requirement before commit — zero out-of-palette colors permitted.
- Portrait canvas: 128×160px fixed. Four expression variants minimum per pilot (neutral, resolve, pain, ghost).
- Ghost portrait variant: only Echo Blue-White (#a0c8ff) and two darkest palette colors. Gold and Red prohibited.
- Naming pattern: `[category]_[name]_[variant]_[size].[ext]` — zero-padded two-digit frame suffixes, no version numbers in filenames.
- Four Sprite Atlases: Atlas_Gameplay, Atlas_UI, Atlas_Portraits, Atlas_VFX. Background tiles and nebula patches are NOT atlased.
