---
name: product-reframing
description: "Reframes product feature requests and user feedback from Voice (what users said) to Context (their real life situation) using product-specific weights. Prevents building exactly what users asked for while missing what they actually needed. Use when analyzing feature requests, user feedback, customer complaints, or product requirements. Triggers: '/product-reframing', user feedback quotes, '유저가 ~라고 했는데', feature request analysis, customer voice, or NPS/CSAT verbatims."
---

# Product Reframing

Extends [context-reframing](../context-reframing/SKILL.md) for product/planning decisions.

> "고객이 원하는 걸 만들었는데 왜 안 쓰지?" — This skill prevents that.

## How It Differs From Core

| Aspect | Core (Universal) | Product |
|--------|-----------------|---------|
| Context weight | 35% | **40%** |
| Voice = | "What they said" | Feature Request |
| Need = | Immediate goal | User Goal |
| Context = | Real situation | Life Context |
| Unique output | Solutions by level | **Customer Focused vs Centric comparison** |

## Product-Specific Weights

| Dimension | Weight | Why |
|-----------|--------|-----|
| Voice Fidelity | 15% | Behavioral patterns matter more than exact words |
| Need Identification | 25% | User goals bridge Voice to Context |
| **Context Discovery** | **40%** | Product decisions live or die by life context |
| Reframe Validity | 20% | Reframe must be actionable for product teams |

## Product Question Patterns

### Phase 1: Capture the Feature Request
- "유저/이해관계자가 정확히 뭐라고 했나요? 어떤 단어를 사용했나요?"
- "이 피드백이 몇 건이나 들어왔나요? 패턴이 있나요?"
- "어떤 채널에서 들어왔나요? (CS, 리뷰, 인터뷰, 내부)"

### Phase 2: Excavate User Goal
- "이 기능 없이 유저가 지금 어떻게 하고 있나요?"
- "이 기능이 생기면 유저의 행동이 어떻게 바뀌나요?"
- "경쟁사에서 이걸 어떻게 해결하고 있나요?"
- "이 기능의 성공을 어떤 지표로 측정할 수 있나요?"

### Phase 3: Discover Life Context
- "이 요청을 하는 유저의 하루를 설명해주세요"
- "이 불편함이 처음 생기는 순간은 언제인가요?"
- "유저가 이 문제를 '참고 넘기는' 경우는 어떤 때인가요?"
- "이 유저의 주변 환경은? (시간 압박? 멀티태스킹? 이동 중?)"

See [references/product-patterns.md](references/product-patterns.md) for B2B, B2C, and marketplace-specific patterns.

## Unique Report Element

After the standard Voice/Need/Context report, add the **Customer Focused vs Customer Centric** comparison:

```
CUSTOMER FOCUSED vs CUSTOMER CENTRIC
========================================

+-- 고객 집중 (Voice Solution) -----------+
| "필터를 50개로 늘린다"                    |
| Cost: ████_  Impact: ██___              |
| Risk: 필터가 많아져도 탐색이 느릴 수 있음  |
+-- 고객 중심 (Context Solution) ----------+
| "큐레이션 + 탐색 동선 단축"               |
| Cost: ███__  Impact: █████              |
| Risk: 큐레이션 알고리즘 품질에 의존        |
+-----------------------------------------+
```

Cost/Impact bars use 5-block scale: each block = 20%.

## Report Location

Save to `.omc/reframes/product-{slug}.md`

## Execution Bridge (Product-Specific)

Present next steps via `AskUserQuestion`:

```
AskUserQuestion(
  question: "Reframing complete (Surface Risk: {r}%). How would you like to proceed?",
  options: [
    "Deep Interview → Define product spec from this problem",
    "Brainstorming → Design the product solution",
    "PRD → Write a Product Requirements Document",
    "Export → Save report and exit",
    "Dig Deeper → Continue exploring Context"
  ]
)
```

## All Other Behavior

Follows [context-reframing](../context-reframing/SKILL.md) exactly: same phases, scoring engine, challenge modes, state persistence, edge cases, and common rules. Only the weights, questions, and report format differ.
