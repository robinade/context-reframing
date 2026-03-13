---
name: product-reframing
description: "Use when analyzing feature requests, user feedback, customer complaints, or product requirements. Triggers: '/product-reframing', user feedback quotes, '유저가 ~라고 했는데', feature request analysis, customer voice, NPS/CSAT verbatims."
---

# Product Reframing

Extends [context-reframing](../context-reframing/SKILL.md) for product/planning decisions.

> "고객이 원하는 걸 만들었는데 왜 안 쓰지?" -- This skill prevents that.

```
NO FEATURE DECISIONS WITHOUT LIFE CONTEXT FIRST
```

<EXTREMELY-IMPORTANT>
This skill is an INTERACTIVE conversation with the user. You MUST use the AskUserQuestion tool
to ask every question and WAIT for real answers. NEVER simulate, fabricate, or assume user answers.
NEVER output questions as plain text. Every question goes through AskUserQuestion. No exceptions.
</EXTREMELY-IMPORTANT>

## Red Flags -- If You Think Any of These, STOP

| Your Thought | Reality |
|-------------|---------|
| "I can infer the user context from the feature request" | NO. That inference IS the Voice-level trap. Ask. |
| "The product domain is obvious" | NO. B2C/B2B/Platform changes everything. Use AskUserQuestion. |
| "I'll just ask in my response text" | NO. Plain text questions don't block. Use AskUserQuestion tool. |
| "I already know what users want" | NO. You know what they SAID, not what they NEED. |

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

All questions below MUST be asked via AskUserQuestion. NEVER output them as plain text.

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
| Cost: ____  Impact: __               |
| Risk: 필터가 많아져도 탐색이 느릴 수 있음  |
+-- 고객 중심 (Context Solution) ----------+
| "큐레이션 + 탐색 동선 단축"               |
| Cost: ___  Impact:                    |
| Risk: 큐레이션 알고리즘 품질에 의존        |
+-----------------------------------------+
```

Cost/Impact bars use 5-block scale: each block = 20%.

## Report Location

Save to `.omc/reframes/product-{slug}.md`

## Execution Bridge (Product-Specific)

After displaying the report, you MUST use AskUserQuestion to present choices:

```
AskUserQuestion(question="Reframing complete (Surface Risk: {r}%)\n\nNext step:\n  [1] Deep Interview - Define product spec from this problem\n  [2] Brainstorming - Design the product solution\n  [3] PRD - Write a Product Requirements Document\n  [4] Export - Save report and exit\n  [5] Dig Deeper - Continue exploring Context\n\nWhich would you like?")
```

Do NOT choose for the user. WAIT for their selection.

## All Other Behavior

Follows [context-reframing](../context-reframing/SKILL.md) exactly: same phases, AskUserQuestion enforcement, scoring engine, challenge modes, state persistence, edge cases, and common rules. Only the weights, questions, and report format differ.
