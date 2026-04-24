# Art Bible: REQUIEM FORMATION

*Created: 2026-04-24*
*Status: In Progress*
*Based on Visual Identity Anchor: Modern Retro Specter*

---

## 1. Visual Identity Statement

### One-Line Visual Rule

**"The 8-bit silhouette is law; everything else is permission."**

Any visual element — sprite, effect, UI overlay, lighting bloom — is permitted to exist on screen only if the pixel silhouette of every gameplay-critical object remains readable in outline alone. When two visual elements compete for the same screen space, the one that preserves silhouette legibility wins, unconditionally.

---

### Supporting Principles

**Principle 1 — Silhouette Sovereignty**
Every gameplay-critical sprite — player ship, echoes, enemy units, bullets — must be unambiguously identifiable by its outline at native resolution, with all effects stripped away.

*Design test*: When a new effect is proposed, export the affected sprite as a flat black silhouette against white and confirm it still reads as its object type. Effects may extend outward from the silhouette; they may not bleed inward.

*Pillar anchor*: **모던 레트로** — "Retro silhouette must remain intact; only add modern effects when silhouette clarity is preserved."

---

**Principle 2 — Echo Luminance Hierarchy**
Echoes are not ghosts of failure — they are monuments of sacrifice. Brightness scales with sacrifice order: most recent echo at 80% opacity (#a0c8ff); oldest echo at 30% opacity. A full formation should read as a river of structured cold light, not a smear of noise.

*Design test*: When the screen is crowded with particles and echoes simultaneously, reduce ambient particle density before reducing echo opacity. Echo readability is non-negotiable; particle glamour is expendable. If a designer cannot distinguish Echo 1 from Echo 7 during a dense bullet pattern, the particle system's draw layer or density is adjusted first.

*Pillar anchor*: **잔상이 이야기다** — "Each echo's identifiability" is the explicit tiebreaker.

---

**Principle 3 — Chromatic Event Grammar**
Color does not decorate — it communicates a specific game-state event. Three colors are reserved as semantic signals and may not be repurposed for decoration:
- **Gold (#ffd700)** = Absorption (power gained)
- **Red (#ff4040)** = Sacrifice moment (chosen death)
- **Blue-white (#a0c8ff)** = Echo state (what was given)

Any new effect needing color must draw from the deep-space neutral palette (#0a0a1a–#2a2a4a) or negotiate a new semantic slot with explicit sign-off.

*Design test*: When an artist proposes a new effect color, ask: "Does this color already carry meaning in the grammar?" Any overlap with the three reserved colors requires documented justification.

*Pillar anchor*: **희생은 선택이다** — Color grammar ensures the player always knows when they are being offered a choice versus watching a system event.

---

### Dual-Mode Art System — The Visual Bridge

REQUIEM FORMATION operates in two visual registers:

**Mode A — Full Illustration (Story Screens)**: Anime cel-shaded portrait art. Used for character introduction, pre-stage dialogue, and the final confrontation reveal. Cool palette (silver, royal blue, violet), clean ink outlines, expressive face work.

**Mode B — Pixel Art (Gameplay)**: High-resolution pixel sprites. Grid-aligned, silhouette-sovereign, operating within the deep-space palette.

**Bridge principle**: Both modes share a single palette origin. The illustration character's royal blue jacket maps to the echo blue-white family. Her silver hair maps to the pixel highlight neutral. Her violet eyes anchor the deep-space background tones. When transitioning from illustration to gameplay, the player's color memory carries forward — the pilot just seen IS the pixel sprite now controlled.

**Transition rule**: Story screens use a pixel-art letterbox border / scanline vignette at the frame edge. This border signals "you are at the threshold between story and game." The illustration character's silhouette at any panel edge must reduce to a pixel-readable outline — her design must never rely on interior detail that cannot survive abstraction to ~32×48 pixels.

---

## 2. Mood & Atmosphere

**Design premise**: Each game state must produce a distinct emotional signature. The emotional arc across a session moves: *invitation → mastery tension → devotional peak → grief recognition → exaltation or mourning*. Visual mood is not decoration; it is pacing.

---

### 2.1 Main Menu / Title Screen

| Property | Target |
|---|---|
| **Primary emotion** | Weighted anticipation — the feeling before walking into something you know will cost you something |
| **Lighting character** | Cool, low ambient (~5500K equivalent). Faint directional backlight from below-screen. Single high-contrast focal point: the title logotype |
| **Atmospheric descriptors** | Still / Dormant / Reverent / Distant / Liminal |
| **Energy level** | Contemplative |
| **Mood carrier** | Player ship silhouette, centered, alone on the deep-space field. One echo begins slowly orbiting when idle past 8 seconds — a narrative statement: something has already been sacrificed |

*Pillar anchor — Echoes Are Narrative*: The single idle echo is not tutorial content. It is a narrative declaration.

---

### 2.2 Stage Gameplay (Normal Waves)

| Property | Target |
|---|---|
| **Primary emotion** | Focused hunger — the alertness of a predator in a target-rich environment, actively seeking patterns to absorb |
| **Lighting character** | Mid-range ambient with high local contrast. Each enemy bullet trail is its own light source; Gold absorption flash (#ffd700) must read instantly against the cool field |
| **Atmospheric descriptors** | Dense / Kinetic / Readable / Luminous / Layered |
| **Energy level** | Frenetic (surface) / Measured (player experience target) |
| **Mood carrier** | Bullet pattern geometry — structured spirals, grids, waves that signal learnability. The pattern IS the atmosphere |

*Pillar anchor — Depth Through Flow*: Bullet patterns must never be so visually noisy that structural geometry is obscured. Readability of pattern = readability of absorption opportunity.

---

### 2.3 Boss Encounter

| Property | Target |
|---|---|
| **Primary emotion** | Exhilarated dread — choosing to run toward something overwhelming because the reward justifies it |
| **Lighting character** | Chiaroscuro. Boss emits dominant directional light. Background dims to near-black (#050510). Boss is the entire visual world |
| **Atmospheric descriptors** | Overwhelming / Precise / Theatrical / Pressurized / Monolithic |
| **Energy level** | Tense — denser than normal waves, but with longer telegraphed cycles creating compression-release rhythm |
| **Mood carrier** | Boss scale contrast. The boss occupies more vertical screen space than any normal encounter. Its silhouette communicates weight before its patterns begin |

Safe zones collapse. Boss patterns fill the entire field rather than descending from the top 60%. The player must enter the boss's space to absorb — that spatial compression is the emotional source.

---

### 2.4 Sacrifice Moment

| Property | Target |
|---|---|
| **Primary emotion** | Devotional release — exhausting, clean, and yours. The player made this choice |
| **Lighting character** | Single-frame flash to near-white (#f0f0ff), then hard cut to semantic Red (#ff4040) desaturating outward from the player's last position over ~0.4 seconds. Everything else dims to 20% brightness during this window |
| **Atmospheric descriptors** | Sudden / Centering / Irreversible / Luminous / Sacred |
| **Energy level** | Reverent — a beat-hold in the action |
| **Mood carrier** | The Red desaturation bloom. Reserved exclusively for this moment per Chromatic Event Grammar. The white flash before the red bloom declares: this was intentional |

*Pillar anchor — Sacrifice is Agency*: The flash-to-white communicates *completion*, not failure. A standard death effect (darkness, fragmentation) would undermine the pillar. White flash is the diverging signal.

---

### 2.5 Chapter Narrative Beat (Story Screen)

| Property | Target |
|---|---|
| **Primary emotion** | Earned stillness — the weight of a pause paid for by the previous stage |
| **Lighting character** | Warm-cool split: illustration character lit by cool key (~6500K royal blue), warm ambient fill from behind (~3200K violet-rose). High contrast on the face. Background near-black with pixel letterbox vignette |
| **Atmospheric descriptors** | Intimate / Weighted / Illustrative / Threshold / Confessional |
| **Energy level** | Contemplative |
| **Mood carrier** | The pixel letterbox border — signals "you are at the threshold between story and game." The illustration is always seen through a frame belonging to the gameplay world |

---

### 2.6 Final Confrontation (Facing the Past-Self Echo)

| Property | Target |
|---|---|
| **Primary emotion** | Mirror recognition — seeing your own behavior reflected back as a threat. Not terror. The feeling of being *known* by something trying to destroy you |
| **Lighting character** | Dual-source opposition: player emits warm gold-white; the final echo emits identical gold-white from the opposite direction. The two sources cancel each other's shadows. No safe dark corners |
| **Atmospheric descriptors** | Symmetrical / Vertiginous / Uncanny / Inevitable / Earned |
| **Energy level** | Tense / Reverent simultaneously |
| **Mood carrier** | The echo's pattern mirroring. The final echo reproduces the player's movement patterns from previous sacrifices. Art direction steps back — lower ambient, lower particle density — to not compete with the recognition moment |

*Pillar anchor — Echoes Are Narrative*: The final echo IS the narrative made mechanical. Art direction explicitly reduces visual noise to let the echo's learned behavior be the visual event.

**vs Boss Encounter**: Boss = single chiaroscuro light source (something to face). Final Confrontation = dual equal opposing sources (something that faces back).

---

### 2.7 Victory / Chapter Clear

| Property | Target |
|---|---|
| **Primary emotion** | Bittersweet clarity — not triumph. The stage is clear; the sacrifices remain on permanent display |
| **Lighting character** | Slow single gold-tinted bloom (#ffd700 at ~15% opacity) spreading from the formation outward, fading over ~2 seconds. Returns to cool ambient. Not a celebration flash — a long exhale of light |
| **Atmospheric descriptors** | Residual / Warm / Unresolved / Clear / Elegiac |
| **Energy level** | Measured |
| **Mood carrier** | Full formation at maximum opacity — Victory is the moment when all echoes are visible without combat chaos obscuring them. Victory does not add a new visual element; it finally allows the existing one to be fully seen |

---

### 2.8 Defeat / Continue Screen

| Property | Target |
|---|---|
| **Primary emotion** | Cold suspension — the sensation of the game world freezing around you, not ending |
| **Lighting character** | Rapid desaturation to ~15% saturation over 0.3 seconds. No color shift to red (that is reserved for sacrifice/choice). Defeat is color *removal*, not color *addition*. Inward vignette closes from screen edges |
| **Atmospheric descriptors** | Arrested / Muted / Suspended / Windless / Waiting |
| **Energy level** | Suspended |
| **Mood carrier** | Desaturated echo formation — echoes remain visible as blue-grey outlines. The continue screen's question: "Will you choose to return?" — re-inviting agency without erasing what happened |

*Pillar anchor — Sacrifice is Agency*: Refusing Red for defeat is a direct application of color grammar. Red is chosen sacrifice. Defeat is not chosen. Desaturation rather than red marks that distinction.

---

### Differentiator Summary

| State | Color Temperature | Energy | Differentiating Geometry |
|---|---|---|---|
| Main Menu | Cold / Dormant | Contemplative | Empty field, single waiting ship |
| Stage Gameplay | Cool + local warm | Frenetic/Measured | Distributed vertical zones |
| Boss Encounter | Near-black + boss-as-light | Tense | Collapsed safe zones, full-field patterns |
| Sacrifice Moment | White flash → Red outward | Reverent | Outward bloom geometry |
| Narrative Beat | Warm-cool split (illustration) | Contemplative | Full-frame illustration + letterbox |
| Final Confrontation | Dual opposing gold-white | Tense/Reverent | Symmetric dual-source, minimal ambient |
| Victory | Slow gold pulse | Measured | Full formation at max opacity |
| Defeat | Desaturated to grey | Suspended | Inward vignette, grey echo outlines |

---

## 3. Shape Language

### 3.0 The Governing Principle

**Every shape must earn its legibility at 32 pixels of height.** All shapes organize into two families:

- **Sovereign shapes** — aggressive, angular, asymmetrical. Used for threats: enemies, enemy bullets. Communicate: "this will not yield to you."
- **Formed shapes** — soft-angular hybrids with defined axes and visual weight. Used for player, echoes, absorption indicators. Communicate: "this was made intentional."

These two families must never be confused. Shape is the first signal the player reads — faster than color, faster than motion.

---

### 3.1 Character Silhouette Philosophy

**The 32px test is the design constraint, not a stretch goal.** Export any sprite as a flat black silhouette on white. The object type must be identifiable without context. If it is not, the silhouette is redesigned — not the test.

**Player Ship — "The Formed Wing"**
Compact bilateral wedge with upward-pointing wing tips creating a shallow "W" silhouette. Downward-pointing nose cone establishes direction of travel. Centered mass — balanced, communicating intentionality and control. The cockpit bump carries the suggestion of the pilot's head-and-goggles at scale.

*Emotional*: This ship looks like it chose to be here.
*Pillar anchor — Sacrifice is Agency*: Symmetrical, intentional form. Not erratic or dangerous-looking — a vessel for deliberate action.

**Echo Formation — "Diminishing Formed Wings"**
Echoes share the player ship's base silhouette but are progressively simplified. The oldest echo retains only three reference points (wing tips + mass lump) at 30% opacity. The most recent echo is nearly full resolution. Echoes trail behind and below the player along the axis of movement — they do not flank.

*Emotional*: The trail of simplified ships reads as a procession — structured grief. Each simplified echo is recognizable as the player. A new player should feel "those are me" before being told it.
*Pillar anchor — Echoes Are Narrative*: The silhouette degradation is narrative, not just technical.

**Enemy Archetype 1 — "The Drone" (Small Interceptor)**
Inverted pointed triangle — apex pointing downward, flat across the top. At 32px reads as a downward arrowhead. Inversion of the player ship's geometry is intentional: player points up (agency); drones point down (threat vector).

*Emotional*: Blunt hostility. A wall of descending arrowheads is visually overwhelming but structurally legible.

**Enemy Archetype 2 — "The Weaver" (Pattern Emitter)**
Horizontal disc with two asymmetric trailing spines. Wide and flat. At 32px reads as a lens or iris shape — something that *watches* rather than charges. Does not dive; broadcasts patterns.

*Emotional*: Surveillance and inevitability.
*Pillar anchor — Depth Through Flow*: Its patterns are the readable geometry that create absorption opportunities.

**Enemy Archetype 3 — "The Fortress" (Armored Anchor)**
Heavy rectangular mass with angular protrusions on both sides. Strictly bilateral symmetry shared with the boss family. Hard rectangles, no curves.

*Emotional*: Architecture, not aviation. This does not negotiate.

**Final Boss — "The Mirror Formation"**
The final boss uses the player's own silhouette at 3–4× scale. No new shape is introduced. At boss scale, the familiar wing-tip "W" reads as flanking structures; the cockpit bump reads as a command position.

*Emotional*: Uncanny mirror dread. The player cannot misread this shape — it is legible, and that legibility is what makes it disturbing.
*Pillar anchor — Echoes Are Narrative*: The final boss's shape is not designed to be a boss. It is designed to be the player's own reflection at scale.

---

### 3.2 Environment Geometry

**Dominant geometry: angular grid with two contrast layers.**

Background is strictly pixel-grid-aligned with diagonal and orthogonal lines only — no curves. Star fields, nebula edges, grid overlays, and debris are all grid-aligned and hard-edged.

**Background layer grammar (back to front):**
- **Layer 1 (deepest)**: Near-black field (#0a0a1a). Sparse pinpoint stars — white and blue-white dots, no shapes.
- **Layer 2**: Diagonal parallax grid at ~10% opacity — faint perspective grid implying infinite depth.
- **Layer 3**: Pixel-art nebula geometry. Rectangular patches of deep violet-blue with hard stepped edges (no anti-aliasing). Regional variation markers.
- **Layer 4 (closest to sprite layer)**: Parallax debris — angular chunks, hard rectangles, no curves. Visual rhythm, not hazards.

*Pillar anchor — Modern Retro*: The diagonal perspective grid is the one element that signals "modern" — it gives depth without violating grid alignment.

---

### 3.3 UI Shape Grammar

**The HUD is a pixel-art native element, not a modern overlay.** HUD elements are grid-aligned, rectangular or segmented-angular, drawn at the same resolution as gameplay sprites.

**HUD element shapes:**

- **Health / Life**: Vertical segmented bar — rectangular pixel-art blocks that deplete individually. Not a smooth bar. Each segment is a discrete piece of yourself, not a draining resource.
- **Echo Count Display**: Horizontal row of small ship silhouettes at ~8px height using the player ship silhouette. Active echoes glow at echo blue-white; empty slots are dark. The formation you have built is *visible as a formation*.
- **Absorption Gauge**: Circular segmented ring around the player ship — in world-space, not HUD-edge. Fills clockwise in gold (#ffd700). The gauge reinforces that absorption is performed *with* the ship.
- **Boss Health**: Single horizontal segmented bar at top edge. Larger segments than player health bar.
- **All HUD borders**: 1–2 pixel outlines, no anti-aliasing, no rounded corners permitted.

*Pillar anchor — Modern Retro*: HUD is retro in form (segmented, pixel-native) but modern in spatial integration (absorption gauge lives in world-space). The duality applies to HUD design, not just sprites.

---

### 3.4 Hero Shapes vs. Supporting Shapes

**Properties that make player/echo shapes read as foreground:**

1. **Defined bilateral symmetry** — player and echoes are the only entities with strict vertical bilateral symmetry. Gestalt figure-ground: symmetrical = figure (foreground).
2. **Orientation axis contrast** — player points up; all enemies point down or sideways. The upward-pointing wing geometry creates perpetual figure-contrast against a downward-scrolling threat field.
3. **Echo blue-white as reserved foreground color** — #a0c8ff belongs exclusively to echoes. No enemy, background, or non-echo HUD element uses this hue. Color as foreground signal requires no shape analysis.
4. **Exclusion of rounded geometry from threats** — rounded shapes are assigned to absorption indicators and friendly indicators only. All threat geometry is angular. Rounded = safe/owned; angular = classify as potential threat.

---

### 3.5 Bullet Classification Grammar (Gameplay Readability)

| Source | Shape | Color family | Motion character |
|---|---|---|---|
| Player bullets | Thin vertical rectangles (2px wide, 8–12px tall) | Blue-white (light #a0c8ff) | Fast, straight, upward |
| Enemy bullets | Small filled circles or rhomboids (≤4px) | Enemy-specific — never blue or gold | Patterned, omnidirectional |
| Echo fire | Thin vertical rectangles (3px wide) with faint trailing ghost | Blue-white echo, dimmer than player | Same motion as player, offset laterally |
| Absorption indicator | Diamond/rhombus outline (unfilled) expanding outward | Gold (#ffd700) outline, transparent fill | Expanding ring, decays in 0.3s |
| Sacrifice shockwave | Expanding octagon outline | Red (#ff4040) outline only | Expands to screen edge in ~0.4s |

**Hard rule**: No enemy bullet type uses vertical rectangle geometry. All enemy bullets are circles or rhomboids. The player trains their eye: rectangle going up = mine; circle/rhombus moving toward me = threat.

*Pillar anchor — Depth Through Flow*: Flow state requires pre-conscious threat classification. This grammar makes it automatic, freeing cognitive resources for pattern recognition and absorption decision-making.

---

### Shape Emotional Architecture Summary

| Shape Element | Core Emotion Communicated |
|---|---|
| Player ship | Intentionality, agency, controlled forward motion |
| Echo formation | Memory, sacrifice-as-presence, procession |
| Drones | Blunt aggression, descending threat |
| Weavers | Surveillance, studied pattern, inevitability |
| Fortress | Architecture, immovability |
| Final Boss | Mirror recognition, uncanny familiarity, earned dread |
| Background geometry | Structured infinite space, pixel-native reality |
| HUD elements | World-integrated readout, narrative presence |
| Player bullets | Upward clarity, "mine" |
| Enemy bullets | Omnidirectional threat, "classify as not-mine" |
| Absorption diamond | Event trace, system response to player action |
| Sacrifice octagon | Intentional geometry, chosen event, not-chaos |

---

## 4. Color System

### 4.1 Primary Palette

The palette is not decorative. Every color occupies a semantic position in the game's emotional grammar. 9 total colors: 3 semantic + 6 supporting.

**The Three Semantic Colors (Reserved — never repurposed for decoration)**

| Color | Hex | Semantic Role | Emotional Justification |
|---|---|---|---|
| Absorption Gold | #ffd700 | Absorbing an enemy pattern | Gold communicates that power is being *taken in*, not blocked. Sits at the warm-apex of visible light, physiologically drawing the eye. |
| Sacrifice Red | #ff4040 | The chosen death moment | Red is decision made visible — not danger. The warmth separates it from threat-red. White flash before red declares: this is completion, not failure. |
| Echo Blue-White | #a0c8ff | The echo formation / what sacrifice produced | Light from a dead star — emitted in the past, only now arriving. Cool, structured, slightly beyond natural. Evidence that something happened and it mattered. |

**The Six Supporting Colors**

| Color | Hex | Role | Justification |
|---|---|---|---|
| Deep Space Black | #0a0a1a | Background base | Slight blue tint reads as *space* rather than void — infinite depth quality. Pure black would make all other colors feel pasted on. |
| Mid Space | #1a1a3a | Background mid-value / nebula underlayer | A step toward echo blue, never reaching it. Separates background from foreground without requiring hard outlines. |
| Pilot Royal Blue | #1a3a8a | Player ship body / character design anchor | The pilot's jacket color in illustration carried into gameplay. When you see this blue, you see the protagonist. |
| Highlight Neutral | #c8c8d8 | Pixel highlights / silver hair bridge | The illustration character's silver hair abstracted into a pixel-safe highlight. No saturation — does not compete with any semantic color. |
| Violet Accent | #6a3aaa | Deep accent / eye-color echo / rare foreground detail | The pilot's violet eyes in illustration. Appears sparingly in UI highlights and deep-space nebula. Never used for bullets or enemies. |
| Warm Shadow | #2a1a2a | Warm near-black for boss/sacrifice screens | Violet-tinted dark value for screens that need warmth. Prevents near-black from reading as the same value across contexts. |

---

### 4.2 Enemy Color Grammar

**Enemy colors must satisfy three conditions**: distinguishable from player/echo at a glance; bullets unambiguously non-player-fire; absorbable enemies carry a proximity-readable absorption signal.

| Enemy Type | Hull Color | Bullet Color | Absorbability Signal |
|---|---|---|---|
| Drones (Ch 1–2) | #3a3a5a–#4a4a7a (cool mid-grey-blue) | Pale cyan (#60c8c8) | Mechanic introduced via tutorial |
| Weavers (Ch 2–3) | #4a2a5a (violet-grey) | Soft magenta (#c860a8) | Faint gold edge pulse every 2–3s, visible only at close proximity |
| Fortress (Ch 3–4) | #1a2a3a (deep dark blue-grey) | Hard white (#e0e8f0) | Not absorbable — white bullets are systemic threat, not opportunity |
| Mirror Echoes (Ch 4–5) | #5a3a7a (shifts toward echo blue range) | #90b8f0 (near-match to player echo, slightly shifted) | Not absorbable. Intentional disorientation — distinguish from player echoes by silhouette and opacity, not color alone |
| **Final Boss (Ch 5)** | **Pilot Royal Blue (#1a3a8a)** | **Absorption Gold (#ffd700)** | **No signal — the boss fires your own semantic colors back at you** |

**Final Boss Gold bullets**: Gold meant "power gained." Now it means "power turned against its source." Same color, inverted context, maximum narrative punch. No new art required — purely semantic re-contextualization.

**Bullet readability rule**: No enemy bullet uses vertical rectangle geometry. No enemy bullet uses Royal Blue (#1a3a8a) or Highlight Neutral (#c8c8d8). These exclusions are enforced at asset spec level.

---

### 4.3 Per-Chapter Color Temperature Arc

The background chromatically absorbs the player's sacrifices over time — the world visually "remembers" the echoes through the nebula layer color.

| Chapter | Emotional Register | Background Color Shift | Temperature |
|---|---|---|---|
| 1 — Approach | Invitation | Pure #0a0a1a — no tint modifier | Coolest, 7000K equivalent |
| 2 — Pattern Recognition | Hunger | +Mid Space blue-violet at 20% opacity | 6500K — violet ambience enters |
| 3 — Offering | Devotional Peak | +Warm Shadow (#2a1a2a) as distant nebula | 5800K — first warmth. The environment is responding to sacrifice. |
| 4 — Reflection | Mirror Recognition | +Violet Accent (#6a3aaa) as mid-distant nebula | 5200K — background absorbs echo color |
| 5 — Requiem | Exaltation or Mourning | Oscillates Ch1 cool ↔ Ch4 violet. Final boss: dual gold-white. | Cold with violet residue — full circle, not the same |

**Semantic colors (Gold, Red, Blue-White) never shift** across chapters. The player's signal grammar is constant; the world around it changes.

---

### 4.4 UI Palette

**HUD uses the semantic color grammar in a restrained, off-opacity register.** Full-saturation semantic colors are reserved for world events. 50% opacity Gold in the HUD does not compete with an in-world absorption flash.

| HUD Element | Color | Hex | Note |
|---|---|---|---|
| HUD frame / border | Deep Space Black + Highlight Neutral border | #0a0a1a + #c8c8d8 at 40% | Neutral, recessive |
| Health segments | Echo Blue-White at 50% opacity | #a0c8ff @50% | Holds same color as the echoes they will become |
| Active formation count | Echo Blue-White at 100% | #a0c8ff | Only HUD element allowed full semantic saturation |
| Absorption charge meter | Gold gradient #2a2a0a → #ffd700 | Gradient | Fill motion (left-to-right) is a non-color readability cue |
| Score / info text | Highlight Neutral | #c8c8d8 | Does not compete with any semantic color |
| Danger state (incoming lethal) | Sacrifice Red at 60%, pulsing | #ff4040 @60% | 100% Red = sacrifice (choice); 60% pulsing = danger (threat). Opacity is the distinction |
| Menu prompts | Violet Accent | #6a3aaa | Bridges illustration palette into UI |

---

### 4.5 Colorblind Safety

| Risk Pair | Deficiency | Risk Level | Backup Cues |
|---|---|---|---|
| Gold vs. Red | Deuteranopia / Protanopia | HIGH | **Shape**: Gold = 4-pointed star flare; Red = outward octagon ring. **Position**: Gold always at enemy position; Red always at player position. **Sound**: Gold = ascending chime; Red = descending low tone. **Screen shake**: Sacrifice triggers 0.2s shake — no other event does. |
| Gold vs. Blue-White | Tritanopia | MEDIUM | **Shape**: Gold uses outward ring + star; Blue-White uses trailing ghost + opacity gradient. **Fill direction**: Absorption gauge fills directionally. |
| Red vs. Blue-White | Deuteranopia | LOW | Red occurs at player position; Blue-White occurs at echo positions and trailing. Positional grammar sufficient. |

**Mirror Echoes caveat**: Chapter 4–5 enemy echoes use #90b8f0 (near-match to player echo). These must be distinguished from player echoes by silhouette shape and opacity alone — colorblind players cannot rely on color differentiation here. This is an accepted design cost; silhouette sovereignty is the safety net.

---

### 4.6 Illustration-to-Pixel Palette Bridge

| Illustration Element | Illustration Color | Pixel Bridge | Type |
|---|---|---|---|
| Pilot jacket | Royal blue family (~#1a3a8a mid-tone) | Pilot Royal Blue (#1a3a8a) | Direct carry |
| Silver hair | Cool silver (#b0b8c8–#e8ecf4) | Highlight Neutral (#c8c8d8) | Mid-value carry |
| Violet eyes | Deep-to-bright violet (#3a1a6a–#9a6af0) | Violet Accent (#6a3aaa) | Mid-value carry (portrait-only) |
| Pilot goggles | Dark glass + specular | Deep Space Black + Highlight Neutral | Frame = space black; lens = neutral highlight |
| Story screen background | Near-black + warm violet fill | Deep Space Black + Warm Shadow | Direct carry |

**Transition rule**: The final frame of any story screen must have Royal Blue as the dominant color and Deep Space Black as the background — ensuring the color handshake into gameplay is: Royal Blue → Royal Blue, Deep Space → Deep Space. Story screens may use warm fill light (violet-rose per Section 2.5) but the dominant color at transition-out must anchor to the cool palette.

**Violation to avoid**: Any story screen whose final frame introduces warm-orange or green as dominant. These colors have no gameplay bridge and will make the transition feel discontinuous.

---

## 5. Character Design Direction

### 5.1 Player Ship — Pixel Spec

**Native size**: 32×32px gameplay sprite.

**Silhouette structure**: Bilateral wedge per Section 3. Cockpit bump offset 2px toward nose from geometric center, creating a forward-leaning read without destroying symmetry. Wing tips cut at 45° angles — the "W" outline reads at any distance. Engine glow ports: 2 symmetric pixels at the tail base, rendered in Echo Blue-White (#a0c8ff). These are the only non-silhouette pixels that must survive the silhouette-sovereignty test — they are the player's only color marker in motion.

**Asymmetric detail rule**: A single 1px horizontal channel on the port (left) side, at mid-body height, breaks pure symmetry enough to feel designed rather than procedural. This detail is only visible at 64px and above — the 32px sprite reads as symmetrical for gameplay clarity.

**Color map (32px)**:
- Hull body: Pilot Royal Blue (#1a3a8a) — 70% of sprite area
- Wing surface highlight: Highlight Neutral (#c8c8d8) — 2px edge light on upper wing surface
- Cockpit: Deep Space Black (#0a0a1a) — cockpit reads as void
- Engine glow: Echo Blue-White (#a0c8ff) — 2 tail pixels, always lit

---

### 5.2 Pilot Portrait System

**Reference anchor**: The exam001 reference image establishes 4 permanent identity elements that must appear in every portrait variant without modification:

1. **Silver-grey hair block** — volume above the brow line, partially swept, reading at all scales as the same character
2. **Goggles resting on forehead** — not over eyes. The goggles are a resting object. Eyes are always visible.
3. **Royal blue jacket** — collar and upper lapels always visible at portrait crop
4. **Violet eye iris** — specific eye color. Not blue. Not purple-grey. Violet (#6a3aaa range, pushed toward the bright end in illustration).

These 4 elements are the character's visual signature. Any portrait variant that loses one of them is not this character.

**Portrait frame**: All dialogue portraits are cropped at upper-chest level. Aspect ratio: 1:1.2 (portrait orientation). The face occupies the upper 60% of the frame. Goggles are always visible in the upper 15%.

**3 Required Expression Variants**:

**Expression 1 — Confident Default** *(used for 80%+ of dialogue lines)*
- One brow slightly higher than the other (asymmetric lift — not a full raise, a micro-elevation)
- Eyes half-lidded — not sleepy; the specific half-lid of someone who has seen this before
- Mouth closed, neutral — no smirk, no frown. The absence of performed emotion
- *Character read*: "I know more than I'm choosing to tell you."

**Expression 2 — Rare Vulnerability** *(maximum once per chapter, used sparingly)*
- Both brows level and softened — symmetric, unlike the default
- Eyes open wider than default — 20% more iris visible
- Mouth slightly open, not speaking
- *Character read*: The one moment she is not performing composure. Reserve for maximum narrative impact.
- *Production rule*: This expression must never appear in combat HUD dialogue. Story screens only.

**Expression 3 — Confrontation Reveal** *(final boss sequence only)*
- Chin raised 3–5px from default chin position — looking down the nose at the player
- Eyes open, direct gaze — no half-lid
- Violet iris saturation pushed 15% warmer and brighter than default — a color shift only readable at portrait size, not on the in-game sprite
- *Character read*: The mask fully off. She knows she is the final boss.
- *Production rule*: The violet saturation shift requires a separate portrait variant — it cannot be achieved via tinting because the tint would affect the jacket blue and hair silver. A dedicated asset is required.

---

### 5.3 Enemy Pixel Specifications

**Drone — 16×16px**
- Shape: Pure inverted triangle. Apex points down, flat edge across top.
- Hull color: Cool mid-grey (#3a3a5a). No highlight. Flat fill with 1px darker edge.
- No interior detail at 16px — the shape IS the design.
- *Absorbability*: Yes. Absorption tutorial enemy. No special visual signal at this stage — absorption is introduced via tutorial, not visual prompt.
- Bullets: Pale cyan (#60c8c8), small filled circles (2px diameter).

**Weaver — 24×24px**
- Shape: Horizontal lens (ellipse-approximated in pixel grid) with two asymmetric trailing spines. Left spine is 2px longer than right.
- Hull color: Violet-grey (#4a2a5a). 1px highlight on the lens center (Highlight Neutral).
- Absorption signal: Faint gold outline (#ffd700 at 30% opacity) pulses outward from the lens edge every 2–3 seconds. Only readable at close proximity (within 48px of player). Signal is on a separate sprite layer, not baked into the hull.
- Bullets: Soft magenta (#c860a8), small circles/arc patterns.

**Fortress — 32×32px**
- Shape: Heavy rectangle with angular protrusions. Bilateral symmetry — shares shape grammar with boss family (Section 3).
- Hull color: Deep dark blue-grey (#1a2a3a). Hard white highlight channels (2×1px each) along the protrusion edges.
- **No gold pulse. No absorption signal. Ever.** The absence of the gold signal IS the communication: this is not absorbable.
- Bullets: Hard white (#e0e8f0) — the only enemy that fires white bullets. White = architectural threat, not pattern opportunity.

---

### 5.4 Echo 7-Stage Degradation

As an echo ages (older sacrifices), it simplifies progressively. **Critical rule: interior detail dissolves before the outline.** The silhouette is always the last element to go.

| Stage | Echo Age | Visual State | Opacity |
|---|---|---|---|
| 1 | Newest | Full 32px sprite, all hull detail | 80% |
| 2 | — | Interior color lost — hull outline + cockpit only | 75% |
| 3 | — | Cockpit lost — wing surface highlight + outline only | 65% |
| 4 | — | Highlights lost — outline only, full resolution | 55% |
| 5 | — | Outline simplified — 16px equivalent resolution | 45% |
| 6 | — | Outline further simplified — 8px equivalent | 35% |
| 7 | Oldest | 3-point "W" shape — two wing tips + mass lump only | 30% |

All stages render in Echo Blue-White (#a0c8ff). No other color is used at any stage.

**Stage 7 is still recognizable as the player ship.** The 3-point "W" is the minimum legible reference. If a player cannot identify Stage 7 as a ship silhouette, simplify the degradation progression — do not reduce Stage 7 further.

*Engine implementation note*: Degradation stages are pre-authored as separate sprites, not computed via shader erosion. This ensures exact silhouette control at each stage.

---

### 5.5 LOD Philosophy

**3 production contexts — each requires its own asset:**

| Context | Size | Pipeline | Usage |
|---|---|---|---|
| Gameplay sprite | 32×32px | Pixel-native, no anti-aliasing | All in-flight gameplay, formation display |
| Cutscene sprite | 64–96px | Pixel-native at double resolution, same palette | Stage clear, sacrifice animation, approach sequences |
| Dialogue portrait | 128×160px illustrated | Cel-shaded illustration, full color palette | Dialogue screens, chapter intro, confrontation reveal |

**Derivation rule**: The 64–96px cutscene sprite must be redrawn from the 32px sprite — scaled up, then redrawn pixel-for-pixel at the higher resolution. It must NOT be derived by upscaling the illustration. The illustration and gameplay sprite share the same color origin but have separate production pipelines.

**Why this matters**: Downscaling the illustration to 64px produces a different visual DNA than upscaling the pixel art. The former reads as "compressed anime"; the latter reads as "expanded retro." The game's bridge principle requires the latter to be legible in both directions.

---

## 6. Environment Design Language

### 6.1 Star Field — Density by Chapter

Stars serve as the primary "memory counter" — the field grows denser as the formation grows, then thins as sacrifices accumulate toward the final confrontation.

| Chapter | Star Count | Narrative Justification |
|---|---|---|
| 1 — Approach | 80–100 | Emptiness. The player has not yet left a mark on this space. |
| 2 — Pattern Recognition | 120–140 | Accumulation begins. The pilot's presence is registering. |
| 3 — Offering | 140–160 | Densest point. Formation is largest; the world has absorbed the most. |
| 4 — Reflection | 140–160 | Density held — but the motif shifts from growth to mirror. |
| 5 — Requiem | 100–120 | Sparse return. The formation has been spent. The field thins toward the end. |

Star colors: white (#f0f0f8) and blue-white (#c0d0f0). No warm-toned stars. All stars are 1px points — no halos, no lens flare at star level. Stars do not animate beyond parallax scroll.

---

### 6.2 4-Layer Parallax System

All layers scroll downward at speeds relative to `worldScrollSpeed` (a global float). Layer speeds are multipliers applied to the base scroll rate.

| Layer | Speed | Content | Resolution Unit |
|---|---|---|---|
| Layer 1 (deepest) | 0.05× | Star field — near-static | 512×512px tile |
| Layer 2 | 0.15× | Diagonal perspective grid (10% opacity, angular only) | 512×512px tile |
| Layer 3 | 0.30× | Nebula patches — tinted at runtime from neutral library | 512×512px tile |
| Layer 4 (closest to sprite layer) | 0.65× | Debris — angular hull fragments, no hazard collision | 512×512px tile |

**Tile unit**: All background layers use 512×512px tiles, seamlessly tiling via Unity 6.4 Tilemap. The tile is the production unit, not the screen.

**Layer 2 rule**: The diagonal perspective grid is grid-aligned at 45°. Only orthogonal and 45° lines — no curves, no irregular angles. This is the "modern depth signal" from Section 3. Opacity ceiling: 10%. If the grid is reading heavier than 10%, reduce before adjusting other layers.

**Layer 3 — Nebula Library**: 16 pre-authored patches across 4 categories:
- **Wisp** (4 patches): Thin horizontal streaks, 2–4px height, long horizontal run
- **Cloud** (4 patches): Rectangular mass, soft hard-stepped edges, 32–64px square range
- **Veil** (4 patches): Near-full-tile gradient overlay, maximum 20% opacity
- **Shard** (4 patches): Angular fragments — triangle and parallelogram shapes, 8–16px

All 16 patches are authored in single-channel greyscale. Color is applied at runtime via the Unity Tilemap color property. Per-chapter tint values:

| Chapter | Nebula Tint | Effect |
|---|---|---|
| 1 | #1a1a3a (Mid Space) | Pure cool — no emotional color yet |
| 2 | #2a1a4a (Mid Space + slight violet) | Violet ambience enters |
| 3 | #2a1a2a (Warm Shadow) | First warmth — environment responding to sacrifice |
| 4 | #4a2a6a (Violet Accent towards mid) | Deep violet — background absorbs echo color |
| 5 | Oscillates Ch1 ↔ Ch4 values over 8-bar cycles | Full circle, not the same as Ch1 |

---

### 6.3 Per-Chapter Environment Motifs

Each chapter's environment layer contains a unique visual motif that communicates the chapter's narrative state without text. All motifs are in Layer 3 or Layer 4 — never Layer 1 or 2.

**Chapter 1 — Approach**: Empty grid. No motifs. The absence is the statement.

**Chapter 2 — Pattern Recognition**: Fractured grid line traces appear in Layer 3 — thin lines that look like collision aftermath, as if something already passed through here. These are horizontal and diagonal scratch-marks, 1px wide, rendered at low opacity in the Highlight Neutral (#c8c8d8 at 15%).

**Chapter 3 — Offering**: Faint formation ghost outlines appear in Layer 3. These are echo-shaped "fossils" — ship silhouettes at Stage 7 degradation level, embedded in the nebula. They do not move with the player's formation. They are spatial memory.

**Chapter 4 — Reflection**: Mirror-axis symmetry lines in Layer 3 — thin vertical lines at screen center and 25%/75% positions. They divide the background space into mirrored halves. Enemy patterns in this chapter are designed to feel like they reflect these axes.

**Chapter 5 — Requiem**: Echo constellation in Layer 1. A pattern of 7 star-point formations arranged in the shape of the player's full 7-echo formation. This constellation scrolls with Layer 1 (0.05×) — near-static. During the final boss fight, this constellation remains. The boss fights beneath a sky made of the sacrifices.

---

### 6.4 Boss Transition

**Duration**: 18 frames at 60fps = 0.3 seconds.

**Sequence** (back-to-front layer fade):
1. Frames 1–6: Layer 1 (stars) fades from current opacity to 20%
2. Frames 4–10: Layer 2 (grid) fades to 0% — grid disappears completely
3. Frames 7–14: Layer 3 (nebula) fades to 10% opacity
4. Frames 12–18: Layer 4 (debris) fades to 0%

At frame 18, the boss sprite enters from top of screen. Boss becomes the sole light source per Section 2.3. The near-black background (#050510) is the result of all layers at minimal opacity — not a hard cut to black.

**Reverse transition** (boss defeated): Reverse the fade order (front-to-back), over 24 frames / 0.4 seconds. Slightly slower than entry — a moment to exhale.

---

### 6.5 Debris Progression

Layer 4 debris evolves across chapters. Debris is visual rhythm, not hazard collision.

| Chapter | Debris Content | Visual Meaning |
|---|---|---|
| 1 | None | Unclaimed space |
| 2 | Anonymous hull splinters — small rectangles, no recognizable shape | Something has been fought here before |
| 3 | Ship-silhouette fragments — 8px readable-as-ship outlines | Named losses |
| 4 | Formation-mass fragments — groups of 3–4 silhouette fragments moving in loose formation | Losses that traveled together |
| 5 | All previous types co-existing | History made visible. The player scrolls through their own past. |

All debris is rendered in #2a2a4a–#3a3a6a range — darker than the sprite layer, lighter than Layer 1. Debris is always behind the sprite layer (lower z-order than enemies and player).

---

### 6.6 Environmental Storytelling Guidelines

The environment must tell the chapter's story without text. Rules for what visual elements carry:

1. **Star density is emotional density** — the world's response to the player's accumulation of sacrifice
2. **Motif progression is cumulative** — later chapters show earlier motifs plus new ones (Ch5 has all motifs co-present, though faded)
3. **Debris is biography** — what you see floating past describes what happened before the player arrived
4. **Echo constellation is testimony** — the final boss fights under a sky that remembers. No dialogue needed.
5. **Nebula color temperature is the thermometer of sacrifice** — warmer = more given. The world absorbs what the player offers.

**What the environment never does**:
- Communicate danger or obstacles (environment has no hazard collision)
- React in real-time to the echo formation's current state (chapter-level only, not frame-level)
- Use colors outside the approved palette, including for nebula tints

---

## 7. UI / HUD Visual Direction

### 7.1 Diegetic vs. Screen-Space Split

**Governing principle**: HUD elements live where they are most honest about what they represent. Elements that describe the player ship's current state live on or near the player ship in world-space. Elements that describe the session's systemic state (score, chapter progress, boss health) live at the screen edge as screen-space overlays.

**Diegetic (World-Space) Elements**

| Element | Position | Justification |
|---|---|---|
| Absorption Gauge | Circular segmented ring orbiting the player ship, radius 24–28px from ship center | Absorption is performed by the ship's body. The gauge confirms the act is happening to the object doing the absorbing. |
| Echo Formation Display | Trailing below-and-behind the player along movement axis | Echoes are world-objects, not HUD readouts. The formation IS the display. |

The Absorption Gauge orbits in world-space and scrolls with the player — never anchored to a screen-space corner. When the player moves, the gauge moves. When a screen shake event occurs, the gauge participates in the shake.

**Screen-Space (Overlay) Elements**

| Element | Screen Position | Justification |
|---|---|---|
| Health bar (segmented vertical) | Top-left corner, vertical stack | Health is a systemic resource, not a spatial one. Edge placement keeps it recessive during play. |
| Score | Top-right corner, right-aligned | Meta-session data. Periphery. |
| Boss Health | Top edge, center, horizontal segmented bar | Requires split-attention read during boss phases. Top-center is highest-attention without obstructing play field. |
| Chapter / Stage indicator | Top-left, beneath health bar, small | Low-urgency, contextual. |

**Do not do**: Place the absorption gauge as a fixed screen-edge arc or bar. This breaks the diegetic principle and converts a spatial relationship into a bureaucratic readout.

---

### 7.2 Typography Direction

**Two type voices — never mixed in the same screen zone.**

**Voice 1 — Pixel Type (Gameplay & HUD)**

Monospaced, strict pixel grid, no sub-pixel rendering, no anti-aliasing. Cap height: 7px at 1× scale (renders as 14px at 2×). All pixel type must be legible as pure black silhouette against white.

Requirements for font selection:
- Grid-perfect 8×8 character cell (or 5×7 with 1px gap) for all numerics
- Zero-width notch differentiation between `0` (zero) and `O` (letter) — mandatory for score and health readouts
- Identical pixel weight for all digits (monospace numerics) — score counter must not shift in width as digits change
- No decorative serifs — pixel serifs only (1px right-angle terminal strokes)

| Use case | Screen size at 2× | Color |
|---|---|---|
| Score counter | 14px | Highlight Neutral (#c8c8d8) |
| HUD numeric readouts | 14px | Highlight Neutral (#c8c8d8) |
| Boss health label | 10px | Highlight Neutral at 60% |
| Chapter stage indicator | 10px | Highlight Neutral at 60% |
| Danger / alert text | 14px | Sacrifice Red (#ff4040) at 60% pulsing |

**Voice 2 — Illustration Type (Menus & Story Screens)**

Clean sans-serif with modest geometric personality — not grotesque-wide, not humanist-curved. Legible at 16–32px. Anti-aliasing permitted in this voice only; this type never appears over gameplay sprites. The type is not retro for its own sake — it is modern type in a retro container, paralleling the Modern Retro pillar.

| Use case | Size | Color |
|---|---|---|
| Title logotype "REQUIEM FORMATION" | 48–64px, Bold, +40 tracking | Highlight Neutral (#c8c8d8) + 2px Pilot Royal Blue (#1a3a8a) outline |
| Chapter title | 32px, Medium | Highlight Neutral (#c8c8d8) |
| Menu items | 20px, Regular | Highlight Neutral; selected: Violet Accent (#6a3aaa) |
| Dialogue text body | 16px, Regular | Highlight Neutral (#c8c8d8) |
| Dialogue speaker label | 16px, Bold | Absorption Gold (#ffd700) |
| Settings labels | 16px, Regular | Highlight Neutral at 80% |
| Button prompts | 14px, Regular | Violet Accent (#6a3aaa) |

**Type mixing rule**: Pixel type and illustration type never on-screen simultaneously in the same visual zone. The pause menu — which overlays gameplay — uses illustration type over a darkened overlay that visually de-activates the gameplay space. The overlay signals: "you are not currently in pixel space."

**Do not do**: Use a pixel-style font with irregular cap heights across characters, or use illustration type directly over live gameplay sprites.

---

### 7.3 Iconography Style

**Governing principle**: Icons are miniature pixel-art objects, not symbolic glyphs. An icon for a life is not a heart — it is a ship silhouette. The iconography system treats icons as members of the same visual family as gameplay sprites.

**Icon grammar**: Flat, single-layer, no gradients. 1px border outline in the icon's semantic color. Interior fill at 60–70% opacity. All icons are square bounding-box with content occupying the inner 80%. No rounded corners, no bevels, no drop shadows, no glow effects.

| Icon type | Native size | Display size | Color |
|---|---|---|---|
| Health segment | 8×8px | 16×16px at 2× | Echo Blue-White (#a0c8ff) at 50%; depleted: Deep Space Black fill, Highlight Neutral border at 30% |
| Echo slot (active) | 8×8px ship silhouette | 8px height row | Echo Blue-White (#a0c8ff) at 100% |
| Echo slot (empty) | 8×8px ship outline | 8px height row | Highlight Neutral (#c8c8d8) at 20% — ghost indicating the slot exists |
| Absorption gauge segment | 2px arc segment | Part of 24–28px radius ring | Gold (#ffd700); unfilled: Highlight Neutral at 15% |
| Menu item icon | 16×16px | 16×16px | Violet Accent outline, Deep Space Black fill |
| Gamepad button prompt | 12×12px | 12×12px | Highlight Neutral border, Deep Space Black fill, glyph in Violet Accent |

**Echo slot specification**: The echo slot icon IS the Stage 7 degradation silhouette from Section 5.4 at 8px — the minimum-legible ship shape (3-point "W" + mass lump). Active slots: filled blue-white. Empty slots: ghost outlines. The row reads as "this is my formation, these are its vacancies."

**Health icon specification**: Each health segment is an 8×8px filled rectangle with a 1px Highlight Neutral border — not a ship silhouette. Health is a resource unit, not an echo-formation concept. Using different icon vocabularies for health vs. echoes preserves the semantic boundary.

**Do not do**: Use heart icons, shield icons, or star icons for any status element. The game's iconography system has no decorative symbols.

---

### 7.4 UI Animation Feel

**Governing principle**: UI motion is either a snap or a drift. There is no bounce, no spring, no overshoot. The emotional register of this game — deliberate, weighted, non-forgiving — does not permit playful easing.

**Profile 1 — Hard Snap (≤ 4 frames / ≤ 67ms)**
Used for all HUD state changes triggered by gameplay events: health segment depleting, echo slot filling, score updating, absorption gauge segment completing, boss health phase changing.

Character: State simply changes between frames. No interpolation visible. The HUD does not wait for the game — it acknowledges what already happened.

**Profile 2 — Linear Drift (6–12 frames / 100–200ms)**
Used for menu entry/exit, dialogue portrait sliding in, pause overlay fading, chapter title appearing.

Character: Constant velocity, no acceleration curve. Moves like a read-head, not a pendulum. The constant-velocity drift feels procedural and considered, not organic.

**Easing specification**: Linear only for Profile 2. No ease-in, no ease-out. Exception: the sacrifice Red bloom (Section 2.4) and victory Gold pulse (Section 2.7) are handled by the VFX system under their own timing rules.

**Event-specific HUD responses**

| Event | HUD Response | Profile |
|---|---|---|
| Health segment lost | Hard-snaps to depleted state (black fill, dim border) | Hard Snap |
| Echo slot filled | New slot hard-snaps to active Echo Blue-White | Hard Snap |
| Absorption ring completes | Full ring: 2-frame white flash on outermost pixel, then steady gold | Hard Snap + 2-frame flash |
| Score increases | Value hard-snaps to new number. No scroll, no counter animation. | Hard Snap |
| Boss phase clears | Phase segment group hard-snaps to depleted | Hard Snap |
| Danger state | Sacrifice Red at 60%, 30-frame cycle: 15 frames on / 15 frames at 30% (hard alternation) | Repeating Hard Snap |

**Menu motion direction**
- Pause menu: fades in from 0% → 85% opacity. Does not slide — fading signals suspension.
- Title screen elements: drift upward from below frame on load, linear velocity, stop without deceleration.
- Chapter select items: drift left-to-right in sequence, 2-frame stagger between items.
- Settings panel: hard-cut swap (same pause state layer, not a journey).

**Do not do**: Apply spring, bounce, or ease-out to any HUD element responding to a gameplay event. A bouncing health bar segment trivializes damage.

---

### 7.5 Dialogue Portrait Integration

**Governing principle**: The pilot's portrait appears at the threshold between story and game. It never fully enters the gameplay field's central 60% of screen width.

**Standard story screen dialogue (full narrative beat — no active gameplay)**
- Portrait occupies the left 30% of the screen, anchored to the bottom-left corner, within the pixel letterbox border.
- Dialogue text box occupies the lower-right 65% of the screen (5% gutter between portrait and text box).
- Speaker label above text box: Absorption Gold (#ffd700), Illustration Type Bold 16px.
- Portrait is a static frame — only the expression variant changes between dialogue lines (hard-cut, 1 frame).
- Entry: drifts in from left edge at linear velocity (8 frames / 133ms). Exit: drifts back left, same duration.

**Portrait frame design**
- 2px Pilot Royal Blue (#1a3a8a) outer frame, 1px Highlight Neutral (#c8c8d8) inner hairline.
- HUD border grammar: no rounded corners, no anti-aliasing, 90° corners only.
- Portrait background: Deep Space Black (#0a0a1a) with Warm Shadow (#2a1a2a) fill at 30%.

**In-flight dialogue (active gameplay — urgent transmission only)**
- Top-left corner, face-crop only (upper 50% of standard portrait, ~64×80px display size).
- Text box appears immediately below, same width.
- No entry animation — hard snap. Urgency communicated by absence of drift-in.
- Auto-advances on timer or player dismiss.
- Expression locked to Confident Default only. Rare Vulnerability is forbidden in this context.

**Do not do**: Slide the portrait into the play field's central zone, use it as a full-screen overlay during gameplay, or animate expression transitions with a morph or crossfade. The pilot comments on the game; she does not interrupt it.

---

### 7.6 Menu System Visual Style

**Governing principle**: Menus are the game's ante-room — illustration type voice, full color palette, but framed in the same pixel-art container all screens share. A menu is not a break from the game's world; it is the game's world at rest.

**Title Screen**
- Full-screen Deep Space Black (#0a0a1a). Player ship silhouette centered at 45% screen height.
- Title logotype at 25% screen height, horizontally centered.
- 1px Highlight Neutral horizontal rule below logotype, full screen width.
- Navigation items: vertical list below the rule, center-screen, 8px spacing. Illustration type 20px. Selected item shifts to Violet Accent (#6a3aaa) — color shift only, no selection box, no arrow.
- The idle echo orbit from Section 2.1 runs as a live gameplay element behind the title UI — the menu is drawn over the game world, which is already running.

**Pause Menu**
- The pause menu overlays gameplay. Gameplay beneath desaturates to **40% saturation** (not a black overlay — the game world "holds" at reduced vitality).
- Over the desaturated gameplay: centered panel in Deep Space Black at 85% opacity, 2px Highlight Neutral border, no rounded corners, 16px internal padding, sized to content.
- Why 40% desaturation rather than black overlay: suspension of the game world (consistent with Section 2.8 where desaturation = "arrested"). 40% is clearly different from normal play (100%) and defeat (15%).

**Chapter Select**
- Background: Chapter 3 nebula tint (#2a1a2a Warm Shadow) — the world at its most-given state. All chapters are accessible from the peak of sacrifice.
- 5 chapter entries as a horizontal row of 64×64px pixel-art tiles: chapter number (pixel type, top) + representative chapter motif silhouette (center).
- Unlocked: full Highlight Neutral tile. Locked: 20% opacity with Deep Space Black tint overlay.
- Selected tile: 1px Violet Accent (#6a3aaa) border. No scale change, no elevation.

**Settings**
- Pause menu panel container, expanded to 60% screen width.
- Settings labels: Illustration type 16px, Highlight Neutral at 80%. Current value: Highlight Neutral at 100%.
- Active selection cursor: 2px Violet Accent border on the current row (full row width).
- Toggle states: On = Absorption Gold (#ffd700); Off = Highlight Neutral at 30%. (Gold = power gained; an enabled feature is, at minimum, available capability.)

**Shared Menu Grammar — all menus, no exceptions**
1. HUD border grammar: 1–2px outlines, no rounded corners, no anti-aliasing on borders.
2. No drop shadows, inner glows, or blur effects on panel edges. Panel border is the only depth signal.
3. Navigation by color shift only — no highlight box, no selection arrow.
4. All menus fully navigable by gamepad d-pad and keyboard arrow keys without mouse.
5. Menu backgrounds never use Gold, Red, or Blue-White as background tints. Semantic colors are reserved for world events.

**Do not do**: Use a frosted-glass blur overlay for pause, animated gradient backgrounds on the title screen, or a glow-effect selection box. The menus must feel built in the same world as the gameplay — not styled differently because "it is just a menu."

---

## 8. Asset Standards

### 8.1 Production Pipeline

**Source tool**: Aseprite (all pixel-art sprites and animations). Illustration portraits may use any vector/raster tool, but final exports must conform to the spec in 8.6.

**Pipeline split**:
- Source files (`.aseprite`, `.psd`, `.clip`) live in `assets/art/source/` — tracked in Git, never imported by Unity directly.
- Unity imports exported PNGs from `assets/art/sprites/` (gameplay), `assets/art/backgrounds/`, `assets/art/ui/`, `assets/art/portraits/`.
- When a source file is updated, the artist exports a new PNG to the correct import folder. Unity reimports automatically.

This separation keeps Git diffs meaningful (source files show intent; PNG diffs show pixel output) and allows outsourcers to deliver final PNGs without requiring Aseprite access.

---

### 8.2 Naming Convention

All art files use this format: `[category]_[object]_[state]_[nativeRes].png`

| Segment | Values | Examples |
|---|---|---|
| category | `ship`, `enemy`, `bullet`, `echo`, `vfx`, `bg`, `ui`, `portrait` | `ship`, `enemy`, `bg` |
| object | Object identity slug | `player`, `drone`, `weaver`, `fortress`, `nebula_wisp01` |
| state | Animation state or variant | `idle`, `move`, `death`, `hit`, `confident`, `layer1` |
| nativeRes | Native pixel dimension (square: single number; non-square: `WxH`) | `32`, `16`, `512`, `128x160` |

**Examples:**
- `ship_player_idle_32.png`
- `enemy_drone_move_16.png`
- `enemy_weaver_idle_24.png`
- `bg_nebula_wisp01_512.png`
- `portrait_pilot_confident_128x160.png`
- `portrait_pilot_vulnerable_128x160.png`
- `ui_echo_slot_active_8.png`
- `vfx_sacrifice_bloom_32.png`

Animation frames: append `_f[frame number]` before the extension if frames are individual files rather than a sprite sheet — e.g., `ship_player_idle_32_f01.png`, `ship_player_idle_32_f02.png`.

**No version numbers in filenames.** Git provides versioning. `ship_player_idle_32_v2.png` is forbidden.

---

### 8.3 Texture Resolution Tiers

**Five tiers. No intermediate sizes.**

| Tier | Native Size | Contents |
|---|---|---|
| Micro | 16×16px | Drone enemy, small bullets/VFX |
| Small | 24×24px | Weaver enemy |
| Gameplay | 32×32px | Player ship, Fortress, most enemies, HUD icons, 32px VFX |
| Cutscene | 64–96px height | Cutscene sprites — must be redrawn from 32px source, NOT downscaled from portrait |
| Portrait | 128×160px | Illustrated pilot portrait variants |
| Background tile | 512×512px | All parallax layer tiles |

**The intermediate size rule**: A sprite authored at 48px because "it reads better" is a production error. The five tiers are the only valid sizes. If a sprite needs more detail at gameplay size, the solution is a better 32px design — not a new tier. Enforce this at source authoring, not at import.

---

### 8.4 Unity Import Settings

All sprites must use the following settings. These are enforced via an `AssetPostprocessor` script at `src/Tools/Editor/PixelArtAssetPostprocessor.cs` (requires lead-programmer approval before implementation).

| Setting | Required Value | Why |
|---|---|---|
| Texture Type | `Sprite (2D and UI)` | Enables sprite mode, PPU, atlas packing |
| Filter Mode | **`Point (no filter)`** | Mandatory for pixel art — Bilinear/Trilinear blurs pixel edges |
| Generate Mip Maps | **Disabled** | Mip maps waste 33% memory and cause blurry sprites at runtime |
| Compression | **`RGBA 32 bit` (PC platform override)** | DXT/BC block compression introduces banding on a 9-color palette |
| Pixels Per Unit (PPU) | **1** for all sprites | 1 texture pixel = 1 Unity world unit; display scaling handled at Camera/Canvas level |
| Alpha Is Transparency | Enabled | Prevents color bleeding at transparent pixel edges |
| Read/Write Enabled | **Disabled** (default) | Enable only where runtime pixel reads are explicitly required; doubles GPU memory |
| sRGB | Enabled for color sprites; **Disabled** for nebula greyscale masks | Nebula patches are linear-space masks tinted at runtime — gamma correction would distort the tint |
| Wrap Mode | `Clamp` for sprites and portraits; `Repeat` for background tiles | Clamp prevents edge bleeding in atlases; background tiles require Repeat for seamless scroll |
| Max Size | See per-category limits in 8.5 | Prevents oversized source files from bloating build |

**Blocking violations** (must be corrected before any build):
- `Filter Mode: Bilinear` or `Trilinear` on any sprite
- `Generate Mip Maps: Enabled` on any 2D sprite
- Any lossy block compression (`DXT1`, `DXT5`, `BC7`, `ETC2`) on pixel-art sprites
- `Read/Write Enabled` on sprites that do not require CPU pixel access
- `Allow Rotation: Enabled` in Sprite Atlas V2 (rotated pixel-art samples incorrectly under Point filter)
- `Pixels Per Unit` mismatched between sprite categories

---

### 8.5 Sprite Atlases and Memory Budgets

**Atlas system**: Unity Sprite Atlas V2. Do not use the legacy Sprite Packer.

**6 production atlases:**

| Atlas | Contents | Max Size | Padding |
|---|---|---|---|
| `Gameplay_Ships` | Player ship + all enemy types | 512×512 | 2px |
| `Gameplay_Bullets` | All bullet and projectile sprites | 512×512 | 2px |
| `Gameplay_FX` | Explosion frames, hit sparks, VFX sprites | 512×512 | 4px |
| `UI_HUD` | HUD icons, echo slot icons, life segments | 512×512 | 2px |
| `UI_Menus` | Menu panels, button states, borders | 1024×1024 | 4px |
| `Portraits` | All pilot portrait variants + cutscene sprites | 512×512 | 4px |

**Background tiles are excluded from all atlases.** Tilemap tiles require `Wrap Mode: Repeat`, which is incompatible with atlas sub-rects. Background sprites live as direct texture references.

**Sprite Atlas V2 settings**: Allow Rotation: Disabled. Tight Packing: Disabled. Include in Build: Enabled.

**Texture memory budget** (~128MB allocation from 512MB total ceiling):

| Category | Format | Per-unit | Count | Budget |
|---|---|---|---|---|
| Gameplay sprite atlases | RGBA32 | 1MB (512×512) | 3 | 3MB |
| Background tiles | RGBA32 | 1MB (512×512) | 4 layers | 4MB |
| Nebula library atlas | R8 (single-channel) | 0.25MB (512×512) | 1 atlas | 0.25MB |
| UI atlases | RGBA32 | 1MB | 2 | 2MB |
| Portrait atlas | RGBA32 | 1MB | 1 | 1MB |
| Headroom | — | — | — | ~117MB |

Run **Project Auditor** (`Window > Analysis > Project Auditor` — built into Unity 6.4) after every batch of new imports to audit texture memory usage.

---

### 8.6 Materials and Shaders

| Sprite category | Required shader |
|---|---|
| Gameplay sprites receiving 2D Lights | `Universal Render Pipeline/2D/Sprite-Lit-Default` |
| Background tiles (no 2D Lights) | `Universal Render Pipeline/2D/Sprite-Unlit-Default` |
| Nebula tint masks | Custom Shader Graph: greyscale mask × `_Color` → alpha-premultiplied output. Runtime tint via `SpriteRenderer.color` |
| Post-process / screen effects | URP Render Graph `ScriptableRendererFeature` implementing `RecordRenderGraph()` |

**Max 10 unique materials per gameplay scene.** All sprites in the same atlas share one material instance. Per-instance hit-flash or tint overrides use `MaterialPropertyBlock` — do not create duplicate material instances for per-enemy overrides.

> **Unity 6.4 breaking change**: `RenderGraphSettings.enableRenderCompatibilityMode` is permanently `false`. Any `ScriptableRendererFeature` using the old `Execute()` override will not function. All custom render passes must implement `RecordRenderGraph()`. Validate all post-process effects before milestone builds.

---

### 8.7 Animation Import

**Animation system**: Animator Controller (Mecanim) with sprite-swap animation clips. The Legacy `Animation` component is forbidden.

| Setting | Required value |
|---|---|
| Sprite Mode on source texture | `Multiple` — slice via Sprite Editor using `Grid By Cell Size` at the sprite's native resolution |
| Gameplay clip frame rate | **12fps** (standard pixel-art frame rate) |
| Cutscene clip frame rate | **24fps** |
| Clip naming | `[SpriteName]_[StateName]` — e.g., `PlayerShip_Idle`, `DroneEnemy_Move` |
| Loop Time | Enabled for idle/movement; Disabled for one-shot clips (death, spawn, sacrifice) |
| Animator Culling Mode | `Cull Completely` on all off-screen gameplay sprites |

Do not animate `Transform.localScale` per-frame for visual effects — use a shader property or particle system instead. Scale keyframes break sprite batching.

---

### 8.8 Tilemap Constraints

| Setting | Required value |
|---|---|
| Tilemap Renderer Mode | `Chunk` — batches entire chunk into one draw call (not `Individual` mode) |
| Grid Cell Size | `(512, 512, 0)` world units, matching PPU=1 and 512px tile size |
| Sorting Layers (4 dedicated) | `BG_Layer0` (farthest) through `BG_Layer3` (nearest background) — defined below `Default` in Sorting Layers |
| Tile Collider Type | `None` on all background tiles |
| Tile Wrap Mode | `Repeat` — required for seamless scroll |

**Parallax scrolling implementation**: Move the Tilemap GameObject's position, not UV offset. UV offset scrolling requires a custom material and breaks Tilemap chunk batching.

---

### 8.9 Export Settings and Palette Validation

**Palette validation is the single most important export gate.** Any pixel outside the approved 9-color palette is a blocking error. Export pipeline steps:

1. In Aseprite: `File > Export As` → PNG, no scaling, no color profile embedding.
2. Before export: run Aseprite's palette validation (restrict palette to the 9 approved colors). Any non-palette pixel = stop and fix.
3. Export at **1× scale** (native pixel resolution). No anti-aliasing on export.
4. Verify in a separate image viewer that no sub-pixel blending was introduced. A correct pixel-art export has exactly the colors present in the palette — no intermediate values.

**Portrait export standards**: 128×160px canvas, RGB color mode (not indexed). The ghost/echo portrait variant (for confrontation reveal context) must not contain Gold (#ffd700) or Red (#ff4040) — these semantic colors are reserved for gameplay events and must not appear on a portrait intended to read as spectral or absent.

**Failure modes to verify on every export:**
- Resampling at export (produces anti-aliased edges) — check canvas scaling is 1×
- ICC color profile mismatch (produces shifted colors in Unity) — export with no embedded profile
- Palette contamination (colors outside the 9-palette appearing at transparent boundaries) — verify with Point-filter preview in Unity immediately after import

---

## 9. Reference Direction

*This section records five specific visual references used to sharpen distinct aspects of the game's DNA. These are not aesthetic targets — REQUIEM FORMATION does not attempt to look like any of them. Each reference is a precision instrument borrowed for one specific technique. When that technique has been absorbed, the reference should recede.*

---

### Reference 1 — *Radiant Silvergun* (Treasure, 1998) — Silhouette Sovereignty Under Visual Saturation

**Domain**: Shape language / silhouette clarity

**Technique to draw from**: Radiant Silvergun saturates the screen with multicolored bullet patterns and layered explosions — yet every sprite type remains unambiguously readable throughout. The discipline is not in reducing visual density; it is in designing silhouettes so geometrically distinct that the eye classifies them before the conscious mind engages. Specifically: enemy types are wide, squat, or horizontal — none share a profile with the player ship, which is narrow and vertical. Profile-axis contrast (horizontal threat vs. vertical player) is the core readability mechanism, not color differentiation.

**What to avoid**: Do not import the color language. Radiant Silvergun uses warm primaries (red, yellow, bronze) that conflict with REQUIEM FORMATION's semantic color grammar. Do not draw from the enemy designs (mech/industrial aesthetic has no place in this world). The reference is geometric strategy only.

**Art bible application**: Reinforces Section 3's axis-contrast principle — player ship points up (agency); drone threats point down. The horizontal Weaver and rectangular Fortress are direct applications of this profile-contrast rule. When VFX artists propose effects that obscure the play field, this reference is the argument for restraint.

*Pillar anchor: 모던 레트로 / 흐름 속의 깊이*

---

### Reference 2 — *Hyper Light Drifter* (Heart Machine, 2016) — Particle-as-Memory, Not Particle-as-Spectacle

**Domain**: VFX philosophy / particle behavior

**Technique to draw from**: Hyper Light Drifter uses particles that read as physical matter, not light emissions — sparks travel on arced ballistic paths, dust hangs and disperses, hit impacts scatter like struck gravel. Each particle event feels like something *happened* in the world, not something being *displayed* to the player. Specifically: the death burst's particle spread encodes the direction the killing blow came from. Particles carry spatial information.

**What to avoid**: Do not import the warm palette or organic texture work (desaturated earth tones — rust, amber, dusty green — are incompatible with the deep-space cool palette). Do not study ground-plane lighting (a different geometric context).

**Art bible application**: Governs VFX on the sacrifice bloom and echo dissolution. When a pilot is sacrificed, the Red bloom should expand with directed ballistic geometry — not an omnidirectional soft glow. When an echo dissolves at Stage 7, its particle scatter should trail in the direction of last movement. Particles are the narrative of what happened.

*Pillar anchor: 잔상이 이야기다 / 희생은 선택이다*

---

### Reference 3 — *Nier: Automata* (PlatinumGames, 2017) — Restraint as the Color Decision

**Domain**: Color and atmospheric mood / palette discipline under emotional load

**Technique to draw from**: Nier: Automata maintains a severely restricted palette — ash-grey, blown-out white, corroded steel — for almost the entire game. This is a deliberate accumulation of color debt. When color finally appears (in story cutscenes, UI transitions), it lands with emotional force impossible in a normally-colorful game. Specifically: the game's UI leans into monochrome-with-single-accent, and the single accent (mild amber-gold of pod dialogue text) carries enormous semantic weight because nothing else competes with it.

**What to avoid**: Do not import the grey-white desaturated battlefield aesthetic (REQUIEM FORMATION's deep space is atmospheric black, not industrial grey). Do not study the character design pipeline (3D-rendered, entirely different production context).

**Art bible application**: This is the argument for the six deep-space neutral supporting colors. The three semantic colors (Gold, Red, Blue-White) only carry weight because the other 95% of the screen is restrained. Any saturation added to the environment is color debt drawn against the semantic grammar. Section 4's palette discipline is Nier's color-debt strategy applied to a shmup.

*Pillar anchor: 희생은 선택이다*

---

### Reference 4 — *Maquia: When the Promised Flower Blooms* (P.A. Works, 2018) — Cel-Shaded Character That Breathes in a Pixel World

**Domain**: Illustration character design / the dual-mode bridge

**Technique to draw from**: Maquia uses a cel-shading approach in which the key light is always cooler than the fill light — the character's face is simultaneously lit from a cool primary source and a warm secondary source. The technique creates depth from two colors (cool key, warm fill) rather than rendering complexity. Critically: the character's signature design elements (hair color, eyes, silhouette of clothing) remain identifiable in distant shots and dark scenes. The character is never lost.

**What to avoid**: Do not attempt to import animation curves or motion philosophy (portraits are static variants, not animated sequences). Do not reference Maquia's warm-pastel color design for the pilot's palette (warm flesh tones and golden light conflict with the cool palette anchor).

**Art bible application**: Directly governs Section 5.2's portrait lighting. The warm-cool split in Section 2.5 (cool key ~6500K royal blue, warm fill ~3200K violet-rose) is this reference translated into the game's palette. The rule that the pilot's four identity markers must remain readable when reduced to ~32×48 pixels is this reference's silhouette-retention principle.

*Pillar anchor: 잔상이 이야기다 (illustration as narrative threshold)*

---

### Reference 5 — *Fez* (Polytron, 2012) — Pixel Typography as a First-Class Design Object

**Domain**: Typographic and UI design

**Technique to draw from**: Fez treats its custom script and in-game typography as designed pixel objects, not functional readouts. Each character cell is a pixel-art composition — weight, counter, and stroke are all designed at the character level. The result is that the game's text has the same visual density and grid-alignment as its sprites; text does not feel imported from a different production context. Specifically: monospaced character width makes multi-line readouts spatially stable (no line-length shift as values change).

**What to avoid**: Do not reference Fez's custom undecipherable alphabet — the game requires readable Latin/Hangul text. Do not import the puzzle-game semantic context (Fez uses typography as gameplay mystery; REQUIEM FORMATION uses it as an information channel).

**Art bible application**: Justifies and clarifies Section 7.2's pixel type specification. The requirement for a 7px cap height at 1×, grid-perfect 8×8 character cell, and zero-width differentiation between `0` and `O` are applications of this discipline — every numeric glyph is a designed object with the same grid compliance as the game's sprites. When a programmer asks "can we just use any monospaced font?" — this reference explains why the answer is no.

*Pillar anchor: 모던 레트로 (retro constraint as design method, not decoration)*

---

### Reference Coverage Summary

| Reference | Domain | Core Technique | Art Bible Sections |
|---|---|---|---|
| Radiant Silvergun | Silhouette / shape legibility | Profile-axis contrast under visual saturation | 3, 3.1, 3.5 |
| Hyper Light Drifter | VFX / particle behavior | Directional-ballistic particles as spatial event records | 2.4, 5.4 |
| Nier: Automata | Color palette discipline | Color-debt accumulation — scarcity creates semantic impact | 4.1, 4.2, 4.3 |
| Maquia (2018 film) | Illustration / portrait lighting | Cool key / warm fill; silhouette retention at scale | 2.5, 5.2 |
| Fez | Typography / UI grid discipline | Type as grid-native pixel object, not font import | 7.2 |

---

*Note on Ikaruga, Hades, and Undertale*: These three titles informed the game's design foundation and are legible throughout the art bible — Ikaruga's absorption duality lives in the Chromatic Event Grammar; Hades' portrait-driven narrative integration lives in Sections 5.2 and 7.5; Undertale's sacrifice-weighted emotional pixel art lives in the Echo Degradation system and the Sacrifice Moment's white-flash treatment. They are not listed as formal references here because they are the conceptual DNA of the game itself, not instruments borrowed for specific techniques. Listing them as references risks making the game feel derivative; the five references above are the more precise tools.
