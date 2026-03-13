---
name: debug-reframing
description: "Use when encountering bugs, errors, stack traces, test failures, or recurring issues that keep coming back. Triggers: '/debug-reframing', error messages, '안 돼요', stack traces, recurring bugs, '근본 원인이 뭐야', or when a bug has been 'fixed' multiple times."
---

# Debug Reframing

Extends [context-reframing](../context-reframing/SKILL.md) for debugging. Maps Voice->Need->Context to **Symptom->Cause->Design Flaw**.

```
NO FIXES WITHOUT DESIGN FLAW UNDERSTANDING FIRST
```

<EXTREMELY-IMPORTANT>
This skill is an INTERACTIVE conversation with the user. You MUST use the AskUserQuestion tool
to ask every question and WAIT for real answers. NEVER simulate, fabricate, or assume user answers.
NEVER output questions as plain text. Every question goes through AskUserQuestion. No exceptions.
</EXTREMELY-IMPORTANT>

<HARD-GATE>
A retry loop around a flaky call is a Voice-level fix. Understanding WHY the call is flaky -- that's Context. Do not propose fixes until you understand the design flaw.
</HARD-GATE>

## Red Flags -- If You Think Any of These, STOP

| Your Thought | Reality |
|-------------|---------|
| "I can see the bug in the code, no need to ask" | NO. You see the SYMPTOM. The design flaw needs user context. Use AskUserQuestion. |
| "The fix is obvious from the stack trace" | NO. Obvious fixes are L1 patches. Ask about the design intent. |
| "I'll explore code and fix it directly" | Explore first, YES. But still ask the user about design intent via AskUserQuestion. |
| "The user just wants it fixed fast" | A fast L1 fix that recurs wastes MORE time. Ask the real questions. |

## How It Differs From Core

| Aspect | Core (Universal) | Debug |
|--------|-----------------|-------|
| Reframe weight | 20% | **30%** |
| Voice = | "What they said" | Symptom / Error |
| Need = | Immediate goal | Direct Cause |
| Context = | Real situation | Design Flaw |
| Unique feature | -- | **Auto Codebase Exploration** |
| Unique output | Solutions by level | **Fix Depth Comparison** |

## Debug-Specific Weights

| Dimension | Weight | Why |
|-----------|--------|-----|
| Voice Fidelity | 20% | Exact error messages and stack traces are critical evidence |
| Need Identification | 20% | Direct cause must be identified before going deeper |
| Context Discovery | 30% | Design flaws hide beneath immediate causes |
| **Reframe Validity** | **30%** | The fix MUST address root cause, not just symptoms |

## Auto Codebase Exploration

Before asking the user ANY question, automatically:

1. Spawn `explore` agent to scan files related to the error
2. Analyze error logs, stack traces, and test output
3. Read relevant source code sections
4. Form initial hypotheses

Then ask INFORMED questions based on what the code reveals. Never ask the user what the code already tells you. But you MUST still use AskUserQuestion for every question to the user.

## Debug Question Patterns

All questions below MUST be asked via AskUserQuestion. NEVER output them as plain text.

### Phase 1: Capture Symptom
- "정확한 에러 메시지나 스택 트레이스가 있나요?"
- "이 증상이 항상 발생하나요, 간헐적인가요?"
- "마지막으로 정상 작동한 시점은 언제인가요?"
- "이 에러를 재현하는 정확한 단계는?"

### Phase 2: Identify Direct Cause
- "이 에러가 발생하는 코드 경로를 추적해봤나요?"
- "[코드 탐색 결과] {file}:{line}에서 {condition}일 때 실패하는 것 같은데, 맞나요?"
- "이 문제가 특정 환경에서만 발생하나요? (dev/staging/prod)"
- "최근에 관련 코드 변경이 있었나요?"

### Phase 3: Discover Design Flaw
- "이 코드가 이렇게 설계된 원래 의도는 뭔가요?"
- "이 패턴이 프로젝트 다른 곳에서도 쓰이나요?"
- "이 에러가 다른 형태로 재발한 적이 있나요?"
- "이 컴포넌트의 실패 모드를 설계할 때 고려했나요?"

## Unique Report Element -- Fix Depth Comparison

```
FIX DEPTH COMPARISON
========================================

+-- Level 1 Fix (Symptom) ----------------+
| try/catch에 retry 추가                    |
| Recurrence risk: HIGH                    |
| Effort: Low                              |
+-- Level 2 Fix (Cause) ------------------+
| refreshToken에 에러 핸들링 추가            |
| Recurrence risk: MEDIUM                  |
| Effort: Medium                           |
+-- Level 3 Fix (Design) -----------------+
| Offline-tolerant auth architecture       |
| Recurrence risk: LOW                     |
| Effort: High                   <- REC   |
+-----------------------------------------+
```

## Report Location

Save to `.omc/reframes/debug-{slug}.md`

## Execution Bridge (Debug-Specific)

After displaying the report, you MUST use AskUserQuestion to present choices:

```
AskUserQuestion(question="Reframing complete (Surface Risk: {r}%)\n\nNext step:\n  [1] Systematic Debugging - Apply reframed understanding\n  [2] Direct Fix - Implement the Context-level solution\n  [3] Architecture Review - Evaluate design flaw scope\n  [4] Export - Save report and exit\n  [5] Dig Deeper - Continue investigating\n\nWhich would you like?")
```

Do NOT choose for the user. WAIT for their selection.

## All Other Behavior

Follows [context-reframing](../context-reframing/SKILL.md) exactly: same phases, AskUserQuestion enforcement, scoring engine, challenge modes, state persistence, edge cases, and common rules. Only the weights, questions, auto-exploration, and report format differ.
