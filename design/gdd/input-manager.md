# Input Manager

> **Status**: Design Complete — Pending Review
> **Author**: Design session + agents
> **Last Updated**: 2026-04-24
> **Implements Pillar**: 희생은 선택이다 (Sacrifice is Agency) / 흐름 속의 깊이 (Depth Through Flow)

## Overview

The Input Manager is the system that translates hardware events (keyboard keypresses, gamepad button presses, analog stick values) into named game actions. It defines the complete vocabulary of what the player can do in REQUIEM FORMATION — not how those actions are executed, but what exists and how it's bound. Every downstream system (ship controller, echo formation, UI navigation) reads from this system's action definitions, never from hardware directly.

The system uses Unity's New Input System (`com.unity.inputsystem`) with a generated `PlayerControls` C# class as the type-safe interface. Legacy `Input` class usage is forbidden project-wide. Two device targets are supported with equal priority: keyboard+mouse and gamepad. Neither is treated as secondary — both must deliver identical action fidelity and responsiveness.

Three action maps govern the session:
- **Gameplay** — ship movement, firing, sacrifice, pause
- **UI** — menu navigation for all screen states (required for full gamepad d-pad support on every menu)
- **Disabled** — the empty map active during non-interactive states (story screens, transition animations)

The player impact of a well-designed Input Manager: controls feel owned rather than operated. A player switching between keyboard and gamepad mid-session does so seamlessly, without configuration. Every press fires where intended. The Sacrifice action — the game's most emotionally loaded input — is unambiguous and impossible to trigger accidentally. When these properties are achieved, the Input Manager disappears from the player's awareness.

**The Sacrifice action is this system's highest-stakes design decision.** Because Sacrifice is the game's core pillar (희생은 선택이다), its input model determines whether the mechanic reads as intentional agency or accidental misfire. This GDD defines that model.

## Player Fantasy

The Input Manager has no direct player fantasy — players do not interact with it consciously. The fantasy is its *absence*: the hardware disappearing so only intent remains.

When the Input Manager works correctly, the player never thinks about it. Their thumb moves and the ship moves; their finger twitches and a sacrifice is made. The fantasy is that the hardware has disappeared and only intent remains: the player decides to die, and death answers on the same frame. This is the standard every input must meet — not "controls feel responsive," but "controls stopped being something the player has to think about."

When the Input Manager fails, the player feels betrayed by their own hands. A missed sacrifice doesn't read as "input lag." It reads as the game refusing their choice at the most sacred moment — and because the game's entire pillar structure (희생은 선택이다) is built on the premise that sacrifice is always the player's deliberate decision, an ambiguous or misfired Sacrifice input is not a bug. It is a contradiction of the game's thesis.

**Sacrifice input specifically**: The Sacrifice action is the only input that must be impossible to trigger accidentally. Accidental sacrifice is not "frustrating controls" — it is the game telling the player that their most important choice wasn't really their choice. This framing defines the design requirement: the Sacrifice action must carry a friction signature (press model or confirmation threshold) that makes accidental firing mechanically impossible, without adding cognitive overhead in the flow state.

## Detailed Design

### Core Rules

1. **No legacy Input class.** All hardware reads use `UnityEngine.InputSystem` exclusively. Any use of `UnityEngine.Input` is a build error. The generated `PlayerControls` C# class is the only public interface to input state.

2. **Automatic device switching.** When the player presses a key or button on a different device than the last active device, the Input Manager switches the active Control Scheme and broadcasts `DeviceSwitchedEvent(DeviceType newDevice)`. No user action is required.

3. **Three mutually exclusive Action Maps.** Only one Action Map is active at any time. Transitions are owned by the Input Manager via `InputManager.EnableMap(ActionMapId id)`. Callers do not enable maps directly — they request transitions through Game State Manager events.

   | Action Map | Active During |
   |---|---|
   | **Gameplay** | Playing state |
   | **UI** | Title, Pause, ChapterClear, GameOver, Settings states |
   | **Disabled** | Story screens, transition animations, cutscenes |

4. **Move — normalized Vector2.** Keyboard WASD produces a normalized diagonal (not magnitude-1.41 raw). Gamepad left stick passes through deadzone inner=0.15 / outer=0.95 with `StickDeadzone` processor. The Move value is read by poll (not event) in `FixedUpdate`.

5. **Fire — Press Only, bool output.** Fire action uses `Press Only` interaction. The Ship Controller polls `IsFiring` each `FixedUpdate`. Rate-of-fire limiting lives in the Ship Controller, not here.

6. **Sacrifice — Hold interaction, 0.3s threshold.**
   - Interaction type: `Hold`, `holdTime = 0.3f`
   - Keyboard binding: Left Shift (primary). X may be offered as secondary in Settings with a proximity warning — it is never the default.
   - Gamepad binding: Right Trigger Axis with `PressPoint = 0.35`. The 0.35 press-point creates a mechanical dead zone against stress-grip crosstalk before the hold timer starts.
   - Three events published:
     - `SacrificeChargeStarted` — fires on `started` callback (t = 0, threshold not yet met)
     - `SacrificeConfirmed` — fires on `performed` callback (t ≥ 0.3s)
     - `SacrificeAborted` — fires on `canceled` callback (released before threshold OR released after confirm)
   - "S" is permanently excluded as a Sacrifice binding candidate — it is WASD Down movement.

7. **Pause — Direct call.** Pause action fires `GameStateManager.RequestPause()` on the `performed` callback. No intermediate event. The Pause binding never changes.

8. **UI Navigation via `InputSystemUIInputModule`.** All menu navigation (Navigate, Submit, Cancel, Point, Click, ScrollWheel, MiddleClick, RightClick, TrackedDevicePosition, TrackedDeviceOrientation) is handled by the `InputSystemUIInputModule` component reading from the UI Action Map. No custom UI input code is written.

9. **UI Action Map covers all menu states.** The UI Action Map is active during Title, Pause, ChapterClear, GameOver, and Settings. All menus must support both keyboard arrow/WASD navigation and gamepad d-pad — no hover-only interactions.

10. **No input buffering.** Sacrifice, Fire, and Pause do not buffer across frame boundaries or state transitions. If a Sacrifice hold is in progress when the Action Map switches to UI, the hold is canceled and `SacrificeAborted` fires. This prevents ghost inputs after scene transitions.

11. **Disabled Map is truly empty.** The Disabled Action Map contains zero actions and zero bindings. It is not a suppressed Gameplay map — it is a separate empty asset. This guarantees zero input processing cost during non-interactive states.

---

### States and Transitions

The Input Manager does not own game state — it owns Action Map activation. All transitions are driven by Game State Manager state-change events, with one exception.

| From | To | Trigger | Action Map Result |
|---|---|---|---|
| Any | Playing | `GameStateManager.StateChanged(Playing)` | Enable **Gameplay** |
| Any | Paused | `GameStateManager.StateChanged(Paused)` | Enable **UI** |
| Any | Title / GameOver / ChapterClear | `GameStateManager.StateChanged(Title/GameOver/ChapterClear)` | Enable **UI** |
| Any | StoryScreen / Transition | `GameStateManager.StateChanged(StoryScreen/Transition)` | Enable **Disabled** |
| Any | Settings | `GameStateManager.StateChanged(Settings)` | Enable **UI** |
| Playing | UI *(exception)* | Application focus lost (Alt-Tab, OS interruption) | Enable **UI** — Input Manager acts directly, does not wait for Game State Manager |

The focus-loss exception prevents a held Sacrifice from confirming in the background when the player returns to the window.

---

### Interactions with Other Systems

| System | Direction | What is exchanged |
|---|---|---|
| **Ship Controller** | Input Manager → Ship Controller | Poll: `MoveVector` (Vector2) and `IsFiring` (bool) read in `FixedUpdate` |
| **Sacrifice System** | Input Manager → Sacrifice System | Events: `SacrificeChargeStarted`, `SacrificeConfirmed`, `SacrificeAborted` |
| **UI System** | Input Manager → UI System | `DeviceSwitchedEvent(DeviceType)` — UI system uses this to show/hide gamepad prompts vs. keyboard hints |
| **Game State Manager** | Bidirectional | Input Manager subscribes to `StateChanged` events to switch Action Maps. Input Manager calls `GameStateManager.RequestPause()` on Pause action. |
| **Settings System** | Bidirectional | Settings calls `InputManager.StartRebindSession(ActionId)` and `InputManager.CancelRebindSession()`. Input Manager calls `PerformInteractiveRebinding()` and notifies Settings on completion. Persisted bindings are loaded at startup via `InputManager.LoadBindingOverrides()`. |

## Formulas

### F1 — Keyboard Diagonal Normalization

Raw WASD produces a vector with up to magnitude √2 on diagonals. The Move action must output a unit vector regardless of input device.

```
RawInput = Vector2(horizontal, vertical)   // each axis ∈ {-1, 0, 1}
MoveVector = RawInput.magnitude > 1 ? RawInput.normalized : RawInput
```

Unity implementation: `Vector2Normalization` processor on the keyboard composite binding, or `Vector2.ClampMagnitude(raw, 1.0f)`.

Example: WASD diagonal → raw (1, 1) → magnitude 1.414 → normalized (0.707, 0.707). Pure right → raw (1, 0) → unchanged (1, 0).

---

### F2 — Gamepad Stick Deadzone Rescaling

```
inner = 0.15
outer = 0.95
magnitude = |rawStick|

if magnitude < inner:  processedMagnitude = 0
if magnitude > outer:  processedMagnitude = 1
else:                  processedMagnitude = (magnitude - inner) / (outer - inner)

MoveVector = rawStick.normalized * processedMagnitude
```

Unity implementation: `StickDeadzone(min: 0.15, max: 0.95)` processor on the left stick binding.

Example: Idle drift at magnitude 0.08 → clipped to 0. Full press at magnitude 0.97 → output 1.0. Half-press at magnitude 0.55 → output `(0.55 - 0.15) / (0.95 - 0.15) = 0.50`.

---

### F3 — Sacrifice Hold Threshold

```
holdTime = 0.3s   // 18 frames at 60fps

t = elapsed time since SacrificeChargeStarted (input held above PressPoint)

SacrificeChargeStarted fires when: t = 0 (input crosses PressPoint)
SacrificeConfirmed fires when:     t >= holdTime
SacrificeAborted fires when:       input drops below PressPoint at any t

HoldProgress (for HUD fill visualization) = clamp(t / holdTime, 0, 1)
```

Example: Player holds for 0.22s then releases → HoldProgress peaks at 0.73, SacrificeAborted fires, no sacrifice occurs.

---

### F4 — Gamepad Trigger Press Point

The trigger hold timer requires a deliberate press depth to prevent stress-grip crosstalk.

```
PressPoint = 0.35   // 35% of full trigger travel
rawTrigger ∈ [0.0, 1.0]

Hold timer starts when:  rawTrigger >= PressPoint
Hold timer resets when:  rawTrigger < PressPoint
```

Combined with F3: `SacrificeConfirmed` fires when the trigger has been held at ≥ 0.35 depth for ≥ 0.3 continuous seconds.

Example: Resting finger at 0.25 depth → no hold timer starts. Deliberate press to 0.40 depth held for 0.3s → SacrificeConfirmed fires.

## Edge Cases

**EC1 — Sacrifice hold interrupted by game state change.**
If a Sacrifice hold is in progress (SacrificeChargeStarted has fired, SacrificeConfirmed has not) and the Action Map switches to UI or Disabled, `SacrificeAborted` fires immediately before the map switch completes. The Sacrifice System receives the abort before losing its listener. No sacrifice occurs.

**EC2 — Sacrifice confirmed while absorbing a pattern.**
The Input Manager fires `SacrificeConfirmed` regardless of game context — it has no knowledge of absorption state. Whether sacrifice interrupts absorption is a Sacrifice System / Pattern Absorption design decision. The Input Manager's responsibility ends at the event. *(Requires cross-system design resolution.)*

**EC3 — Gamepad disconnected mid-session.**
On `InputDevice.disconnected`: Input Manager fires `DeviceSwitchedEvent(Keyboard)` and reverts the active Control Scheme to Keyboard&Mouse. If in Playing state, Input Manager calls `GameStateManager.RequestPause()`. The "controller disconnected" modal is the Game State Manager's responsibility. Input Manager never silently falls through to keyboard without notification.

**EC4 — Two gamepads connected simultaneously.**
Only the first gamepad to send input after session start is assigned to the player. If a second gamepad sends input, `DeviceSwitchedEvent` fires with the new device. The player actively claims a gamepad by pressing any button on it. No player-slot assignment is needed.

**EC5 — Rebind session: player tries to bind a reserved key.**
Reserved bindings (Escape/Start for Pause, WASD for Move) cannot be overwritten. `PerformInteractiveRebinding()` is configured with `.WithCancelingThrough("<Keyboard>/escape")` and `.WithControlsExcluding()` for reserved actions. The rebind is rejected and the player is returned to the binding prompt.

**EC6 — Rebind session: player binds Sacrifice to the same key as Fire.**
Duplicate binding detection is the Settings System's responsibility. The Input Manager executes whatever bindings it is given. If the Settings System allows a duplicate, both actions will fire from the same input. The Settings System must validate before saving.

**EC7 — Sacrifice input during Pause/UI state.**
The Gameplay Action Map is inactive during UI state. Right Trigger in the UI Action Map is bound to `Cancel` via `InputSystemUIInputModule`, not to Sacrifice. No `SacrificeChargeStarted` event fires. Releasing the trigger in UI state has no sacrifice-related effect.

**EC8 — Hold timer: frame-rate dependency.**
The Hold interaction timer uses real time (`Time.unscaledDeltaTime`), not frame count. `SacrificeConfirmed` fires at 0.3 wall-clock seconds regardless of frame rate. At 30fps, the threshold is still 0.3s. The "18 frames" reference in F3 is a 60fps illustration, not a frame-count specification.

**EC9 — Application loses focus mid-hold.**
On `Application.focusChanged(false)`: Input Manager enables the UI Action Map directly without waiting for Game State Manager. Any in-progress Sacrifice hold issues `SacrificeAborted`. When focus returns, the Action Map remains on UI until Game State Manager resumes Playing state.

**EC10 — Binding overrides not found at startup.**
If `LoadBindingOverrides()` fails to find persisted override data (first launch, corrupt save, or cleared data), the Input Manager loads the default bindings from the Input Actions Asset. No error is thrown. Default bindings are always valid fallbacks.

## Dependencies

| System | Relationship | What this system needs / provides |
|---|---|---|
| **Game State Manager** | Bidirectional | *Needs*: `StateChanged` events to switch Action Maps. *Provides*: `RequestPause()` call on Pause action. |
| **Ship Controller** | Outbound | *Provides*: `MoveVector` (Vector2) and `IsFiring` (bool) polled in `FixedUpdate`. Ship Controller must not read input directly. |
| **Sacrifice System** | Outbound | *Provides*: `SacrificeChargeStarted`, `SacrificeConfirmed`, `SacrificeAborted` events. |
| **UI System** | Outbound | *Provides*: `DeviceSwitchedEvent(DeviceType)` for prompt visibility. UI navigation handled automatically via `InputSystemUIInputModule`. |
| **Settings System** | Bidirectional | *Needs*: `StartRebindSession(ActionId)` / `CancelRebindSession()` calls. *Provides*: rebind execution, completion notification, and `LoadBindingOverrides()` at startup. |
| **Unity New Input System** | External | `com.unity.inputsystem` — `PlayerControls` generated class, `InputSystemUIInputModule`, `Hold` interaction, `StickDeadzone` processor. |

**Bidirectionality note**: Game State Manager GDD must list Input Manager as a caller (it receives `RequestPause()` and must fire state-change events consumed here). Settings System GDD must describe the rebind session protocol. Ship Controller GDD must note it polls Input Manager, not hardware.

## Tuning Knobs

| Knob | Default | Safe Range | Gameplay Effect |
|---|---|---|---|
| `SacrificeHoldTime` | 0.3s | 0.2–0.4s | Hold duration before `SacrificeConfirmed`. Lower = more responsive, higher accidental-fire risk. Higher = safer, adds latency to the game's most emotional input. |
| `TriggerPressPoint` | 0.35 | 0.20–0.50 | Gamepad trigger depth required before hold timer starts. Lower = more sensitive (stress-grip crosstalk risk). Higher = requires deliberate press (crosstalk protection increases). |
| `DeadzoneInner` | 0.15 | 0.08–0.20 | Stick deadzone lower bound. Lower = more responsive to small movements, more noise from worn sticks. Higher = less drift, reduced fine control precision. |
| `DeadzoneOuter` | 0.95 | 0.85–1.00 | Stick deadzone upper bound. Lower = full speed reached earlier in stick travel. Higher = requires full physical press for full speed output. |

**Exposure**: `SacrificeHoldTime` should be exposed in the Settings System as an Accessibility option — "Sacrifice Hold Duration" with short/default/long presets. The remaining three are developer tuning values, not player-facing.

## Visual/Audio Requirements

The Input Manager produces no visuals or audio directly. It publishes events; downstream systems respond.

| Event | Visual Response | Audio Response | Owner |
|---|---|---|---|
| `SacrificeChargeStarted` | Ship luminance pulse begins; HUD sacrifice indicator fill starts | Low-frequency "charging" audio begins | VFX System / Audio System |
| `SacrificeConfirmed` | Red explosion (per art bible #ff4040) | Sacrifice audio sting | VFX System / Audio System |
| `SacrificeAborted` | Instant snap back to baseline — no fade | Audio stops immediately, no release tail | VFX System / Audio System |
| `DeviceSwitchedEvent` | Gamepad/keyboard UI prompts swap | None | UI System |

**HUD sacrifice indicator states** (required from HUD system):
- Idle: base state (no fill)
- Charging: fill animates with `HoldProgress` (see F3)
- Locked/Unavailable: distinct visual state for when sacrifice is blocked by game state

## UI Requirements

- All menus must support gamepad d-pad navigation and keyboard arrow navigation. No hover-only interactions.
- Controls screen must display current active bindings (including player overrides), not defaults.
- Controls screen must show both Keyboard and Gamepad bindings simultaneously — one row per action, two columns.
- When a rebind session is active, the bound-key field must display a "Press any key…" prompt and accept only the next input.
- Reserved bindings (Pause, Move) must be visually marked as non-rebindable.
- `SacrificeHoldTime` must be exposed as an Accessibility setting ("Sacrifice Hold Duration": Short / Default / Long) — not a raw numeric field.

## Acceptance Criteria

**AC1 — Move: keyboard diagonal magnitude**
Given: WASD diagonal held (W + D). Expect: `MoveVector.magnitude` = 1.0 ± 0.01. Fail if: magnitude ≈ 1.414.

**AC2 — Move: stick deadzone low end**
Given: Gamepad left stick at magnitude 0.08 (simulated noise). Expect: `MoveVector` = Vector2.zero. Fail if: any nonzero output.

**AC3 — Move: stick deadzone rescaling**
Given: Stick at magnitude 0.55. Expect: `MoveVector.magnitude` ≈ 0.50 (per F2). Fail if: output equals raw 0.55 or is zero.

**AC4 — Sacrifice: keyboard hold fires correct event sequence**
Given: Left Shift held for 0.35s then released. Expect in order: `SacrificeChargeStarted` → `SacrificeConfirmed` → `SacrificeAborted`. Fail if: any event missing, out of order, or duplicate.

**AC5 — Sacrifice: keyboard tap fires abort only**
Given: Left Shift tapped (held 0.15s, released). Expect: `SacrificeChargeStarted` → `SacrificeAborted`. Fail if: `SacrificeConfirmed` fires.

**AC6 — Sacrifice: trigger press-point gate**
Given: Right trigger held at 0.25 depth for 0.5s. Expect: no events fire. Fail if: `SacrificeChargeStarted` fires.

**AC7 — Sacrifice: trigger hold fires at threshold**
Given: Right trigger pressed to 0.40 depth and held for 0.35s. Expect: `SacrificeChargeStarted` then `SacrificeConfirmed`. Fail if: either event missing.

**AC8 — Device switching: keyboard to gamepad**
Given: Playing with keyboard; press gamepad A button. Expect: `DeviceSwitchedEvent(Gamepad)` fires. Fail if: no event, or event fires with wrong DeviceType.

**AC9 — Action map exclusivity: Gameplay never active during UI state**
Given: Game enters Paused state. Expect: Gameplay Action Map disabled; UI Action Map enabled. Pressing Left Shift does not fire `SacrificeChargeStarted`. Fail if: Sacrifice event fires during pause.

**AC10 — Disabled map: zero input processing**
Given: Game in StoryScreen state (Disabled map active). Expect: no Move, Fire, Sacrifice, or UI events fire regardless of input. Fail if: any action event fires.

**AC11 — Pause: fires RequestPause on press**
Given: Escape key pressed during Playing state. Expect: `GameStateManager.RequestPause()` called within the same frame. Fail if: method not called, or called with delay.

**AC12 — Binding persistence: overrides survive restart**
Given: Player rebinds Sacrifice to X key; game is closed and reopened. Expect: Sacrifice binding is X, not Left Shift. Fail if: bindings reset to defaults on restart.

**AC13 — Gamepad disconnect: auto-pause**
Given: Playing state; gamepad physically disconnected. Expect: `DeviceSwitchedEvent(Keyboard)` fires and `GameStateManager.RequestPause()` is called. Fail if: game continues without pause.

**AC14 — Hold timer uses real time, not frames**
Given: Application running at locked 30fps; Left Shift held for 0.31s wall-clock time. Expect: `SacrificeConfirmed` fires. Fail if: system requires 18 frames (0.6s at 30fps) before confirming.

## Open Questions

1. **Sacrifice during absorption** — Does `SacrificeConfirmed` interrupt an in-progress pattern absorption, or is sacrifice blocked while absorbing? This is a Sacrifice System + Pattern Absorption cross-system design decision. The Input Manager fires the event regardless; the receiving system decides whether to act on it. *Requires resolution before Sacrifice System GDD is authored.*

2. **"Locked/Unavailable" sacrifice states** — What game states render sacrifice unavailable (e.g., already at 0 lives, specific boss phases)? The HUD indicator needs a locked visual state; the Input Manager needs to know whether to suppress `SacrificeConfirmed` or let the Sacrifice System reject it. *Requires coordination with Sacrifice System GDD.*

3. **X key secondary binding proximity warning** — If X is offered as a secondary sacrifice binding, when and how should the Settings System display the proximity-to-fire-cluster warning? UX design decision for the Settings screen. *Requires UX spec.*
