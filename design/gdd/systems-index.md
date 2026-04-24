# Systems Index: REQUIEM FORMATION

> **Status**: Approved
> **Created**: 2026-04-24
> **Last Updated**: 2026-04-24
> **Source Concept**: design/gdd/game-concept.md

---

## Overview

REQUIEM FORMATION is a vertical scroll shoot 'em up whose systems cluster around three interconnected mechanical pillars: **pattern absorption** (reading and absorbing enemy attack patterns), **strategic sacrifice** (intentional self-destruction to create echo ghosts), and **echo formation** (a persistent ghost fleet that auto-attacks using absorbed patterns). The game does not use procedural generation, multiplayer, or open-world systems — it is a handcrafted, linear 5-chapter experience where every system exists to deepen the sacrifice-and-formation loop.

Foundation systems (input, state management, audio, pattern data) must be stable before any of the game's three differentiating mechanics can be built. The Pattern Database is the single most important data design artifact — it defines the data contract for all 12–18 patterns, and both Echo Formation and Boss System read from it. Game State Manager is the highest-risk bottleneck (8 systems depend on it). Echo Formation is the most design-complex feature system: it must handle up to 7 simultaneous ghost AIs, each playing back a unique absorbed pattern, while maintaining visual degradation across 7 opacity stages.

Core pillars: 희생은 선택이다 / 잔상이 이야기다 / 흐름 속의 깊이 / 모던 레트로

---

## Systems Enumeration

| # | System Name | Category | Priority | Status | Design Doc | Depends On |
|---|---|---|---|---|---|---|
| 1 | Input Manager | Core | MVP | Design Complete | `design/gdd/input-manager.md` | — |
| 2 | Game State Manager | Core | MVP | Not Started | — | — |
| 3 | Audio System | Core | MVP | Not Started | — | — |
| 4 | Pattern Database | Core | MVP | Not Started | — | — |
| 5 | Player Ship Controller | Core | MVP | Not Started | — | Input Manager, Game State Manager |
| 6 | Player Health System | Core | MVP | Not Started | — | Game State Manager |
| 7 | Collision Detection (inferred) | Core | MVP | Not Started | — | — |
| 8 | Enemy System | Gameplay | MVP | Not Started | — | Game State Manager, Pattern Database |
| 9 | Score System (inferred) | Core | Vertical Slice | Not Started | — | Game State Manager |
| 10 | Pattern Absorption | Gameplay | MVP | Not Started | — | Player Ship Controller, Collision Detection, Pattern Database, Enemy System |
| 11 | Strategic Sacrifice | Gameplay | MVP | Not Started | — | Player Ship Controller, Player Health System, Pattern Absorption |
| 12 | Echo Formation | Gameplay | MVP | Not Started | — | Strategic Sacrifice, Pattern Database, Input Manager |
| 13 | Boss System (inferred) | Gameplay | Vertical Slice | Not Started | — | Enemy System, Pattern Database |
| 14 | Final Boss (Final Echo) | Gameplay | Vertical Slice | Not Started | — | Boss System, Echo Formation |
| 15 | Chapter Manager (inferred) | Gameplay | MVP | Not Started | — | Enemy System, Player Health System, Game State Manager, Save System |
| 16 | Save System (inferred) | Persistence | MVP | Not Started | — | Game State Manager |
| 17 | HUD (inferred) | UI | MVP | Not Started | — | Player Health System, Echo Formation, Pattern Absorption, Boss System, Score System |
| 18 | Story Screen System (inferred) | Narrative | MVP | Not Started | — | Chapter Manager, Game State Manager, Audio System |
| 19 | Menu System (inferred) | UI | Vertical Slice | Not Started | — | Game State Manager, Save System, Chapter Manager |
| 20 | VFX System (inferred) | Core | Alpha | Not Started | — | Strategic Sacrifice, Pattern Absorption, Echo Formation, Audio System |
| 21 | Settings System (inferred) | Meta | Full Vision | Not Started | — | Audio System, Input Manager, Menu System |

---

## Categories

| Category | Description | Systems in This Game |
|---|---|---|
| **Core** | Foundation systems everything depends on | Input Manager, Game State Manager, Audio System, Pattern Database, Player Ship Controller, Player Health System, Collision Detection, Score System, VFX System |
| **Gameplay** | The systems that make the game fun | Pattern Absorption, Strategic Sacrifice, Echo Formation, Enemy System, Boss System, Final Boss, Chapter Manager |
| **Persistence** | Save state and continuity | Save System |
| **UI** | Player-facing information displays | HUD, Menu System |
| **Narrative** | Story and dialogue delivery | Story Screen System |
| **Meta** | Systems outside the core game loop | Settings System |

---

## Priority Tiers

| Tier | Definition | Target Milestone | Design Urgency |
|---|---|---|---|
| **MVP** | Required for the core loop hypothesis test — "Does strategic sacrifice + echo creation sustain 30+ min sessions?" Chapters 1–2, 2 bosses, 3 patterns, 1 echo. | First playable prototype (weeks 1–4) | Design FIRST |
| **Vertical Slice** | Required for a complete emotional experience — Chapter 3, full echo fleet (up to 7), narrative beats, chapter select. | Vertical slice / demo (weeks 5–7) | Design SECOND |
| **Alpha** | All features present in rough form — all 5 chapters, all 12–18 patterns, VFX pass, full menu. | Alpha milestone (weeks 8–10) | Design THIRD |
| **Full Vision** | Polish, accessibility options, settings, content-complete. | Beta / Release (weeks 11–14) | Design as needed |

---

## Dependency Map

### Foundation Layer (no dependencies)

1. **Input Manager** — every system that needs player input reads from here; must be stable before any interactive system is built
2. **Game State Manager** — 8 systems depend on it; defines the states (Title, Playing, Paused, ChapterClear, GameOver) that all other systems must query
3. **Audio System** — needed even with temp sounds; sacrifice and absorption moments cannot be emotionally playtested without audio feedback
4. **Pattern Database** — data asset; defines the data contract for all 12–18 patterns; Pattern Absorption, Echo Formation, and Boss System all read from it

### Core Layer (depends on Foundation)

1. **Player Ship Controller** — depends on: Input Manager, Game State Manager
2. **Player Health System** — depends on: Game State Manager
3. **Collision Detection** — framework connecting Player Ship, Enemy bullets, and enemy ships; no explicit deps but must be built before Feature systems can detect events
4. **Enemy System** — depends on: Game State Manager, Pattern Database
5. **Score System** — depends on: Game State Manager

### Feature Layer (depends on Core)

1. **Pattern Absorption** — depends on: Player Ship Controller, Collision Detection, Pattern Database, Enemy System
2. **Strategic Sacrifice** — depends on: Player Ship Controller, Player Health System, Pattern Absorption
3. **Echo Formation** — depends on: Strategic Sacrifice, Pattern Database, Input Manager
4. **Boss System** — depends on: Enemy System, Pattern Database
5. **Final Boss** — depends on: Boss System, Echo Formation
6. **Chapter Manager** — depends on: Enemy System, Player Health System, Game State Manager, Save System
7. **Save System** — depends on: Game State Manager

### Presentation Layer (depends on Feature)

1. **HUD** — depends on: Player Health System, Echo Formation, Pattern Absorption, Boss System, Score System
2. **Story Screen System** — depends on: Chapter Manager, Game State Manager, Audio System
3. **Menu System** — depends on: Game State Manager, Save System, Chapter Manager

### Polish Layer (depends on Presentation)

1. **VFX System** — depends on: Strategic Sacrifice, Pattern Absorption, Echo Formation, Audio System
2. **Settings System** — depends on: Audio System, Input Manager, Menu System

---

## Recommended Design Order

Design these systems in order. Independent systems at the same layer can be designed in parallel.

| Order | System | Priority | Layer | Est. Effort |
|---|---|---|---|---|
| 1 | Input Manager | MVP | Foundation | S |
| 2 | Game State Manager | MVP | Foundation | M |
| 3 | Audio System | MVP | Foundation | S |
| 4 | Pattern Database | MVP | Foundation | M |
| 5 | Player Ship Controller | MVP | Core | S |
| 6 | Player Health System | MVP | Core | S |
| 7 | Collision Detection | MVP | Core | S |
| 8 | Enemy System | MVP | Core | M |
| 9 | Pattern Absorption | MVP | Feature | L |
| 10 | Strategic Sacrifice | MVP | Feature | M |
| 11 | Echo Formation | MVP | Feature | L |
| 12 | Chapter Manager | MVP | Feature | M |
| 13 | Save System | MVP | Feature | S |
| 14 | HUD | MVP | Presentation | M |
| 15 | Story Screen System | MVP | Presentation | M |
| 16 | Score System | VS | Core | S |
| 17 | Boss System | VS | Feature | M |
| 18 | Final Boss | VS | Feature | L |
| 19 | Menu System | VS | Presentation | M |
| 20 | VFX System | Alpha | Polish | M |
| 21 | Settings System | Full Vision | Polish | S |

*Effort: S = 1 session (~2hrs), M = 2–3 sessions, L = 4+ sessions. Parallel design allowed at same layer and same priority.*

**First 3 to design**: Input Manager → Game State Manager → Pattern Database (in parallel with Game State Manager once foundation context is set).

---

## Circular Dependencies

None found. The dependency graph is acyclic.

The closest structural tension: **Chapter Manager** depends on **Save System**, and **Save System** depends on **Game State Manager**, which must understand chapter state to know when to save. This is not a circle — it resolves as: Game State Manager provides state events; Save System listens and persists; Chapter Manager reads persisted state at load. The data flows one direction.

---

## High-Risk Systems

| System | Risk Type | Risk Description | Mitigation |
|---|---|---|---|
| **Game State Manager** | Design | 8 systems depend on its state contract. If the state machine is incorrectly designed (wrong states, missing transitions, bad ownership model), every dependent system requires rework. | Design the state machine as the **first GDD authored**. Include all state transitions explicitly — do not leave "and so on" gaps. Review with lead-programmer before implementing. |
| **Echo Formation** | Technical | Up to 7 simultaneous echo AIs each playing back an absorbed pattern. At 60fps with 7 echos + heavy bullet patterns on screen simultaneously, this is the primary frame budget risk. | **Prototype first** — build a stress test with 7 dummy echoes + 200 bullets before full GDD implementation. Performance budget: ≤3ms CPU per frame for all echo updates combined. Consider DOTS Jobs if profile shows bottleneck. |
| **Pattern Absorption** | Design | The absorption condition (what exactly triggers "this kill counts as absorption?") must be unambiguous and telegraphed to the player without requiring a tutorial. If the condition is opaque, the core loop breaks. | Prototype absorption conditions early. A/B test at least 2 condition models (proximity + kill vs. specific kill input vs. bullet-nullification-kill). |
| **Strategic Sacrifice** | Design | The game's emotional thesis requires the player to *feel* sacrifice as a choice, not an accident. The input model (dedicated button? context-sensitive?) must be playtested — wrong UX here undermines Pillar 1. | See Open Question in game-concept.md: "전용 버튼인가, 맥락적 액션인가?" — resolve via prototype A/B test before GDD lock. |
| **Pattern Database** | Scope | 12–18 patterns is a significant content design task. Each pattern needs: spawn behavior, absorption condition, echo playback behavior, and visual spec. Scope can balloon if not constrained. | Design 3 patterns at MVP depth (full GDD), then validate the data schema before authoring the remaining 9–15. Add patterns in batches, not one-by-one. |

---

## Progress Tracker

| Metric | Count |
|---|---|
| Total systems identified | 21 |
| Design docs started | 1 |
| Design docs reviewed | 0 |
| Design docs approved | 0 |
| MVP systems designed | 1 / 15 |
| Vertical Slice systems designed | 0 / 4 |
| Alpha systems designed | 0 / 1 |
| Full Vision systems designed | 0 / 1 |

---

## Next Steps

- [x] Systems enumeration complete (21 systems)
- [x] Dependency map approved
- [x] Priority assignments approved
- [x] Design first GDD: **Input Manager** — `design/gdd/input-manager.md`
- [ ] Design second GDD: **Game State Manager** — run `/design-system game-state-manager`
- [ ] Design third GDD: **Pattern Database** — run `/design-system pattern-database`
- [ ] Prototype echo formation stress test before GDD lock — run `/prototype echo-formation-performance`
- [ ] Run `/gate-check pre-production` when all 15 MVP system GDDs are designed and reviewed
