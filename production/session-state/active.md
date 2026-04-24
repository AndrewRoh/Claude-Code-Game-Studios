# Session State — REQUIEM FORMATION

**Last updated**: 2026-04-24
**Current task**: Input Manager GDD complete

<!-- STATUS -->
Epic: Pre-Production
Feature: Systems Design
Task: Input Manager GDD done — ready to author Game State Manager GDD
<!-- /STATUS -->

---

## Progress Checklist

- [x] Game concept: `design/gdd/game-concept.md`
- [x] Engine configured: Unity 6.4 (6000.4.4f1) — `CLAUDE.md`, `.claude/docs/technical-preferences.md`
- [x] Engine reference docs: `docs/engine-reference/unity/VERSION.md`
- [x] Art bible complete (9 sections): `design/art/art-bible.md`
- [x] Systems index: `design/gdd/systems-index.md` — 21 systems identified, dependencies mapped, priorities assigned
- [ ] GDDs: 1/21 — **Input Manager complete**
  - [x] Input Manager: `design/gdd/input-manager.md` — all 8 required sections + supplementary sections
  - [ ] Game State Manager — **NEXT**
  - [ ] Audio System
  - [ ] Pattern Database
  - [ ] Player Ship Controller
  - [ ] (16 more...)
- [ ] Architecture document
- [ ] Gate check (pre-production)
- [ ] Prototype: echo formation performance stress test

---

## Key Decisions Made

- **Engine**: Unity 6.4 (6000.4.4f1), URP 2D Renderer, C#
- **Review mode**: lean (directors at phase gates only)
- **Visual identity**: "The 8-bit silhouette is law; everything else is permission"
- **Color grammar**: Gold #ffd700 (absorption) / Red #ff4040 (sacrifice) / Blue-white #a0c8ff (echo)
- **Echo degradation**: 7-stage silhouette simplification; interior dissolves before outline
- **Sacrifice input**: Dedicated hold button, 0.3s threshold (Left Shift / Right Trigger at 0.35 press point)
- **Input architecture**: Poll model (Move/Fire in FixedUpdate) + Event model (Sacrifice: ChargeStarted/Confirmed/Aborted) + Direct call (Pause → GameStateManager.RequestPause())
- **Pattern absorption condition**: TBD — A/B test in prototype
- **Echo count ceiling**: 7 (performance management)

## High-Risk Items

1. **Game State Manager** — highest bottleneck risk (8 deps). Design first, review with lead-programmer before implementing.
2. **Echo Formation** — 7 simultaneous AIs = primary frame budget risk. Prototype BEFORE GDD lock.
3. **Pattern Absorption** — absorption condition must be unambiguous without a tutorial.
4. **Sacrifice during absorption** — open question in Input Manager GDD (EC2 / OQ1) — must resolve before Sacrifice System GDD.

---

## Pending Registry Work

- Register `SacrificeHoldTime = 0.3f` constant in `design/registry/entities.yaml` (flagged by systems-designer during Section C review)

---

## Files Modified This Session

| File | Purpose |
|---|---|
| `design/art/art-bible.md` | All 9 sections complete (sections 5–9 written this session) |
| `design/gdd/systems-index.md` | 21 systems, full dependency map, priority assignments |
| `design/gdd/input-manager.md` | Input Manager GDD — all sections complete |
| `production/session-state/active.md` | This file |

---

## Next Action

Run `/design-system game-state-manager` to begin the Game State Manager GDD.

Design order (remaining first 4):
1. ~~Input Manager~~ DONE
2. Game State Manager (M effort) ← **highest priority bottleneck, 8 dependents**
3. Audio System (S effort) — can parallel with Game State Manager
4. Pattern Database (M effort)
