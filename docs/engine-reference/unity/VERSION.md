# Unity Engine — Version Reference

| Field | Value |
|-------|-------|
| **Engine Version** | Unity 6.4 (6000.4.4f1) |
| **Release Date** | March 2026 |
| **Project Pinned** | 2026-04-24 |
| **Last Docs Verified** | 2026-04-24 |
| **LLM Knowledge Cutoff** | August 2025 |

## Knowledge Gap Warning

**Risk Level: HIGH** — Unity 6.4 was released March 2026, after the LLM's training cutoff.
Always cross-reference this directory before suggesting Unity API calls.

## Post-Cutoff Version Timeline

| Version | Release | Risk Level | Key Theme |
|---------|---------|------------|-----------|
| Unity 6.0 (6000.0) | Oct 2024 | MEDIUM | Unity 6 launch: URP Render Graph, New Input System default |
| Unity 6.1 (6000.1) | Early 2025 | MEDIUM | Stability + URP improvements |
| Unity 6.2 (6000.2) | Mid 2025 | HIGH | Near LLM cutoff — verify APIs |
| Unity 6.3 (6000.3) | Late 2025 | HIGH | Post-cutoff |
| Unity 6.4 (6000.4) | Mar 2026 | HIGH | ECS as core package, DirectStorage, Project Auditor built-in |

## Key Changes in Unity 6.4 (vs. LLM training data)

### Breaking Changes

- **`RenderGraphSettings.enableRenderCompatibilityMode`** is now read-only (returns `false`). Projects must use URP Render Graph — Compatibility Mode is fully removed.
- **`WeakObjectSceneReference.LoadAsync`** now returns the `Scene` instance directly (API signature changed).
- **`RuntimeContentManager.UnloadScene`** signature changed — accepts only `Scene` instance, not path/handle.
- **ECS Entities package**: `Entities.ForEach` marked obsolete. Use `IJobEntity` and `SystemAPI.Query` instead.
- **ECS `IAspect`** marked obsolete. Use Component and EntityQuery APIs directly.
- **`ComponentLookup.GetRefRWOptional()` / `GetRefROOptional()`** deprecated (internal use only).
- **`EntityManager.CopyEntities()`** deprecated. Use `EntityManager.Instantiate()` instead.

### New Features Relevant to REQUIEM FORMATION

| Feature | Relevance |
|---------|-----------|
| ECS/Entities now a core Editor package (no separate install) | Bullet simulation at scale if DOTS adopted |
| DirectStorage API (Windows Standalone) | Up to 40% faster load times for textures/meshes |
| Project Auditor built into Editor | Free performance profiling — use it during development |
| Improved 2D Renderer in URP | Better 2D lights, shadows, pixel art support |
| Adaptive Performance on PS4/5 and Xbox Series | If console port planned in future |

### Best Practices for Unity 6.4 (vs. older patterns the LLM may suggest)

| Old pattern (LLM may suggest) | Correct Unity 6.4 pattern |
|---|---|
| `Entities.ForEach` | `IJobEntity` + `SystemAPI.Query` |
| `IAspect` | Direct Component + EntityQuery APIs |
| URP Compatibility Mode | URP Render Graph (only option now) |
| `EntityManager.CopyEntities()` | `EntityManager.Instantiate()` |
| Old Input System (`Input.GetAxis`) | New Input System (`InputAction`, `PlayerInput`) |

## Verified Sources

- Official docs: https://docs.unity3d.com/6000.4/Documentation/Manual/
- What's New in 6.4: https://docs.unity3d.com/6000.4/Documentation/Manual/WhatsNewUnity64.html
- Upgrade to 6.4 guide: https://docs.unity3d.com/6000.4/Documentation/Manual/UpgradeGuideUnity64.html
- Breaking changes discussion: https://discussions.unity.com/t/planned-breaking-changes-in-unity-6-4/1682100
- Entities 6.4.0 changelog: https://docs.unity3d.com/Packages/com.unity.entities@6.4/changelog/CHANGELOG.html
