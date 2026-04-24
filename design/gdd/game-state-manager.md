# Game State Manager

> **Status**: In Design
> **Author**: Design session + agents
> **Last Updated**: 2026-04-24
> **Implements Pillar**: 흐름 속의 깊이 (Depth Through Flow) / 희생은 선택이다 (Sacrifice is Agency)

## Overview

The Game State Manager is the single authority on what state the game is in at any moment. It defines the complete set of named game states, owns all transitions between them, and broadcasts state changes to all dependent systems via a typed event. No other system makes state decisions — they read from the Game State Manager and react.

This system exists to prevent a failure mode that scales with the number of systems: without a single state authority, each system independently tracks whether the game is paused, in a menu, or playing — and those local state variables diverge. In a game with 12 systems that care about game state, 12 independent state trackers create 12 surfaces for bugs. The Game State Manager eliminates that surface entirely.

The full state vocabulary defined here: **Title**, **Playing**, **Paused**, **StoryScreen**, **ChapterClear**, **GameOver**, **Settings**, and **Transition** (a transient state spanning scene loads and animated hand-offs between named states). Every system that behaves differently in different contexts reads `GameStateManager.CurrentState` or subscribes to `GameStateManager.StateChanged`. No system polls hardware or checks scene names to infer game state.

## Player Fantasy

The Game State Manager has no direct player fantasy. Players never see it, never touch it, never name it. Its job is to be the invisible stage on which every other fantasy is performed — the place where the pilot's sacrifice lands, where the echoes resolve into narrative, where a chapter ends and the next begins without the player ever feeling the seam.

This system serves **흐름 속의 깊이 (Depth Through Flow)** above all else. Flow is not the absence of complexity — it is complexity delivered without interruption. When the player triggers a sacrifice and the world dims, when a chapter clears and the story screen rises to meet them, when they pause mid-run and return to a battlefield that remembers exactly where it was — those moments are only possible because one authority owns the transitions. Twelve systems reacting to a single truth feels like a game that knows itself. Twelve systems guessing at the truth feels like a game falling apart.

When this system works, the player feels nothing. They feel the pilot, the weight of the choice, the story — never the scaffolding. When it fails, the feeling is unmistakable: a pause menu that dims the HUD but not the music, a Game Over that still accepts fire input, a chapter transition where the echoes flicker before the next stage loads. The fantasy this system protects is **continuity of self** — the player's unbroken belief that they are commanding the battlefield and not operating a machine.

## Detailed Design

### Core Rules

**CR1 — Single Authority, Request Model.**
The Game State Manager is the only system that changes the current state. All state changes originate from an explicit `RequestXxx()` call made by another system, an internal self-transition triggered by a Transition completion callback, or a startup initialization. Other systems never set state by publishing events the GSM "listens for." The direction is always: caller invokes a named method on the GSM. This makes every state-change intent explicit, traceable, and auditable.

**CR2 — Transition Is a Gate, Not a Queue.**
While `Transition` is the current state, all `RequestXxx()` calls from external systems are silently dropped — not queued, not deferred, not retried. The only state changes that occur during `Transition` are internal: the GSM advances to the next named state when the transition operation completes. This prevents competing state changes during animated handoffs or scene loads.

**CR3 — Time Scale Ownership.**
The Game State Manager owns `Time.timeScale`. No other system writes to `Time.timeScale` directly.

| State | Time.timeScale |
|---|---|
| Playing | 1.0 |
| Paused | 0.0 |
| StoryScreen | 1.0 |
| ChapterClear | 1.0 |
| GameOver | 1.0 |
| Title | 1.0 |
| Settings (from Paused) | 0.0 — inherits from origin |
| Settings (from Title) | 1.0 — inherits from origin |
| Transition | Inherits from exiting state until scene load begins; then 1.0 (transition animations use unscaled time) |

`StoryScreen` runs at timeScale 1.0. Gameplay is halted by a separate mechanism: every gameplay system (Ship Controller, Enemy System, Pattern Absorption, etc.) suspends itself on `StateChanged(StoryScreen)`. This preserves full-speed animation and UI during story moments without requiring all story screen code to use `unscaledDeltaTime`.

**CR4 — Chapter Index Ownership.**
The Game State Manager owns `CurrentChapterIndex` (integer, 1–5). The Chapter Manager reads this property but does not own or mutate it. When Chapter Manager calls `RequestChapterClear()`, the GSM increments `CurrentChapterIndex` as part of processing that transition. No other system may write chapter index.

**CR5 — Startup State.**
The game boots into `Title` state with `CurrentChapterIndex = 1`. The GSM fires `StateChanged(Title, Title)` during its own initialization so all subscribers receive the initial state on first subscription.

**CR6 — Settings Is a Derived State.**
`Settings` is only entered from `Title` or `Paused`. It is never entered from `Playing`, `StoryScreen`, `ChapterClear`, `GameOver`, or `Transition` directly. On exit from `Settings`, the GSM returns to the origin state (whichever was active when `RequestSettings()` was called). The GSM tracks this origin internally; the Settings System has no knowledge of it.

**CR7 — StateChanged Fires on Every Transition.**
`StateChanged(GameState newState, GameState previousState)` is broadcast every time the current state changes — including when entering or exiting `Transition`. All subscribers receive both new and previous state. Systems that need to know "what state was active before this transition?" may read `previousState` without querying the GSM again.

**CR8 — No Internal Recovery Logic.**
If a Transition cannot complete (e.g., scene load failure), the game enters an undefined blocking state. Recovery from such failures is outside the scope of this system. The GSM's contract is that every valid transition it begins, it completes.

---

### States and Transitions

#### State Definitions

| State | Description | Time.timeScale | Input Map |
|---|---|---|---|
| `Title` | Main title screen and main menu | 1.0 | UI |
| `Playing` | Active gameplay — ship, enemies, scoring, absorption, sacrifice live | 1.0 | Gameplay |
| `Paused` | Gameplay frozen, pause menu visible | 0.0 | UI |
| `StoryScreen` | Pre/post-chapter narrative; game simulation suspended via StateChanged | 1.0 | Disabled |
| `ChapterClear` | Chapter completion screen with results | 1.0 | UI |
| `GameOver` | Player health depleted by non-sacrifice death; retry/quit screen overlays battlefield | 1.0 | UI |
| `Settings` | Settings menu; entered from Title or Paused only | Inherits from origin | UI |
| `Transition` | Transient blocking state spanning animated handoffs and scene loads | Varies | Disabled |

#### Valid Transitions

| # | From | To | Trigger | Caller |
|---|---|---|---|---|
| T01 | `Title` | `Transition` → `StoryScreen` or `Playing` | Player selects New Game or Continue | Menu System: `RequestStartGame(int chapterIndex)` |
| T02 | `Title` | `Settings` | Player selects Settings | Menu System: `RequestSettings()` |
| T03 | `Playing` | `Paused` | Player presses Pause | Input Manager: `RequestPause()` |
| T04 | `Playing` | `Paused` | Controller disconnected | Input Manager: `RequestPause()` |
| T05 | `Playing` | `Paused` | Application loses focus | Input Manager: `RequestPause()` (after directly enabling UI map) |
| T06 | `Playing` | `Transition` → `StoryScreen` | Chapter story event triggered mid-chapter | Chapter Manager: `RequestStoryScreen(ctx)` |
| T07 | `Playing` | `Transition` → `ChapterClear` | Chapter end condition met | Chapter Manager: `RequestChapterClear()` — GSM increments `CurrentChapterIndex` |
| T08 | `Playing` | `GameOver` | Player health reaches zero via non-sacrifice | Player Health System: `RequestGameOver()` — direct overlay, no Transition |
| T09 | `Paused` | `Playing` | Player resumes | Menu System: `RequestResume()` |
| T10 | `Paused` | `Settings` | Player selects Settings from pause menu | Menu System: `RequestSettings()` |
| T11 | `Paused` | `Transition` → `Title` | Player selects Quit to Title | Menu System: `RequestQuitToTitle()` |
| T12 | `Settings` | `Title` or `Paused` | Player closes Settings | Menu System: `RequestExitSettings()` — no Transition (no scene change) |
| T13 | `StoryScreen` | `Transition` → `Playing` | Story screen concludes, next state is gameplay | Story Screen System: `RequestStoryComplete()` |
| T14 | `StoryScreen` | `Transition` → `ChapterClear` | Story screen concludes, next state is chapter clear | Story Screen System: `RequestStoryComplete()` — GSM determines next state from `StoryScreenContext` |
| T15 | `ChapterClear` | `Transition` → `StoryScreen` or `Playing` | Player advances to next chapter | Menu System: `RequestNextChapter()` |
| T16 | `ChapterClear` | `Transition` → `Title` | Player returns to main menu | Menu System: `RequestQuitToTitle()` |
| T17 | `GameOver` | `Transition` → `Playing` | Player retries current chapter | Menu System: `RequestRetry()` — `CurrentChapterIndex` unchanged |
| T18 | `GameOver` | `Transition` → `Title` | Player quits to title | Menu System: `RequestQuitToTitle()` |
| T19 | `Transition` | *(target state)* | Async operation completes | Internal GSM callback — no external caller |

*T01 routing*: `RequestStartGame()` routes through `Transition` then to `StoryScreen` (if a pre-chapter story screen exists for that chapter) or directly to `Playing`. Routing is determined by chapter configuration data, not hardcoded GSM logic.

*T07 / Final chapter*: If `CurrentChapterIndex` = 5 at the time of `RequestChapterClear()`, the GSM routes to the game's final sequence rather than standard `ChapterClear`. This special path is defined in the Chapter Manager GDD.

#### Invalid / Blocked Transitions

| Attempted Transition | Result |
|---|---|
| Any `RequestXxx()` while in `Transition` | Silently dropped. No state change. No callback. |
| `RequestPause()` while in `Paused` | Dropped — already in target state. |
| `RequestResume()` while in `Playing` | Dropped — already in target state. |
| `RequestPause()` from `Title`, `ChapterClear`, `GameOver`, `StoryScreen` | Dropped — Pause only valid during `Playing`. |
| `RequestGameOver()` from any state other than `Playing` | Dropped. |
| `RequestChapterClear()` from any state other than `Playing` or `StoryScreen` | Dropped. |
| `RequestSettings()` from `Playing`, `StoryScreen`, `ChapterClear`, `GameOver`, `Transition` | Dropped — Settings only reachable from `Title` or `Paused`. |
| `RequestNextChapter()` when `CurrentChapterIndex` = 5 and already in special final sequence | Dropped — handled by T07 final-chapter routing. |

#### Transition State — Entry and Exit

**Entry**: GSM sets `CurrentState = Transition`, fires `StateChanged(Transition, previousState)`, begins the async operation (scene load, animation), and stops accepting external requests.

**Exit**: When the operation completes, GSM sets `CurrentState` to the target named state, applies the target state's timeScale, and fires `StateChanged(targetState, Transition)`.

`Transition` is never a resting state. Minimum duration is one frame (if the operation completes immediately). Maximum duration is unbounded — the GSM waits for the registered completion callback.

---

### Interactions with Other Systems

| System | Direction | What is exchanged |
|---|---|---|
| **Input Manager** | Bidirectional | *Receives*: `RequestPause()` calls (on Pause input, controller disconnect, focus loss). *Provides*: `StateChanged` event for Action Map switching. |
| **Player Ship Controller** | Outbound only | *Provides*: `StateChanged` event. Ship Controller is active only in `Playing`; self-suspends on all other states. Does not rely on timeScale to halt — halts on `StateChanged` directly. |
| **Player Health System** | Bidirectional | *Receives*: `RequestGameOver()` when health reaches zero by non-sacrifice. *Provides*: `StateChanged` event. Damage intake suspended in all states except `Playing`. |
| **Enemy System** | Outbound only | *Provides*: `StateChanged` event. All enemy AI, movement, and spawning active only in `Playing`. Enemies freeze on other states; not destroyed until scene unload. |
| **Score System** | Outbound only | *Provides*: `StateChanged` event. Scoring events processed only in `Playing`. Score finalizes and becomes available on `ChapterClear`. |
| **Pattern Absorption** | Outbound only | *Provides*: `StateChanged` event. Absorption logic runs only in `Playing`. In-progress absorption suspends on pause, discards on `GameOver`. |
| **Strategic Sacrifice** | Outbound + readable | *Provides*: `StateChanged` event; `CurrentState` readable property. Sacrifice System queries `CurrentState` on `SacrificeConfirmed` — only acts if `Playing`. Does NOT call `RequestGameOver()` — strategic sacrifice is never a death path through the Health System. |
| **Echo Formation** | Outbound + readable | *Provides*: `StateChanged` event; `CurrentChapterIndex` readable property. Echo AI and formation logic active only in `Playing`. Echo Formation reads `CurrentChapterIndex` to inform save/persistence coordination with Save System. |
| **Chapter Manager** | Bidirectional | *Receives*: `RequestChapterClear()`, `RequestStoryScreen(StoryScreenContext ctx)`, scene-load completion callbacks. *Provides*: `StateChanged` event; `CurrentChapterIndex` readable property. Chapter Manager is the primary driver of mid-game structural transitions. The `StoryScreenContext` parameter tells the GSM whether the story screen precedes chapter gameplay (next → `Playing`) or follows it (next → `ChapterClear`). |
| **Save System** | Outbound only | *Provides*: `StateChanged` event. Save System is event-driven — it writes on `ChapterClear`, `GameOver`, and `QuitToTitle` transitions. GSM does not call save methods directly. |
| **HUD** | Outbound only | *Provides*: `StateChanged` event. HUD visibility is fully state-driven. HUD is visible in `Playing`; hidden or overlaid in all other states. |
| **Story Screen System** | Bidirectional | *Receives*: `RequestStoryComplete()` when story presentation ends. *Provides*: `StateChanged(StoryScreen)` activation event. Story Screen System does not decide what state comes after it completes — the GSM determines the next state from the stored `StoryScreenContext`. |
| **Menu System** | Bidirectional | *Receives*: `RequestStartGame()`, `RequestResume()`, `RequestSettings()`, `RequestExitSettings()`, `RequestNextChapter()`, `RequestRetry()`, `RequestQuitToTitle()`. *Provides*: `StateChanged` event to activate the correct menu screen. Menu System translates player UI selections into named GSM requests; it contains no state logic. |

---

### GSM Public Interface Summary

**Request methods** (callers listed above):

| Method | Valid-from States |
|---|---|
| `RequestPause()` | `Playing` |
| `RequestResume()` | `Paused` |
| `RequestGameOver()` | `Playing` |
| `RequestChapterClear()` | `Playing`, `StoryScreen` |
| `RequestStoryScreen(StoryScreenContext ctx)` | `Playing`, `ChapterClear` |
| `RequestStoryComplete()` | `StoryScreen` |
| `RequestStartGame(int chapterIndex)` | `Title` |
| `RequestNextChapter()` | `ChapterClear` |
| `RequestRetry()` | `GameOver` |
| `RequestQuitToTitle()` | `Paused`, `ChapterClear`, `GameOver` |
| `RequestSettings()` | `Title`, `Paused` |
| `RequestExitSettings()` | `Settings` |

**Readable properties:**

| Property | Type | Description |
|---|---|---|
| `CurrentState` | `GameState` (enum) | Current named state. Never null. |
| `PreviousState` | `GameState` (enum) | State before most recent transition. |
| `CurrentChapterIndex` | `int`, 1–5 | Active chapter number. |

**Events:**

| Event | Signature | When fired |
|---|---|---|
| `StateChanged` | `(GameState newState, GameState previousState)` | Every state transition, including to/from `Transition` |

## Formulas

The Game State Manager contains no gameplay-balance formulas. Its quantifiable behaviors are bounds and mappings:

### F1 — Chapter Index Bounds

```
CurrentChapterIndex ∈ {1, 2, 3, 4, 5}

On RequestStartGame(chapterIndex):
  CurrentChapterIndex = clamp(chapterIndex, 1, 5)

On RequestChapterClear():
  CurrentChapterIndex = CurrentChapterIndex + 1
  if CurrentChapterIndex > 5: route to final-chapter sequence (not an error)
```

Valid range: [1, 5]. `RequestChapterClear()` beyond 5 triggers the final-chapter sequence rather than incrementing further.

### F2 — Time Scale Mapping

```
TimeScale(state) → float:
  Playing        → 1.0
  Paused         → 0.0
  Title          → 1.0
  StoryScreen    → 1.0
  ChapterClear   → 1.0
  GameOver       → 1.0
  Transition     → inherits previous state's value until scene load begins, then 1.0
  Settings       → inherits origin state's value (0.0 if entered from Paused; 1.0 if from Title)
```

Output range: {0.0, 1.0} exclusively. TimeScale is never set to an intermediate value by this system.

## Edge Cases

**EC1 — RequestPause() arrives frames after focus-loss.**
Input Manager enables the UI map directly on focus loss, then calls `RequestPause()`. Since GSM processes calls synchronously and `RequestPause()` from `Playing` is always valid, no race condition exists. The GSM processes it cleanly in the frame it arrives.

**EC2 — Two systems call conflicting transitions simultaneously (same frame).**
Example: Pause input fires the same frame as `RequestGameOver()`. Unity's single-threaded model means one call executes first — the second arrives in a state that may accept or drop it. The first-caller "wins." Execution order between the Health System and Input Manager must be defined in an ADR to guarantee deterministic resolution. *(Open — execution order ADR required.)*

**EC3 — Chapter 5 clear: final chapter routing.**
When `RequestChapterClear()` fires with `CurrentChapterIndex = 5`, the GSM does not enter standard `ChapterClear` — it routes to the final-chapter sequence (Final Echo boss + ending). Callers must not assume `ChapterClear` state follows a `RequestChapterClear()` call when on chapter 5.

**EC4 — RequestRetry() preserves chapter index.**
`RequestRetry()` routes to `Playing` for the current chapter (`CurrentChapterIndex` unchanged). The Save System GDD defines what echo formation state is restored on retry — the GSM owns the chapter index, not the echo state.

**EC5 — Settings animations when timeScale = 0.0.**
Settings entered from Paused inherits `timeScale = 0.0`. Any Settings screen element with time-driven animation must use `Time.unscaledDeltaTime`. The GSM does not provide a special time mode for Settings — this is an implementation constraint on the Settings System.

**EC6 — RequestQuitToTitle() during an active save operation.**
If the Save System is mid-write when `QuitToTitle` fires, the GSM enters `Transition` and waits for its completion callback. The Save System must complete its write before releasing the callback that ends the Transition. The GSM waits without intervention.

**EC7 — Player input during StoryScreen.**
The Disabled Action Map is active. No gameplay input fires. If a story screen has a player-advance prompt, the Story Screen System provides its own input binding for that purpose — the GSM does not partially re-enable gameplay input during `StoryScreen`.

**EC8 — StateChanged fires twice per Transition.**
Each transition fires `StateChanged` twice: entering Transition (`StateChanged(Transition, from)`) and exiting (`StateChanged(targetState, Transition)`). Systems must distinguish resume-from-transition from fresh initialization. A system suspending on `StateChanged(Transition, Playing)` must resume its suspended state on `StateChanged(Playing, Transition)`, not re-initialize from scratch.

**EC9 — Application quit during Playing state.**
`Application.Quit()` does not trigger a GSM state change or save. The Save System owns `OnApplicationQuit()` handling. The GSM has no quit state and takes no action on application termination.

## Dependencies

| System | Relationship | Interface |
|---|---|---|
| **Input Manager** | Bidirectional | *Needs*: `RequestPause()` from Input Manager. *Provides*: `StateChanged` event for Action Map switching. |
| **Player Ship Controller** | Outbound | *Provides*: `StateChanged` event. Ship Controller suspends gameplay on non-Playing states. |
| **Player Health System** | Bidirectional | *Needs*: `RequestGameOver()` when health reaches zero by non-sacrifice. *Provides*: `StateChanged` event. |
| **Enemy System** | Outbound | *Provides*: `StateChanged` event. Enemy AI active only in `Playing`. |
| **Score System** | Outbound | *Provides*: `StateChanged` event. Score locked outside `Playing`; finalizes on `ChapterClear`. |
| **Pattern Absorption** | Outbound | *Provides*: `StateChanged` event. Absorption logic active only in `Playing`. |
| **Strategic Sacrifice** | Outbound + readable | *Provides*: `StateChanged` event and `CurrentState` readable property. Sacrifice System queries `CurrentState` before acting on `SacrificeConfirmed`. |
| **Echo Formation** | Outbound + readable | *Provides*: `StateChanged` event and `CurrentChapterIndex` readable property. |
| **Chapter Manager** | Bidirectional | *Needs*: `RequestChapterClear()`, `RequestStoryScreen(StoryScreenContext)`, scene-load completion callbacks. *Provides*: `StateChanged` event and `CurrentChapterIndex` readable property. |
| **Save System** | Outbound | *Provides*: `StateChanged` event. Save System self-triggers on `ChapterClear`, `GameOver`, and `QuitToTitle` transitions. |
| **HUD** | Outbound | *Provides*: `StateChanged` event. HUD visibility fully state-driven. |
| **Story Screen System** | Bidirectional | *Needs*: `RequestStoryComplete()` when story ends. *Provides*: `StateChanged(StoryScreen)` activation event. |
| **Menu System** | Bidirectional | *Needs*: All 7 menu request methods (`RequestStartGame`, `RequestResume`, `RequestSettings`, `RequestExitSettings`, `RequestNextChapter`, `RequestRetry`, `RequestQuitToTitle`). *Provides*: `StateChanged` event to activate the correct screen. |

**Bidirectionality note**: All 12 dependent system GDDs must list the Game State Manager as a dependency and specify which `RequestXxx()` method they call and which `StateChanged` events they subscribe to.

## Tuning Knobs

The Game State Manager has very few designer-adjustable values. Its behavior is defined by the state machine, not runtime parameters.

| Knob | Default | Safe Range | Notes |
|---|---|---|---|
| `ChapterCount` | 5 | 1–5 | Total chapter count. Build-time constant, not runtime — changing it requires updating all systems that use chapter 5 as the final boundary. |
| `GameOverOverlayDelay` | 0s | 0–1.5s | Seconds before the GameOver overlay appears after `RequestGameOver()`. A 0.3–0.5s delay allows a death animation to play before the overlay interrupts. May live in HUD or GameOver screen rather than GSM depending on implementation. |

The state machine definition (states, transitions, timeScale assignments) is not a tuning knob. Changing it requires a GDD revision.

## Visual/Audio Requirements

[To be designed]

## UI Requirements

[To be designed]

## Acceptance Criteria

[To be designed]

## Open Questions

[To be designed]
