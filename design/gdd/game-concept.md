# Game Concept: REQUIEM FORMATION

*Created: 2026-04-24*
*Status: Draft*

---

## Elevator Pitch

> 적의 패턴을 흡수하고 전략적으로 희생하며 잔상 편대를 완성하는 종스크롤 슈팅.
> 쌓인 잔상들이 곧 나의 이야기가 되고, 마지막 출격에서 과거의 자신과 마주한다.
>
> *It's a narrative vertical shmup where you absorb enemy patterns and sacrifice
> yourself strategically to build a ghost formation — and your echoes ARE your story.*

---

## Core Identity

| Aspect | Detail |
| ---- | ---- |
| **Genre** | Vertical Scroll Shoot 'em up + Narrative RPG |
| **Platform** | PC (Steam / Epic) |
| **Target Audience** | Hardcore/Mid-core — mastery-driven players who want emotional depth in an action game |
| **Player Count** | Single-player |
| **Session Length** | 30~60분 (첫 클리어 기준 1~2시간) |
| **Monetization** | Premium (one-time purchase) |
| **Estimated Scope** | Medium-Large (12~14주, 솔로 프로 개발자) |
| **Comparable Titles** | Hades, Ikaruga, Undertale |

---

## Core Fantasy

나는 전장을 지배하는 파일럿이다 — 그러나 그 지배는 생존이 아니라 *선택*에서 온다.
적의 패턴을 읽고 흡수하며, 언제 희생할지를 결정하는 것이 나의 권력이다.

내가 만들어온 잔상 편대는 실패의 기록이 아니라 헌신의 증거다.
마지막 챕터에서 과거의 나 자신과 마주쳤을 때, 나는 내가 어떤 선택들을 해왔는지 편대를 통해 본다.

그리고 마지막 희생 — 돌아오지 않을 것을 알면서도 출격하는 그 결정이, 이 게임의 심장이다.

---

## Unique Hook

Like **Ikaruga**, AND ALSO 당신의 죽음이 동료가 되고, 희생이 전략이며, 편대가 곧 당신의 이야기다.

---

## Visual Identity Anchor

**방향명**: Modern Retro Specter (현대적 레트로 유령)

**핵심 규칙**: 8비트 픽셀 실루엣은 절대 흐트러지지 않는다 — 그 위에서 현대적 이펙트가 폭발한다.

**지지 원칙:**
1. **실루엣 우선**: 모든 스프라이트는 윤곽선만으로 식별 가능해야 한다. 이펙트가 실루엣을 가리면 안 된다.
   - *Design test*: 파티클을 제거했을 때도 플레이어·적·잔상의 구분이 명확한가?
2. **잔상은 빛의 궤적**: 잔상 편대는 희미한 청백색 잔광으로 표현. 편대가 커질수록 화면이 하나의 빛의 흐름이 된다.
   - *Design test*: 잔상 3개 이상일 때 화면이 시각적으로 아름다운가, 아니면 지저분한가?
3. **대비의 충격**: 8비트 그리드 정렬 배경 위에 유기적인 파티클이 터질 때의 대비가 이 게임의 미적 정체성이다.
   - *Design test*: 스크린샷 한 장으로 "레트로이면서 현대적"이라는 인상이 전달되는가?

**색상 철학**: 어두운 스페이스 배경 (#0a0a1a) 위에 원색의 픽셀 스프라이트. 잔상은 청백색 계열 (#a0c8ff), 흡수 이펙트는 황금색 (#ffd700), 희생 순간은 붉은 폭발 (#ff4040) 후 청백 잔광으로 전환.

---

## Player Experience Analysis (MDA Framework)

### Target Aesthetics (What the player FEELS)

| Aesthetic | Priority | How We Deliver It |
| ---- | ---- | ---- |
| **Sensation** (sensory pleasure) | 2 | 파티클 폭발, 스크린 쉐이크, 8비트+현대 대비 |
| **Fantasy** (make-believe) | 3 | 파일럿 정체성, 잔상 편대의 시각적 신화 |
| **Narrative** (drama) | 2 | 챕터 서사 비트, 희생 선택의 감정적 무게 |
| **Challenge** (mastery) | 1 | 패턴 흡수 타이밍, 희생 전략, 편대 최적화 |
| **Fellowship** | N/A | 싱글플레이어 |
| **Discovery** | 4 | 흡수 가능한 패턴 조합 발견, 서사의 반전 |
| **Expression** | 3 | 희생 타이밍과 빌드 조합으로 나만의 편대 구성 |
| **Submission** (flow) | 1 | 숙달될수록 생각 없이 움직이는 흐름 상태 |

### Key Dynamics (Emergent player behaviors)

- 플레이어는 자연스럽게 "이 적을 먼저 흡수할까, 아니면 저 적을?" 우선순위를 계산하기 시작한다
- 희생 타이밍을 잘못 잡은 후 "다시 해봐야겠다"는 충동이 생긴다 ("one more run")
- 잔상 편대가 커질수록 플레이어는 편대를 잃지 않으려는 투자 심리가 생긴다
- 커뮤니티에서 최적 희생 순서와 패턴 조합을 공유하기 시작한다

### Core Mechanics (Systems we build)

1. **패턴 흡수 (Pattern Absorption)** — 적을 특정 조건으로 처치하면 해당 적의 공격 패턴을 흡수. 흡수한 패턴은 잔상이 사용하는 능력이 된다.
2. **전략적 희생 (Strategic Sacrifice)** — 플레이어가 명시적 입력으로 희생을 선택. 희생 시 현재 흡수한 패턴을 가진 잔상이 생성되어 편대에 합류.
3. **잔상 편대 (Echo Formation)** — 생성된 잔상들이 플레이어와 함께 비행하며 자동 공격. 각 잔상은 생성 시점의 능력을 보유. 편대 최대 수: 7기 (상한으로 퍼포먼스 관리).
4. **챕터 서사 (Chapter Narrative)** — 스테이지 전후 짧은 연출 씬. 텍스트 최소화, 비주얼과 음악으로 감정 전달.
5. **최종 대면 (Final Echo)** — 마지막 챕터의 보스는 플레이어가 만들어온 잔상 편대 중 가장 강한 잔상 — 과거의 자신.

---

## Player Motivation Profile

### Primary Psychological Needs Served

| Need | How This Game Satisfies It | Strength |
| ---- | ---- | ---- |
| **Autonomy** | 언제 희생할지, 어떤 패턴을 흡수할지 — 플레이어의 모든 중요한 결정 | Core |
| **Competence** | 패턴을 읽고 흡수 타이밍을 완성하는 숙련의 증거가 편대로 시각화됨 | Core |
| **Relatedness** | 잔상 편대 = 내가 만들어온 역사. 챕터 서사의 인물들과의 유대 | Supporting |

### Player Type Appeal (Bartle Taxonomy)

- [x] **Achievers** — 모든 패턴 흡수, 최적 편대 구성, 클리어 타임 단축
- [x] **Explorers** — 흡수 패턴 조합 발견, 서사의 숨겨진 의미 발굴
- [ ] **Socializers** — 싱글플레이어 중심 (커뮤니티 공략 공유는 부산물)
- [x] **Killers/Competitors** — 스코어 어택, 최소 희생 클리어 도전

### Flow State Design

- **Onboarding curve**: 챕터 1은 패턴 흡수만. 챕터 2에서 희생 시스템 도입. 잔상 편대 전략은 챕터 3부터.
- **Difficulty scaling**: 흡수 가능한 패턴 복잡도 증가. 챕터 후반으로 갈수록 희생 타이밍 요구 정밀도 상승.
- **Feedback clarity**: 흡수 성공 시 황금 이펙트 + 사운드. 희생 시 붉은 폭발 → 청백 잔광 전환 연출. 즉각적이고 명확한 피드백.
- **Recovery from failure**: 챕터 체크포인트. 강제 사망 시 해당 챕터 처음부터 (잔상 편대 유지). 희생은 언제든 재시도 가능.

---

## Core Loop

### Moment-to-Moment (30 seconds)

비행하며 적의 패턴을 관찰 → 흡수 조건 충족을 위해 적을 처치 → *지금 희생해서 잔상을 만들까, 더 흡수해서 더 강한 잔상을 만들까?* → 결정과 실행

이 루프가 본질적으로 재미있는 이유: 리스크/보상 계산이 매 순간 일어난다. LoL의 순간 판단력 + FF5의 최적화 욕구가 30초 안에 압축된다.

### Short-Term (5-15 minutes)

웨이브 단위로 진행 → 흡수 가능한 패턴 조합 탐색 → 희생 타이밍 전략 실행 → 잔상 편대 쌓임 확인

"한 번만 더" 심리: 희생 타이밍을 잘못 잡으면 더 좋은 잔상을 만들 수 있었는데 하는 아쉬움이 재시도를 유발한다.

### Session-Level (30-60 minutes)

챕터 인트로 연출 → 웨이브 전투 (패턴 흡수 + 희생 전략) → 챕터 보스 (최대 패턴 흡수 기회) → 챕터 아웃트로 서사 비트 → 잔상 편대 현황 확인 → 다음 챕터로

자연스러운 정지점: 챕터 완료 후. 다음 챕터의 "무슨 이야기가 나올까?"가 재접속 동기.

### Long-Term Progression

- 챕터 언락 = 스토리 전진 (5챕터 + 엔딩)
- 흡수 패턴 도감 완성 (컬렉터 욕구)
- 최소 희생 클리어 / 스코어 어택 (숙련 증명)
- 최종 목표: 과거의 나(최강 잔상)와의 대면, 그리고 마지막 희생의 선택

### Retention Hooks

- **Curiosity**: 다음 챕터의 서사 — 누가 희생되고 무슨 이야기가 나올까
- **Investment**: 쌓아온 잔상 편대를 잃지 않으려는 심리
- **Mastery**: 더 나은 희생 타이밍, 더 효율적인 패턴 조합을 향한 도전
- **Curiosity**: 파이널 보스가 "과거의 나"라는 사실 — 어떤 모습일지

---

## Game Pillars

### Pillar 1: 희생은 선택이다 (Sacrifice is Agency)
모든 죽음은 의미가 있어야 한다. 실패로서의 죽음도, 전략으로서의 희생도 플레이어의 결정이다.

*Design test*: 적이 너무 강해서 어쩔 수 없이 죽는 상황 vs 내가 선택해서 희생하는 상황 — 이 필라는 후자를 우선한다. 강제 사망을 최소화하고, 희생은 명시적 입력(버튼)으로 분리 설계한다.

### Pillar 2: 잔상이 이야기다 (Echoes Are Narrative)
플레이어의 행동 기록이 그 자체로 서사가 된다. 텍스트 없이도 편대를 보면 여정이 보여야 한다.

*Design test*: 시각 효과를 추가할 때 화려함 vs 가독성이 충돌하면 → 잔상의 개성과 식별성이 우선. 잔상 7기를 동시에 표시해도 각각의 "성격"이 보여야 한다.

### Pillar 3: 흐름 속의 깊이 (Depth Through Flow)
복잡한 시스템을 배우는 과정이 스트레스가 아닌 발견의 기쁨이어야 한다. 파고들수록 더 보이지만, 처음부터 압도하지 않는다.

*Design test*: 능력 흡수 UI/정보량 — 단순함 vs 디테일이 충돌하면 → 처음엔 보이지 않아도 작동하는 레이어를 우선. 시스템을 몰라도 클리어 가능하되, 알면 훨씬 재미있어야 한다.

### Pillar 4: 모던 레트로 감성 (Modern Retro)
8비트의 문법으로 현대의 감정을 전달한다. 픽셀 스프라이트 위에 파티클이 터지는 그 순간의 대비.

*Design test*: 그래픽 이펙트 추가 시 더 화려하게 vs 레트로 감성 유지 → 레트로 실루엣이 살아있으면 현대 이펙트를 추가한다. 실루엣이 흐트러지면 이펙트를 줄인다.

### Anti-Pillars (What This Game Is NOT)

- **NOT 탄막 지옥 (Bullet Hell)**: 회피 자체가 목적이 되는 순간 흐름이 깨진다. 패턴 피하기 < 패턴 흡수하기. 탄막 밀도는 스트레스가 아닌 리듬감을 위해 존재한다.
- **NOT 랜덤 로그라이트**: 희생의 의미는 축적에서 나온다. 매 런마다 모든 것이 리셋되면 잔상 편대가 감정적 무게를 잃는다. 챕터 진행은 누적된다.
- **NOT 긴 그라인드**: 1~3개월 스코프, 밀도 높은 단편. 10시간짜리 컨텐츠보다 2시간의 완전한 감정적 호를 우선한다.

---

## Inspiration and References

| Reference | What We Take From It | What We Do Differently | Why It Matters |
| ---- | ---- | ---- | ---- |
| **Hades** | 죽음이 이야기의 일부가 되는 구조, 반복이 서사를 심화 | 죽음 = 이야기 심화가 아니라 죽음 = 동료 생성 | 장르 예상을 뒤엎는 서사 접목의 선례 |
| **Ikaruga** | 패턴 전환/흡수 메카닉, 집중된 디자인 | 흑백 전환 < 다양한 패턴 흡수 + 잔상 생성 | 흡수 메카닉의 게임플레이 가능성 검증 |
| **Undertale** | 장르 예상을 뒤엎는 감정적 서사, 소규모 팀 강한 임팩트 | 텍스트 서사 < 비주얼+음악 기반 감정 전달 | 작은 게임도 깊은 감동을 줄 수 있다는 증거 |

**Non-game inspirations**:
- **Final Fantasy V (가라프의 희생)**: 힘이 있어도 이기지 못하고 사랑으로 희생하는 이야기 구조 — 마지막 챕터의 감정적 목표
- **Prince of Persia: Warrior Within (과거와의 조우)**: 서사와 게임플레이가 하나로 합쳐지는 반전 — 파이널 보스 "과거의 나"의 원형

---

## Target Player Profile

| Attribute | Detail |
| ---- | ---- |
| **Age range** | 25~40세 |
| **Gaming experience** | Hardcore / Mid-core |
| **Time availability** | 평일 30~60분, 주말 2~3시간 세션 가능 |
| **Platform preference** | PC |
| **Current games they play** | Hades, Hollow Knight, Elden Ring, Ikaruga |
| **What they're looking for** | 숙달의 기쁨 + 감정적 울림 — 슈팅 장르에서 기대하지 않았던 이야기 |
| **What would turn them away** | 과도한 랜덤성, 반복 그라인드, 얕은 시스템 |

---

## Technical Considerations

| Consideration | Assessment |
| ---- | ---- |
| **Recommended Engine** | TBD — `/setup-engine` 실행 후 결정 (PC Steam 타겟, 2D 픽셀 아트) |
| **Key Technical Challenges** | 다수 잔상 동시 재생 시 CPU 부하 관리 (상한 7기 + LOD 전략 필요) |
| **Art Style** | 2D Pixel (8비트 스프라이트) + Modern Particle/Dynamic Lighting |
| **Art Pipeline Complexity** | Medium — 스프라이트는 가볍지만 이펙트 레이어가 별도 작업량 생성 |
| **Audio Needs** | Music-heavy — 레트로 칩튠 + 오케스트라 하이브리드. 희생 순간의 사운드 디자인 중요 |
| **Networking** | None |
| **Content Volume** | 챕터 5개, 보스 5개, 흡수 패턴 12~18종, 플레이타임 1~2시간 |
| **Procedural Systems** | 없음 — 핸드크래프트 챕터 구성 |

---

## Risks and Open Questions

### Design Risks
- 전략적 희생 vs 실수에 의한 죽음의 구분이 플레이어에게 직관적으로 전달되지 않을 수 있다
- 잔상 편대가 화면을 과도하게 채워 코어 슈팅 게임플레이의 가독성을 해칠 수 있다

### Technical Risks
- 잔상 7기 동시 AI 재생 시 프레임 드롭 — MVP 단계에서 프로토타입 검증 필수
- 희생 타이밍 입력이 일반 조작과 충돌할 경우 오입력 발생 가능

### Market Risks
- 종스크롤 슈팅 장르의 코어 팬 시장이 제한적
- "감정적 슈팅"이라는 포지셔닝이 장르 팬과 스토리 팬 모두에게 어중간하게 느껴질 수 있다

### Scope Risks
- 챕터 서사의 품질이 기대에 못 미칠 경우 차별점이 사라짐 — 작가/연출 리소스 필요
- 패턴 흡수 시스템 밸런스 조정에 예상보다 많은 이터레이션이 필요할 수 있다

### Open Questions
- 잔상의 챕터 간 지속 여부: 챕터가 끝나도 잔상이 유지되는가, 아니면 챕터마다 리셋되는가? → MVP 플레이테스트로 검증
- 희생 입력 UX: 전용 버튼인가, 특정 조건 충족 시 활성화되는 맥락적 액션인가? → 프로토타입에서 A/B 테스트 필요

---

## MVP Definition

**Core hypothesis**: 플레이어는 "전략적 희생 → 잔상 생성"의 루프를 경험한 후 30분 이상 플레이를 지속하려는 동기를 느낀다.

**Required for MVP**:
1. 기본 이동/발사 시스템 + 1종의 흡수 가능한 적 패턴
2. 희생 입력 → 잔상 1기 생성 → 잔상 자동 공격 시스템
3. 챕터 1~2 (웨이브 + 보스 2개) + 최소한의 서사 연출 1개

**Explicitly NOT in MVP**:
- 챕터 3~5 서사 (검증 후 추가)
- 다양한 패턴 조합/시너지 시스템
- 풀 사운드트랙 (프로토타입은 임시 음악)
- 폴리시 이펙트 (기능 검증 우선)

### Scope Tiers

| Tier | Content | Features | Timeline |
| ---- | ---- | ---- | ---- |
| **MVP** | 챕터 1~2, 보스 2개, 흡수 패턴 3종 | 이동/발사, 패턴 흡수, 잔상 1기, 기본 서사 연출 | 3~4주 |
| **Vertical Slice** | 챕터 1~3, 보스 3개, 흡수 패턴 8종 | 전체 잔상 편대(최대 7기), 패턴 조합, 챕터 서사 비트 | 6~7주 |
| **Alpha** | 전체 5챕터 플레이스홀더, 패턴 12종 | 모든 피처 (러프), 파이널 보스 프로토타입 | 10주 |
| **Full Vision** | 완성된 5챕터 + 엔딩 씬, 패턴 18종 | 모든 피처 폴리시, 밸런스, 칩튠 사운드트랙 | 12~14주 |

---

## Next Steps

- [ ] Run `/setup-engine` — 엔진 선택 및 버전 고정 (PC Steam, 2D 픽셀 아트 기준)
- [ ] Run `/art-bible` — Visual Identity Anchor를 바탕으로 아트 바이블 작성 (GDD 작성 전 완료 필수)
- [ ] Run `/design-review design/gdd/game-concept.md` — 컨셉 문서 완성도 검증
- [ ] Run `/map-systems` — 컨셉을 개별 시스템으로 분해 (의존성 매핑)
- [ ] Run `/design-system` — 각 시스템별 GDD 작성 (패턴 흡수, 잔상 편대, 챕터 서사 우선)
- [ ] Run `/create-architecture` — 마스터 아키텍처 블루프린트 생성
- [ ] Run `/prototype pattern-absorption` — MVP 코어 루프 프로토타입으로 핵심 가설 검증
- [ ] Run `/playtest-report` — 프로토타입 플레이테스트 후 문서화
- [ ] Run `/gate-check` — 프리프로덕션 진입 전 레디니스 검증
