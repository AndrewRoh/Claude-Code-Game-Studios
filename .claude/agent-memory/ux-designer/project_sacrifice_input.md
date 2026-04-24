---
name: Sacrifice Input Design Decisions
description: Confirmed bindings, threshold rationale, feedback arc, and flagged risks for the Sacrifice input in REQUIEM FORMATION
type: project
---

## Confirmed Design Decisions (as of 2026-04-24)

- Sacrifice input: dedicated hold button, 0.3s threshold (18 frames at 60fps)
- Keyboard default: move=WASD, fire=Z or Space, sacrifice=TBD (Left Shift recommended), pause=Escape
- Gamepad default: move=Left stick, fire=A/South, sacrifice=Right trigger hold, pause=Start
- All menus: gamepad d-pad + keyboard arrow navigation required

## Recommendations Made (UX Assessment 2026-04-24)

**Threshold**: 0.3s is correct. Safe tuning range: 0.2-0.4s. Expose as Tuning Knob.

**Keyboard sacrifice**: Left Shift (primary). X (secondary, warn about proximity to fire cluster). S must never be sacrifice — it is already Down movement in WASD.

**Gamepad sacrifice**: Right trigger hold confirmed correct. Require minimum 0.3-0.4 trigger depth before hold timer starts (dead zone against stress-grip crosstalk).

**Feedback arc during hold (before confirmation)**:
- Frame 0: Ship luminance pulse begins + low-frequency "charging" audio + HUD indicator fill starts
- Frames 1-16: Pulse grows, audio pitch-bends upward, screen edge subtle red bleed (#ff4040 low opacity)
- Frame 17-18 (threshold): Full sacrifice fires (red explosion per art bible)
- Cancel (release before threshold): Instant snap to baseline — no fade, no ambiguity

## Flagged Risks

- "S" as sacrifice candidate must be permanently removed from consideration
- New players need one-time contextual hint on failed tap (below threshold hold)
- Sacrifice during absorption: game design decision needed — does sacrifice interrupt absorption?
- Gamepad disconnect must pause game and show modal — never silently switch to keyboard
- Controls screen must display current remapped bindings, not defaults
- HUD sacrifice indicator needs a distinct "locked/unavailable" visual state for states where sacrifice is blocked

**Why**: These were identified during UX assessment of the input-manager GDD skeleton. Input-manager GDD sections (Detailed Rules, Formulas, Edge Cases, Tuning Knobs, Acceptance Criteria) are all still "[To be designed]" as of this date.
