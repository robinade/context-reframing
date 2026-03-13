---
name: prompt-reframing
description: "Reframes ambiguous AI conversation requests from Voice (literal ask) to Context (work situation) for better responses. Includes passive mode for automatic detection of ambiguous prompts. Use when a user's request seems vague or could mean different things depending on context. Triggers: '/prompt-reframing', '내 질문 다시 이해해봐', 'reinterpret my question', 'what do I really mean', or passive mode auto-detection of ambiguous prompts."
---

# Prompt Reframing

Extends [context-reframing](../context-reframing/SKILL.md) for AI conversations. Maps Voice→Need→Context to **Literal Ask→Intent→Work Situation**.

> "리팩토링해줘" could mean cleanup for readability, prep for new features, or fixing an onboarding bottleneck. The right response depends entirely on WHY.

## How It Differs From Core

| Aspect | Core (Universal) | Prompt |
|--------|-----------------|--------|
| Weights | Context 35% | **Equal 25% all** |
| Voice = | "What they said" | Literal Ask |
| Need = | Immediate goal | Intent |
| Context = | Real situation | Work Situation |
| Output | Report file | **Inline confirmation** (no file) |
| Unique feature | — | **Passive Mode** |

## Prompt-Specific Weights

All dimensions weighted equally at 25%. AI conversations need balanced clarity — no single dimension dominates.

## Prompt Question Patterns

### Phase 1: Capture Literal Ask
- "정확히 뭘 해달라는 건가요?"
- "결과물이 어떤 형태면 되나요? (코드? 설명? 계획?)"

### Phase 2: Identify Intent
- "이걸 왜 하려는 건가요?"
- "이 결과물로 뭘 하실 건가요?"
- "어떤 문제를 해결하려는 건가요?"

### Phase 3: Discover Work Situation
- "지금 작업 맥락이 뭔가요? (새 기능? 디버깅? 온보딩?)"
- "이 작업의 긴급도와 중요도는?"
- "팀 내에서 이 작업의 목적은?"

## Output: Inline Confirmation via AskUserQuestion

Prompt reframing is lightweight. Instead of generating a report file, confirm your understanding interactively:

First, display the reframed understanding as text:
```
I understood your context as:
  Said:      "리팩토링해줘"
  Intent:    코드 가독성 향상
  Situation: 새 팀원 온보딩이 느려서 코드를 이해하기 쉽게 만들려는 것
```

Then immediately use `AskUserQuestion` to confirm:
```
AskUserQuestion(
  question: "Is this understanding correct?",
  options: [
    "Yes, that's exactly right — proceed",
    "Partially right, let me clarify...",
    "No, that's not what I meant"
  ]
)
```

Then proceed directly with the reframed understanding. No file saved.

## Passive Mode

When activated, Claude automatically runs Voice→Need→Context analysis on ambiguous requests without explicit skill invocation.

**Activate:** `/prompt-reframing --passive`
**Deactivate:** `/prompt-reframing --passive off`

### How It Works

1. On activation, writes state to `.omc/state/reframing-passive.json`:
```json
{
  "passive_mode": true,
  "activated_at": "2026-03-14T08:00:00Z"
}
```

2. On each user message, if passive mode is active:
   - Internally analyze: is this request at Voice level?
   - If ambiguous: ask ONE clarifying question before proceeding
   - If clear: proceed normally (no interruption)

3. On deactivation: deletes the state file

### When Passive Mode Triggers

- Request uses vague verbs without targets ("개선해줘", "고쳐줘", "정리해줘")
- Request could mean multiple very different things
- Request lacks context that would significantly change the approach

### When Passive Mode Stays Silent

- Request includes file paths, function names, or concrete criteria
- Request is simple and unambiguous
- Request explicitly says "just do it" or "skip the questions"

## Execution Bridge

No bridge needed — prompt reframing flows directly into the user's actual task with the reframed understanding applied.

## All Other Behavior

Follows [context-reframing](../context-reframing/SKILL.md) for active (non-passive) mode: same phases, scoring engine, challenge modes. Passive mode is a lightweight subset that skips formal scoring and report generation.
