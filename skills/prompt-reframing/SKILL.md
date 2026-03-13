---
name: prompt-reframing
description: "Use when a user's request seems vague or could mean different things depending on context. Triggers: '/prompt-reframing', '내 질문 다시 이해해봐', 'reinterpret my question', 'what do I really mean', or passive mode auto-detection of ambiguous prompts."
---

# Prompt Reframing

Extends [context-reframing](../context-reframing/SKILL.md) for AI conversations. Maps Voice->Need->Context to **Literal Ask->Intent->Work Situation**.

> "리팩토링해줘" could mean cleanup for readability, prep for new features, or fixing an onboarding bottleneck. The right response depends entirely on WHY.

```
NO EXECUTION WITHOUT INTENT CLARITY FIRST
```

<EXTREMELY-IMPORTANT>
This skill REQUIRES real user interaction. You MUST use the AskUserQuestion tool for every
question and confirmation. NEVER simulate answers. NEVER skip the confirmation step.
NEVER output questions as plain text. Every interaction goes through AskUserQuestion.

The inline confirmation at the end is ESPECIALLY critical -- you MUST use AskUserQuestion
to present "Is this right? [Yes] [No] [Partially]" and WAIT for the user's actual response
before proceeding. If you skip this, you will execute based on assumptions, which is the
exact problem this skill exists to prevent.
</EXTREMELY-IMPORTANT>

## Red Flags -- If You Think Any of These, STOP

| Your Thought | Reality |
|-------------|---------|
| "The request is clear enough to proceed" | If it were clear, this skill wouldn't have triggered. Use AskUserQuestion. |
| "I'll ask a quick clarifying question in my response" | NO. Plain text doesn't block. Use AskUserQuestion tool. |
| "I can show the confirmation and proceed" | NO. Show confirmation via AskUserQuestion, then WAIT. |
| "Passive mode means I should be subtle" | Subtle yes, skip AskUserQuestion no. One clarifying question via the tool. |
| "I'll just assume Yes for the confirmation" | NEVER. The confirmation exists because your assumption might be wrong. |

## How It Differs From Core

| Aspect | Core (Universal) | Prompt |
|--------|-----------------|--------|
| Weights | Context 35% | **Equal 25% all** |
| Voice = | "What they said" | Literal Ask |
| Need = | Immediate goal | Intent |
| Context = | Real situation | Work Situation |
| Output | Report file | **Inline confirmation** (no file) |
| Unique feature | -- | **Passive Mode** |

## Prompt-Specific Weights

All dimensions weighted equally at 25%. AI conversations need balanced clarity -- no single dimension dominates.

## Prompt Question Patterns

All questions below MUST be asked via AskUserQuestion. NEVER output them as plain text.

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

## Output: Inline Confirmation

Prompt reframing is lightweight. Instead of generating a report file, use AskUserQuestion to present an inline confirmation:

```
AskUserQuestion(question="I understood your context as:\n  Said:      \"{voice}\"\n  Intent:    {need}\n  Situation: {context}\n\n  Is this right?\n  [Yes] [No, actually...] [Partially]")
```

<HARD-GATE>
You MUST wait for the user's response to the confirmation before proceeding.
- If "Yes": proceed with the reframed understanding
- If "No, actually...": the user will clarify, restart reframing with new information
- If "Partially": use AskUserQuestion to ask which part is wrong
NEVER assume "Yes". NEVER proceed without the actual response.
</HARD-GATE>

## Passive Mode

When activated, Claude automatically runs Voice->Need->Context analysis on ambiguous requests without explicit skill invocation.

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
   - If ambiguous: use AskUserQuestion to ask ONE clarifying question before proceeding
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

### Passive Mode Question Format

Even in passive mode, clarifying questions MUST use AskUserQuestion:

```
AskUserQuestion(question="Quick check: \"{voice}\" -- are you looking to {most_likely_need}?\n  [Yes] [No, I mean...]")
```

## Execution Bridge

No bridge needed -- prompt reframing flows directly into the user's actual task with the reframed understanding applied. But ONLY after the user confirms via AskUserQuestion.

## All Other Behavior

Follows [context-reframing](../context-reframing/SKILL.md) for active (non-passive) mode: same phases, AskUserQuestion enforcement, scoring engine, challenge modes. Passive mode is a lightweight subset that skips formal scoring and report generation but STILL uses AskUserQuestion for its one clarifying question.
