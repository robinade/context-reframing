# Context Reframing

**Stop solving the wrong problem well. Start finding the right problem to solve.**

**잘못된 문제를 잘 푸는 것을 멈추고, 진짜 문제를 찾아내세요.**

A Claude Code skill family that transforms surface-level requests into deep contextual understanding using the **Voice→Need→Context** framework. It blocks all solution proposals until the real problem is understood — mathematically verified with a Surface Risk score.

Claude Code 스킬 패밀리로, **Voice→Need→Context** 프레임워크를 사용하여 표면적 요청을 깊은 맥락 이해로 전환합니다. Surface Risk 점수로 수학적으로 검증될 때까지 모든 솔루션 제안을 차단합니다.

---

## The Origin Story / 탄생 배경

This skill was inspired by a LinkedIn post from **박재오** (Bucketplace Commerce Division) that perfectly captures why we built this:

이 스킬은 **박재오**님(버킷플레이스 커머스부문)의 LinkedIn 글에서 영감을 받아 만들었습니다:

> **"고객의 말을 '너무' 잘 들어서 실패하는 이유"**
>
> *"Why listening 'too well' to customers causes failure"*

### The Drill Story / 드릴 이야기

Theodore Levitt famously said: *"Customers don't want a quarter-inch drill. They want a quarter-inch hole."*

But go one level deeper — the customer doesn't actually want a *hole*. They want to **hang a picture frame on the wall**. That's the Context.

시어도어 레빗은 이렇게 말했습니다: *"고객은 1/4인치 드릴을 사고 싶은 것이 아니다. 그들은 1/4인치 구멍을 뚫고 싶은 것이다."*

하지만 한 단계 더 들어가면, 사실 고객은 구멍을 뚫고 싶은 게 아니라 **'액자를 벽에 걸고 싶은 것(Context)'**일 수 있습니다.

- **Customer Focused** approach: Build a better, cheaper drill → 더 강력하고 저렴한 드릴을 만든다
- **Customer Centric** approach: Suggest adhesive hooks (no drill needed!) → 초강력 접착 후크를 제안한다 (드릴 불필요!)

The customer asked for a drill because they didn't know hooks existed. The real problem was never about the drill — it was about *hanging*.

고객은 후크의 존재를 모르기에 드릴을 달라고 했을 뿐, 진짜 문제는 '구멍'이 아니라 **'거치'**였던 셈이죠.

### The Elevator Mirror / 엘리베이터 거울

Tenants complained: *"The elevator is too slow."*

세입자들이 불만을 쏟아냅니다: *"엘리베이터 속도가 너무 느리다."*

| | Customer Focused | Customer Centric |
|---|---|---|
| **Solution** | Replace the motor ($$$) / 거액을 들여 모터를 교체 | Install a mirror ($) / 거울을 설치 |
| **Addresses** | Voice: "it's slow" / "느리다" | Context: "waiting is boring" / "기다리는 시간이 지루하다" |
| **Result** | Faster elevator / 더 빠른 엘리베이터 | Complaints disappeared / 불만이 사라짐 |

The real complaint was never about physical speed — it was about **the boredom of waiting**. Installing a mirror made people check their appearance, and the complaints vanished.

진짜 불만은 '물리적 속도'가 아니라 **'기다리는 시간의 지루함'**이었습니다. 거울을 설치하자 사람들은 옷매무새를 다듬느라 집중했고, 불만은 사라졌습니다.

**Solution A** focused on the customer's Voice and spent heavily. **Solution B** understood the customer's Context and solved the problem at a fraction of the cost.

**해결책 A**는 고객의 '말(Voice)'에 집중해 비용을 쏟았지만, **해결책 B**는 고객의 '상황(Context)'을 통찰해 훨씬 적은 비용으로 문제를 종식시켰습니다.

### The Search Filter Trap / 검색 필터의 함정

In platform businesses, this trap appears daily:

플랫폼 비즈니스에서도 매일 이 갈림길에 섭니다:

> Users say: *"Add more search filters please"*
>
> 유저들이 말합니다: *"검색 필터를 더 늘려주세요"*

Adding 50 filters just increases fatigue. But if the Context is *"I can't find what I want"*, the real answer might be **better curation** or **shorter navigation paths** — not more filters.

필터 옵션을 50개로 늘리는 건 오히려 피로도만 높이죠. 하지만 맥락이 "원하는 상품을 못 찾아서 헤매는 중"이라면, 진짜 답은 필터가 아니라 **'더 정교한 추천(Curation)'**이나 **'탐색 동선 단축'**일 수 있습니다.

### The Takeaway / 핵심

> *"Fulfilling requests is 'kindness'. Solving hidden context is 'real improvement'. We should be problem-solvers, not just kind bystanders."*
>
> *"요구사항을 들어주는 건 '친절'이지만, 숨겨진 맥락을 해결해 주는 건 '진짜 개선'이 됩니다. 우리는 친절한 방관자가 아니라, 문제를 끝내는 해결사가 되어야 하니까요."*
>
> — 박재오

**This skill brings that philosophy into Claude Code.** Before your AI assistant proposes any solution, it first digs through Voice→Need→Context to make sure it's solving the *right* problem.

**이 스킬은 그 철학을 Claude Code에 가져옵니다.** AI 어시스턴트가 솔루션을 제안하기 전에, 먼저 Voice→Need→Context를 파고들어 *올바른* 문제를 풀고 있는지 확인합니다.

---

## Install / 설치

```bash
claude plugin install robinade/context-reframing
```

Or register the marketplace and install:

또는 마켓플레이스에 등록 후 설치:

```bash
claude marketplace register robinade/context-reframing
claude plugin install context-reframing
```

---

## The Voice→Need→Context Framework

Every request has three layers. Most people only communicate the first one.

모든 요청에는 세 가지 레이어가 있습니다. 대부분의 사람들은 첫 번째만 전달합니다.

```
┌─────────────────────────────────────────────────┐
│  Voice   What they literally said               │  ← Surface
│          그들이 문자 그대로 말한 것                  │
├─────────────────────────────────────────────────┤
│  Need    The immediate goal behind the words    │  ← Deeper
│          말 뒤에 숨겨진 즉각적인 목표                │
├─────────────────────────────────────────────────┤
│  Context The real situation driving everything   │  ← Deepest
│          모든 것을 움직이는 진짜 상황                │
└─────────────────────────────────────────────────┘
```

### Real-World Examples / 실전 예시

**Example 1: Product Feature Request / 제품 기능 요청**

```
Voice:   "Add 10 more search filters"
         "검색 필터 10개 추가해주세요"

Need:    Users can't find what they're looking for
         유저가 원하는 것을 찾지 못하고 있다

Context: The search algorithm itself is inaccurate,
         so users try to compensate with filters
         검색 알고리즘 자체가 부정확해서 필터로 보완하려는 것
```

**Example 2: Recurring Bug / 반복되는 버그**

```
Voice:   "Login keeps failing — third time this quarter"
         "로그인이 자꾸 실패해요 — 이번 분기에 세 번째"

Need:    Session tokens are expiring unexpectedly
         세션 토큰이 예기치 않게 만료됨

Context: Token refresh logic silently swallows network errors,
         a design flaw that no amount of retry logic will fix
         토큰 갱신 로직이 네트워크 에러를 무시하는 설계 결함
```

**Example 3: Vague AI Prompt / 모호한 AI 프롬프트**

```
Voice:   "Refactor this code"
         "이 코드 리팩토링해줘"

Need:    Could mean: readability? performance? extensibility?
         가독성? 성능? 확장성? — 무엇이든 될 수 있음

Context: New team member is joining next week and
         can't understand the current codebase
         다음 주에 새 팀원이 합류하는데 현재 코드를 이해 못 하는 상황
```

Without context, you might optimize for performance when the real need is readability for onboarding.

맥락 없이는 실제 필요가 온보딩을 위한 가독성인데 성능 최적화를 할 수도 있습니다.

---

## The 4 Skills / 4개 스킬

This plugin includes 4 domain-specific reframing skills, each with tuned weights and specialized outputs:

이 플러그인에는 4개의 도메인별 리프레이밍 스킬이 포함되어 있으며, 각각 조정된 가중치와 특화된 출력을 제공합니다:

### 1. `/context-reframing` — Universal / 범용

> For any problem in any domain. The core engine.
>
> 모든 도메인의 모든 문제에 적용. 코어 엔진.

- **Weights**: Voice 20% · Need 25% · Context 35% · Reframe 20%
- **Output**: Full reframing report saved to `.omc/reframes/`
- **Trigger**: `reframe`, `what's the real problem`, `진짜 문제가 뭐야`

### 2. `/product-reframing` — Product Decisions / 제품 의사결정

> When someone requests a feature, ask: are we being Customer Focused or Customer Centric?
>
> 누군가 기능을 요청할 때: 우리가 Customer Focused인가, Customer Centric인가?

- **Weights**: Voice 15% · Need 25% · **Context 40%** · Reframe 20%
- **Output**: **Customer Focused vs Customer Centric** comparison table
- **Trigger**: feature requests, `이 기능 진짜 필요해?`, `should we build this`
- **Best for**: PMs, product teams, founders evaluating user requests

### 3. `/debug-reframing` — Root Cause Debugging / 근본 원인 디버깅

> Stop patching symptoms. Find the design flaw.
>
> 증상 패치를 멈추고. 설계 결함을 찾으세요.

- **Weights**: Voice 20% · Need 20% · Context 30% · **Reframe 30%**
- **Output**: **Fix Depth Comparison** (L1 Symptom → L2 Cause → L3 Design)
- **Trigger**: recurring bugs, stack traces, `this broke again`, `또 재발했어`
- **Unique**: Auto-explores your codebase before asking questions
- **Best for**: Engineers debugging persistent issues, tech leads reviewing fixes

### 4. `/prompt-reframing` — AI Prompt Clarity / AI 프롬프트 명확화

> Catch ambiguous requests before your AI builds the wrong thing.
>
> AI가 잘못된 것을 만들기 전에 모호한 요청을 포착하세요.

- **Weights**: All dimensions **balanced at 25%**
- **Output**: Inline confirmation (no file saved)
- **Trigger**: vague requests like `리팩토링해줘`, `improve this`, `고쳐줘`
- **Unique**: **Passive Mode** — auto-detects ambiguity without explicit invocation
- **Best for**: Anyone using AI coding assistants daily

---

## How It Works / 작동 방식

### The Hard Gate / 하드 게이트

**No solution is proposed until Surface Risk ≤ 20%.**

**Surface Risk가 20% 이하가 될 때까지 솔루션을 제안하지 않습니다.**

This is enforced mathematically:

```
Surface Risk = 1 - Σ(depth_i × weight_i)
```

Each dimension is scored 0.0–1.0 on a 5-point rubric. The skill loops through targeted questions, scoring after each round, and only proceeds when the math says the problem is understood deeply enough.

각 차원은 5점 루브릭으로 0.0–1.0 점수를 매깁니다. 스킬은 타겟팅된 질문을 반복하며, 매 라운드마다 점수를 매기고, 수학적으로 문제가 충분히 깊게 이해되었다고 판단될 때만 진행합니다.

### Context Depth Score (CDS)

| Dimension | What It Measures | Description |
|-----------|-----------------|-------------|
| **Voice Fidelity** | Did we capture the exact words? | 정확한 말을 포착했는가? |
| **Need Identification** | Did we find the immediate goal? | 즉각적인 목표를 찾았는가? |
| **Context Discovery** | Did we uncover the real situation? | 진짜 상황을 발견했는가? |
| **Reframe Validity** | Does the reframe explain things better? | 리프레임이 더 잘 설명하는가? |

### Challenge Modes / 챌린지 모드

As the conversation deepens, the skill shifts perspective to prevent tunneling into the wrong direction:

대화가 깊어질수록, 스킬은 잘못된 방향으로의 터널링을 방지하기 위해 관점을 전환합니다:

| Mode | Activates | Inspired By | Question Style |
|------|-----------|-------------|---------------|
| **Mirror** | Round 3+ | The elevator mirror story / 엘리베이터 거울 | *"What if this problem is actually about something completely different?"* |
| **Levitt** | Round 5+ | Theodore Levitt's drill story / 레빗의 드릴 이야기 | *"What does the user actually want to achieve? Not the tool — the outcome."* |
| **Inversion** | Round 7+ | The adhesive hook / 접착 후크 | *"What if we removed this component entirely? Would the problem disappear?"* |

---

## Use Cases & Best Practices / 사용 사례 & 베스트 프랙티스

### When to Use / 언제 사용하나요

| Scenario | Skill | Why |
|----------|-------|-----|
| PM gets a feature request from users | `/product-reframing` | Distinguish Customer Focused vs Centric before committing dev time |
| Bug has been "fixed" 3 times but keeps returning | `/debug-reframing` | Stop patching symptoms, find the design flaw |
| Team member says "refactor this" with no other context | `/prompt-reframing` | Clarify intent before spending hours on the wrong refactor |
| Stakeholder says "we need a dashboard" | `/context-reframing` | Uncover what decision the dashboard should support |
| User says "make it faster" | `/context-reframing` | Is it actual latency? Perceived slowness? Missing loading states? |
| CEO says "add AI to the product" | `/product-reframing` | What user problem would AI solve? Or is this a solution looking for a problem? |

### When NOT to Use / 언제 사용하지 않나요

- The request is specific and clear: *"Fix the typo in line 42 of auth.ts"* → Just do it
- There's an emergency and speed matters more than depth → Fix first, reframe later
- The user explicitly says *"just do it"* or *"skip the questions"* → Respect their intent

### Recommended Workflows / 추천 워크플로우

**For Product Teams / 제품팀:**
```
User feedback → /product-reframing → CF vs CC comparison → Informed decision
```

**For Engineering Teams / 엔지니어링팀:**
```
Recurring bug → /debug-reframing → Fix Depth Comparison → L3 architecture fix
```

**For Daily AI Usage / 일상 AI 사용:**
```
/prompt-reframing --passive   (activate once, works forever)
Vague prompt → auto-clarification → better AI output
```

**For Strategic Decisions / 전략적 결정:**
```
Stakeholder request → /context-reframing → Full report → Aligned execution
```

---

## Output Examples / 출력 예시

### Product Reframing Output / 제품 리프레이밍 출력

```
┌─ Customer Focused ──────────────────────────────┐
│ Add 10 search filters                            │
│ 필터 10개 추가                                     │
│ → Build exactly what was requested               │
│ → 요청한 그대로 구현                                │
│ Risk: Root cause unaddressed / 근본 원인 미해결    │
├─ Customer Centric ──────────────────────────────┤
│ Improve search algorithm + add 3 key filters     │
│ 검색 알고리즘 개선 + 핵심 필터 3개                   │
│ → Solve the real need / 진짜 필요를 해결           │
│ Risk: Higher dev cost / 개발 비용 증가     ← REC  │
└─────────────────────────────────────────────────┘
```

### Debug Reframing Output / 디버그 리프레이밍 출력

```
FIX DEPTH COMPARISON
========================================

+-- Level 1 Fix (Symptom) ----------------+
| Add retry logic to try/catch             |
| try/catch에 retry 추가                    |
| Recurrence risk: HIGH                    |
| Effort: Low                              |
+-- Level 2 Fix (Cause) ------------------+
| Add error handling to refreshToken       |
| refreshToken에 에러 핸들링 추가            |
| Recurrence risk: MEDIUM                  |
| Effort: Medium                           |
+-- Level 3 Fix (Design) -----------------+
| Offline-tolerant auth architecture       |
| 오프라인 내성 인증 아키텍처                  |
| Recurrence risk: LOW                     |
| Effort: High                   ← REC    |
+-----------------------------------------+
```

### Prompt Reframing Output (Passive Mode) / 프롬프트 리프레이밍 출력 (패시브 모드)

```
I understood your context as:
  Said:      "Refactor this code" / "리팩토링해줘"
  Intent:    Improve code readability / 코드 가독성 향상
  Situation: New team member onboarding next week /
             새 팀원 온보딩이 느려서 코드를 이해하기 쉽게 만들려는 것

  Is this right?
  [Yes] [No, actually...] [Partially]
```

---

## Architecture / 아키텍처

```
context-reframing/
├── .claude-plugin/
│   ├── plugin.json              Plugin manifest / 플러그인 매니페스트
│   └── marketplace.json         Marketplace registry / 마켓플레이스 등록
├── skills/
│   ├── context-reframing/       Core universal skill / 코어 범용 스킬
│   │   ├── SKILL.md                CDS engine, 5 phases, challenge modes
│   │   └── references/
│   │       ├── scoring-engine.md   5-point rubric, weight profiles
│   │       ├── question-patterns.md Phase 1-4 targeting strategy
│   │       ├── challenge-modes.md  Mirror/Levitt/Inversion definitions
│   │       └── examples.md        4 worked examples
│   ├── product-reframing/       Product domain / 제품 도메인
│   │   ├── SKILL.md                Context weight 40%, CF vs CC output
│   │   └── references/
│   │       └── product-patterns.md B2C/B2B/Platform patterns
│   ├── debug-reframing/         Debug domain / 디버그 도메인
│   │   ├── SKILL.md                Reframe weight 30%, auto-exploration
│   │   └── references/
│   │       └── debug-patterns.md   Symptom→Cause→Design Flaw chains
│   └── prompt-reframing/        AI prompt domain / AI 프롬프트 도메인
│       ├── SKILL.md                Balanced 25%, passive mode
│       └── references/
│           └── prompt-patterns.md  Ambiguity detection heuristics
├── README.md
└── LICENSE (MIT)
```

### Design Principles / 설계 원칙

- **Progressive Disclosure**: SKILL.md stays under 500 lines. Detailed rubrics, patterns, and examples live in `references/` and are loaded only when needed.
- **Domain-Specific Weights**: Each skill tunes the CDS formula for its domain. Product emphasizes Context (40%). Debug emphasizes Reframe validity (30%).
- **Hard Gate, Not Soft Suggestion**: The Surface Risk threshold is enforced, not advisory. This prevents the natural tendency to jump to solutions.
- **Challenge Modes as Perspective Shifts**: Mirror, Levitt, and Inversion modes aren't random — they activate at specific depth thresholds to prevent cognitive tunneling.

---

## FAQ

**Q: How is this different from just asking "why?" repeatedly?**

It's structured and scored. Asking "why" 5 times (the Toyota method) is useful but unguided. Context Reframing targets the weakest dimension with each question, scores progress mathematically, and shifts perspective through challenge modes. It also blocks solutions until the score proves understanding.

단순히 "왜?"를 반복하는 것과 다릅니다. 구조화되고 점수가 매겨집니다. 매 질문마다 가장 약한 차원을 타겟팅하고, 수학적으로 진행도를 측정하며, 챌린지 모드를 통해 관점을 전환합니다.

**Q: What if I already know the context?**

Skip to execution. These skills detect when requests are specific enough (file paths, function names, concrete criteria) and stay silent. They only activate when ambiguity is detected.

이미 맥락을 알고 있다면 바로 실행하세요. 이 스킬들은 요청이 충분히 구체적일 때 (파일 경로, 함수명, 구체적 기준) 조용히 있습니다. 모호성이 감지될 때만 활성화됩니다.

**Q: Can I use this outside Claude Code?**

The framework (Voice→Need→Context) is universal — you can apply it in any conversation, meeting, or product discussion. The Claude Code skills just automate and enforce it.

프레임워크(Voice→Need→Context)는 보편적입니다 — 어떤 대화, 회의, 제품 토론에서든 적용할 수 있습니다. Claude Code 스킬은 이를 자동화하고 강제할 뿐입니다.

---

## Credits / 크레딧

- **Voice→Need→Context framework**: Inspired by [박재오](https://www.linkedin.com/in/jaeoh-park/)'s LinkedIn post on Customer Focused vs Customer Centric
- **Elevator Mirror Problem**: Classic problem-reframing case study
- **Theodore Levitt**: "People don't want a quarter-inch drill" (Harvard Business School)
- **Plugin architecture**: Inspired by [Superpowers](https://github.com/obra/superpowers) and [Ouroboros](https://github.com/Q00/ouroboros)

## License / 라이선스

MIT — use it, fork it, extend it. Build your own domain-specific reframing skills.

MIT — 사용하고, 포크하고, 확장하세요. 자신만의 도메인별 리프레이밍 스킬을 만드세요.
