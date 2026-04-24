# Technical Preferences

<!-- Populated by /setup-engine. Updated as the user makes decisions throughout development. -->
<!-- All agents reference this file for project-specific standards and conventions. -->

## Engine & Language

- **Engine**: Unity 6.4 (6000.4.4f1)
- **Language**: C#
- **Rendering**: Universal Render Pipeline (URP) — 2D Renderer with 2D Lights and particle effects
- **Physics**: Unity 2D Physics (Box2D)

## Input & Platform

<!-- Written by /setup-engine. Read by /ux-design, /ux-review, /test-setup, /team-ui, and /dev-story -->
<!-- to scope interaction specs, test helpers, and implementation to the correct input methods. -->

- **Target Platforms**: PC (Steam / Epic)
- **Input Methods**: Keyboard/Mouse, Gamepad
- **Primary Input**: Keyboard/Mouse
- **Gamepad Support**: Full — vertical shmups are gamepad-native; both inputs must feel first-class
- **Touch Support**: None
- **Platform Notes**: All UI must be navigable without mouse hover. Gamepad and keyboard d-pad navigation required for all menus.

## Naming Conventions

- **Classes**: PascalCase (e.g., `PlayerShip`, `EchoFormation`, `PatternAbsorber`)
- **Public fields/properties**: PascalCase (e.g., `MoveSpeed`, `AbsorbRadius`, `MaxEchoCount`)
- **Private fields**: `_camelCase` (e.g., `_currentHealth`, `_echoCount`, `_absorbedPatterns`)
- **Methods**: PascalCase (e.g., `TakeDamage()`, `AbsorbPattern()`, `TriggerSacrifice()`)
- **Signals/Events**: C# `event` + `EventHandler` suffix (e.g., `PatternAbsorbedEventHandler`, `SacrificeTriggeredEventHandler`)
- **Files**: PascalCase matching class (e.g., `PlayerShip.cs`, `EchoFormation.cs`)
- **Scenes/Prefabs**: PascalCase (e.g., `PlayerShip.prefab`, `Stage01_Opening.unity`)
- **Constants**: PascalCase (e.g., `MaxEchoCount`, `DefaultMoveSpeed`)

## Performance Budgets

- **Target Framerate**: 60fps
- **Frame Budget**: 16.6ms
- **Draw Calls**: ≤200 (2D URP with sprite batching enabled)
- **Memory Ceiling**: 512MB

## Testing

- **Framework**: NUnit + Unity Test Framework (Unity 6.4 built-in)
- **Minimum Coverage**: 80%
- **Required Tests**: Balance formulas, gameplay systems (pattern absorption logic, echo formation, sacrifice state machine), networking (if applicable)

## Forbidden Patterns

<!-- Add patterns that should never appear in this project's codebase -->
- [None configured yet — add as architectural decisions are made]

## Allowed Libraries / Addons

<!-- Add approved third-party dependencies here -->
<!-- Only add a library when it is actively being integrated — never speculatively -->
- [None configured yet — add as dependencies are approved]

## Architecture Decisions Log

<!-- Quick reference linking to full ADRs in docs/architecture/ -->
- [No ADRs yet — use /architecture-decision to create one]

## Engine Specialists

<!-- Written by /setup-engine when engine is configured. -->
<!-- Read by /code-review, /architecture-decision, /architecture-review, and team skills -->
<!-- to know which specialist to spawn for engine-specific validation. -->

- **Primary**: unity-specialist
- **Language/Code Specialist**: unity-specialist (C# review — primary covers it)
- **Shader Specialist**: unity-shader-specialist (Shader Graph, HLSL, URP/2D materials)
- **UI Specialist**: unity-ui-specialist (UI Toolkit UXML/USS, UGUI Canvas, runtime UI)
- **Additional Specialists**: unity-addressables-specialist (asset loading, memory management, content catalogs), unity-dots-specialist (ECS, Jobs system, Burst compiler — if bullet-heavy scenes require performance optimization)
- **Routing Notes**: Invoke primary for architecture and general C# code review. Invoke shader specialist for rendering, particle effects, and visual effects. Invoke UI specialist for all interface implementation. Invoke Addressables specialist for asset management systems. Invoke DOTS specialist only if ECS/Jobs patterns are adopted for performance-critical systems (e.g., bulk bullet simulation).

### File Extension Routing

<!-- Skills use this table to select the right specialist per file type. -->

| File Extension / Type | Specialist to Spawn |
|-----------------------|---------------------|
| Game code (.cs files) | unity-specialist |
| Shader / material files (.shader, .shadergraph, .mat) | unity-shader-specialist |
| UI / screen files (.uxml, .uss, Canvas prefabs) | unity-ui-specialist |
| Scene / prefab / level files (.unity, .prefab) | unity-specialist |
| Native extension / plugin files (.dll, native plugins) | unity-specialist |
| General architecture review | unity-specialist |
