# Context Reframing

> "엘리베이터가 느리다"는 불만에 거울을 설치한 것처럼, 진짜 문제를 찾아내는 Claude Code 스킬 패밀리

**Voice→Need→Context** 3단계 리프레이밍으로 표면적 요청을 깊은 맥락 이해로 변환합니다.
Surface Risk가 20% 이하로 내려갈 때까지 솔루션 제안을 차단하는 Hard Gate를 통해, "잘못된 문제를 잘 푸는 것"을 방지합니다.

## Install

```bash
claude plugin install Q00/context-reframing
```

Or register the marketplace and install:

```bash
claude marketplace register Q00/context-reframing
claude plugin install context-reframing
```

## Skills

| Skill | Trigger | What It Does |
|-------|---------|-------------|
| `/context-reframing` | `reframe`, `진짜 문제가 뭐야` | Universal reframing — any domain |
| `/product-reframing` | `이 기능 진짜 필요해?`, feature requests | Product decisions — Customer Focused vs Centric |
| `/debug-reframing` | error messages, recurring bugs | Debugging — Symptom→Cause→Design Flaw |
| `/prompt-reframing` | `리팩토링해줘`, vague AI prompts | AI prompts — Passive mode auto-detection |

## How It Works

### The Core Idea

Most requests are **Voice-level** — what people literally say. But the real problem lives at **Context-level** — the situation behind the request.

```
Voice:   "검색 필터 10개 추가해주세요"
Need:    유저가 원하는 상품을 못 찾고 있다
Context: 검색 알고리즘 자체가 부정확해서 필터로 보완하려는 것
```

### Context Depth Score (CDS)

Each reframing session scores 4 dimensions:

| Dimension | Description |
|-----------|-------------|
| Voice Fidelity | Did we capture the exact words? |
| Need Identification | Did we find the immediate goal? |
| Context Discovery | Did we uncover the real situation? |
| Reframe Validity | Does the reframe actually explain things better? |

**Surface Risk** = `1 - Σ(depth × weight)` — must be ≤ 20% before any solution is proposed.

### Challenge Modes

At deeper rounds, the skill shifts perspective:

- **Mirror Mode** (R3+): "What if the problem isn't what you think?" — inspired by the elevator mirror story
- **Levitt Mode** (R5+): "What does the data actually say?" — inspired by Freakonomics-style thinking
- **Inversion Mode** (R7+): "What if we remove the thing instead of fixing it?" — inspired by adhesive hook innovation

## Skill Family Architecture

```
context-reframing/          ← Core (universal)
├── SKILL.md                   CDS engine, phases, challenge modes
└── references/
    ├── scoring-engine.md      5-point rubric, weight profiles
    ├── question-patterns.md   Phase 1-4 targeting strategy
    ├── challenge-modes.md     Mirror/Levitt/Inversion definitions
    └── examples.md            4 worked examples

product-reframing/          ← Product domain
├── SKILL.md                   Context weight 40%, CF vs CC output
└── references/
    └── product-patterns.md    B2C/B2B/Platform patterns

debug-reframing/            ← Debug domain
├── SKILL.md                   Reframe weight 30%, auto-exploration
└── references/
    └── debug-patterns.md      Symptom→Cause→Design Flaw chains

prompt-reframing/           ← AI prompt domain
├── SKILL.md                   Balanced 25%, passive mode
└── references/
    └── prompt-patterns.md     Ambiguity detection heuristics
```

## Examples

### Product Reframing

```
User: 유저들이 검색 필터를 더 추가해달라고 해요

Voice:   "검색 필터 추가 요청"
Need:    유저가 원하는 것을 찾지 못하고 있음
Context: 검색 정확도가 낮아 필터로 보완하려는 것

┌─ Customer Focused ──────────────────┐
│ 필터 10개 추가                       │
│ → 요청한 그대로 구현                  │
│ Risk: 근본 원인 미해결               │
├─ Customer Centric ──────────────────┤
│ 검색 알고리즘 개선 + 핵심 필터 3개    │
│ → 진짜 필요를 해결                   │
│ Risk: 개발 비용 증가          ← REC │
└─────────────────────────────────────┘
```

### Debug Reframing

```
User: 로그인이 세 번째 재발이에요

+-- Level 1 Fix (Symptom) ----------------+
| try/catch에 retry 추가                    |
| Recurrence risk: HIGH                    |
+-- Level 2 Fix (Cause) ------------------+
| refreshToken에 에러 핸들링 추가            |
| Recurrence risk: MEDIUM                  |
+-- Level 3 Fix (Design) -----------------+
| Offline-tolerant auth architecture       |
| Recurrence risk: LOW           ← REC   |
+-----------------------------------------+
```

## Passive Mode (Prompt Reframing)

Automatically detects ambiguous AI prompts and asks one clarifying question before proceeding.

```bash
# Activate
/prompt-reframing --passive

# Deactivate
/prompt-reframing --passive off
```

When active, vague requests like "리팩토링해줘" trigger an inline confirmation:

```
I understood your context as:
  Said:      "리팩토링해줘"
  Intent:    코드 가독성 향상
  Situation: 새 팀원 온보딩이 느려서 코드를 이해하기 쉽게 만들려는 것

  Is this right?
  [Yes] [No, actually...] [Partially]
```

## Credits

- **Voice→Need→Context** framework: 박재오 (LinkedIn post)
- Inspired by [Superpowers](https://github.com/obra/superpowers) and [Ouroboros](https://github.com/Q00/ouroboros)

## License

MIT
