# Challenge Modes Reference

Challenge modes shift the questioning perspective at specific round thresholds. Each mode activates ONCE, then returns to normal Socratic questioning. Track used modes in state to prevent repetition.

## Mirror Mode (거울 모드) — Round 3+

**Inspiration:** Residents complained the elevator was slow. Engineers couldn't make it faster. A psychologist installed a mirror — complaints dropped to zero. The problem wasn't speed; it was boredom while waiting.

**Purpose:** Challenge whether the perceived problem is the real problem. Look for the emotion behind the request.

**Prompt injection:**
> You are now in MIRROR mode. Challenge whether the stated problem is the actual problem. Ask about the EMOTION or EXPERIENCE behind the request. Like the elevator mirror — "slow elevator" was really "boring wait." What emotion drives this request?

**Example questions:**
- "잠깐, 이 요청의 표면 아래에 있는 감정이 뭔가요? 불안? 좌절? 지루함?"
- "엘리베이터 거울 이야기처럼 — 진짜 불편한 건 뭔가요?"
- "이 기능이 없어서 유저가 느끼는 감정을 한 단어로?"

## Levitt Mode (레빗 모드) — Round 5+

**Inspiration:** Theodore Levitt: "People don't want a quarter-inch drill. They want a quarter-inch hole." But deeper: they don't want the hole — they want to hang a picture. Deeper still: they want their home to feel like theirs.

**Purpose:** Push past Need into Context. Each "why" reveals a deeper layer.

**Prompt injection:**
> You are now in LEVITT mode. The user has identified a Need, but there's a deeper Context. Like Levitt's drill → hole → picture → home identity chain, ask "why does this Need matter?" to excavate the Context layer. What life situation makes this Need urgent?

**Example questions:**
- "드릴 → 구멍 → 액자 → '내 집다운 느낌' 처럼 — 이 Need 뒤의 Context는 뭔가요?"
- "이 목표가 중요한 이유가 뭔가요? 한 단계 더 들어가면?"
- "이 Need가 충족되면 유저의 삶에서 뭐가 달라지나요?"

## Inversion Mode (반전 모드) — Round 7+

**Inspiration:** The adhesive hook. Instead of a better drill, eliminate the need to drill entirely. Command strips solve "hang a picture" without making any holes.

**Purpose:** Question whether the Need itself can be eliminated. The most elegant solution removes the problem rather than solving it.

**Prompt injection:**
> You are now in INVERSION mode. Instead of solving the problem better, ask whether the problem itself can be eliminated. Like adhesive hooks that removed the need for drilling — what if this Need simply didn't exist? What would make this request unnecessary?

**Example questions:**
- "이 필요 자체를 없앨 수는 없을까요?"
- "접착 훅처럼 — 드릴 없이 액자를 거는 방법은?"
- "이 문제가 아예 발생하지 않는 설계는 어떤 모습일까요?"
- "이 기능 요청이 불필요해지는 시나리오는?"

## Activation Rules

1. Check if mode has been used (via state `challenge_modes_used` array)
2. If not used AND round threshold met → activate
3. Inject the prompt ONCE into question generation
4. Add mode name to `challenge_modes_used`
5. Return to normal Socratic questioning next round

## Stall Detection

If Surface Risk doesn't change by more than ±0.05 for 3 consecutive rounds:
- If unused challenge modes remain → activate the next available one
- If all modes used → suggest early exit or reframe the problem from scratch
