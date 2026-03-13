---
name: context-reframing
description: "Transforms surface-level requests (Voice) into deep contextual understanding (Context) before proposing solutions. Prevents solving the wrong problem well. Use when encountering feature requests, bug reports, vague requirements, user feedback, or any situation where the stated problem might not be the real problem. Triggers: 'reframe', '진짜 문제가 뭐야', 'what is the real problem', 'Voice→Need→Context', or when you suspect a request addresses symptoms rather than root causes."
---

# Context Reframing

Surface-level requests lead to surface-level solutions. This skill systematically excavates the real problem before you commit to solving the wrong one.

<HARD-GATE>
Do NOT propose solutions until Surface Risk drops below 20%. Solving the wrong problem well is worse than not solving it at all.
</HARD-GATE>

## The Core Insight

| Level | Name | What It Is | Elevator Example | Filter Example |
|-------|------|-----------|-----------------|---------------|
| L1 | **Voice** | What they said | "엘리베이터가 느려요" | "필터를 더 늘려주세요" |
| L2 | **Need** | Immediate goal | "빨리 이동하고 싶다" | "상품을 빨리 찾고 싶다" |
| L3 | **Context** | Real situation | "기다림이 지루하다" | "탐색하며 헤매는 중" |

**Voice-level solution** (고객 집중): Faster motor / 50 more filters
**Context-level solution** (고객 중심): Install a mirror / Better curation

## When to Use

- Feature requests or user feedback that might be surface-level
- Bug reports where the symptom might mask a deeper design flaw
- Vague requirements before committing to an approach
- Any time "solving the stated problem" feels suspiciously easy
- When someone quotes user feedback: "유저가 ~라고 했는데"

## When NOT to Use

- The request is concrete and specific (file paths, function names, acceptance criteria)
- You already understand the full context
- The user says "just do it" or "skip the questions"
- Simple, mechanical tasks (formatting, renaming, standard CRUD)

## Execution Flow

### Phase 1: Initialize

1. **Detect project type**: brownfield (existing code) or greenfield
2. **For brownfield**: Spawn `explore` agent to map relevant code areas before asking the user anything
3. **Initialize state** at `.omc/state/reframing-state.json`
4. **Announce**:

> Starting context reframing. I'll ask targeted questions to find the real problem behind this request. After each answer, I'll show your Context Depth Score.
>
> **Your request:** "{voice}"
> **Project type:** {greenfield|brownfield}
> **Current Surface Risk:** 100%

### Phase 2: Reframing Loop

Repeat until Surface Risk ≤ 0.2 OR early exit OR hard cap (15 rounds):

**Step A — Target the weakest dimension**

Identify which of the 4 scoring dimensions has the lowest score. Generate ONE question that specifically improves that dimension. Questions should expose ASSUMPTIONS, not gather feature lists.

See [references/question-patterns.md](references/question-patterns.md) for templates by phase and dimension.

**Step B — Ask the question**

```
Round {n} | Targeting: {weakest_dimension} | Surface Risk: {score}%

{question}
```

**Step C — Score all 4 dimensions**

After receiving the answer, re-score ALL dimensions from scratch using the full conversation so far. Scores CAN decrease if contradictions emerge.

See [references/scoring-engine.md](references/scoring-engine.md) for the 5-point rubric and calculation logic.

**Step D — Display progress**

```
Round {n} complete.

| Dimension        | Score | Weight | Weighted | Gap              |
|------------------|-------|--------|----------|------------------|
| Voice Fidelity   | {s}   | {w}%   | {s*w}    | {gap or "Clear"} |
| Need ID          | {s}   | {w}%   | {s*w}    | {gap or "Clear"} |
| Context Disc.    | {s}   | {w}%   | {s*w}    | {gap or "Clear"} |
| Reframe Valid.   | {s}   | {w}%   | {s*w}    | {gap or "Clear"} |
| **Surface Risk** |       |        | **{r}%** |                  |

{r <= 20 ? "Threshold met. Ready to report." : "Next question targets: {weakest}"}
```

**Step E — Check limits**

- **Round 3+**: Allow early exit if user says "enough" / "let's go" / "그만"
- **Round 10**: Soft warning: "10 rounds reached. Surface Risk: {r}%. Continue or proceed?"
- **Round 15**: Hard cap — proceed with current clarity

### Phase 3: Challenge Modes

At specific round thresholds, shift questioning perspective. Each mode activates ONCE, then returns to normal questioning. Track used modes in state.

| Mode | Round | Inspiration | Core Question |
|------|-------|-------------|---------------|
| **Mirror** (거울) | 3+ | Elevator mirror | "인지된 문제가 진짜 문제인가? 이 요청 뒤의 감정은?" |
| **Levitt** (레빗) | 5+ | Drill→Hole→Picture | "한 단계 더: Need 뒤의 Context는?" |
| **Inversion** (반전) | 7+ | Adhesive hook | "이 필요 자체를 없앨 수는 없을까?" |

See [references/challenge-modes.md](references/challenge-modes.md) for prompt templates and activation rules.

**Stall detection**: If Surface Risk doesn't change by more than ±0.05 for 3 consecutive rounds, activate the next unused challenge mode.

### Phase 4: Generate Report

```
CONTEXT REFRAMING REPORT
=======================================
Surface Risk: {r}% (threshold: ≤20%)

+-- VOICE ------------------------------+
| "{exact user words}"                   |
+-- NEED --------------------------------+
| {identified immediate goal}            |
+-- CONTEXT -----------------------------+
| {discovered real situation}            |
+----------------------------------------+

SOLUTIONS BY LEVEL
--------------------------------------
Voice Solution:   {literal solution}
Need Solution:    {goal-addressing solution}
Context Solution: {situation-addressing solution}  <- Recommended

CONTEXT DEPTH SCORE
+------------------+-------+--------+----------+
| Dimension        | Score | Weight | Weighted |
+------------------+-------+--------+----------+
| Voice Fidelity   | {s}   |  {w}%  |  {s*w}   |
| Need ID          | {s}   |  {w}%  |  {s*w}   |
| Context Disc.    | {s}   |  {w}%  |  {s*w}   |
| Reframe Valid.   | {s}   |  {w}%  |  {s*w}   |
+------------------+-------+--------+----------+
| SURFACE RISK     |       |        |  {r}%    |
+------------------+-------+--------+----------+

ASSUMPTIONS EXPOSED
+----------------------------+-------------------------+
| {what was assumed}         | -> {what was discovered} |
+----------------------------+-------------------------+
```

Save report to `.omc/reframes/general-{slug}.md`.

### Phase 5: Execution Bridge

```
Reframing complete (Surface Risk: {r}%)

Next step:
  [1] Deep Interview → Define spec from this problem
  [2] Brainstorming → Jump to solution design
  [3] Export → Save report and exit
  [4] Dig Deeper → Continue exploring Context
```

## Context Depth Score (CDS)

```
Surface Risk = 1 - (voice × w_v + need × w_n + context × w_c + reframe × w_r)
```

**Gate:** Surface Risk ≤ 0.2 → ready to proceed.

**Universal weights**: Voice 20% / Need 25% / Context 35% / Reframe 20%

Domain skills override these weights. See [references/scoring-engine.md](references/scoring-engine.md) for full rubrics and domain weight profiles.

## Common Rules

| Rule | Detail |
|------|--------|
| One question at a time | Never batch multiple questions |
| Score every round | Display CDS transparently after each answer |
| Gather facts first | Explore codebase BEFORE asking user about it |
| Early exit | Round 3+, with Surface Risk warning |
| Hard cap | 15 rounds max |
| State persistence | `.omc/state/reframing-state.json` for resume |
| Challenge modes | Mirror (R3+), Levitt (R5+), Inversion (R7+) — each once |

## Edge Cases

**Voice Confirmed** — When Voice IS the real problem:
Report shows `Result: VOICE CONFIRMED`. Reframe Validity scores 1.0 when Voice is validated as correct. The reframe confirms the original framing.

**Inconclusive Exit** — Hard cap reached with Surface Risk > 0.2:
Report shows `Result: INCONCLUSIVE`. Lists ranked hypotheses with confidence levels and recommends data gathering.

**Domain Overlap** — Request matches multiple domains:
Ask: "이 문제를 코드 수준에서 고치려는 건가요, 아니면 유저 경험 차원에서 분석하려는 건가요?"
Default to this universal skill if still ambiguous, then route to domain skill after Phase 1.

See [references/examples.md](references/examples.md) for worked examples of each path.

## Domain Skills

For domain-specific reframing with tailored weights, questions, and report formats:

- **Product**: `/product-reframing` — Feature requests, user feedback (Context 40%)
- **Debug**: `/debug-reframing` — Bugs, errors, stack traces (Reframe 30%)
- **Prompt**: `/prompt-reframing` — AI conversation, ambiguous requests (balanced 25%)

## Pipeline Position

```
context-reframing → deep-interview → brainstorming → execution
  "Real problem"     "Specification"   "Design"        "Build"
```

This skill handles problem DEFINITION, not solution SPECIFICATION. Keep it fast (5-10 min typical).

## Design Principles

1. **Voice is not the enemy** — Capturing Voice accurately is the FIRST step. We don't dismiss what was said; we go deeper.
2. **Context is not always deeper** — Sometimes Voice IS the real problem. The skill validates this too.
3. **Empathy over analysis** — The elevator mirror worked because it addressed an EMOTION (boredom), not a metric (speed).
4. **Lighter than a spec** — This is problem definition, not solution specification.
5. **The reframe must be testable** — "Is this reframe more useful than the original request?" is always the final validation.
