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

[To be designed]

### States and Transitions

[To be designed]

### Interactions with Other Systems

[To be designed]

## Formulas

[To be designed]

## Edge Cases

[To be designed]

## Dependencies

[To be designed]

## Tuning Knobs

[To be designed]

## Visual/Audio Requirements

[To be designed]

## UI Requirements

[To be designed]

## Acceptance Criteria

[To be designed]

## Open Questions

[To be designed]
