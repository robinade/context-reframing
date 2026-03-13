# Question Patterns Reference

## Targeting Strategy

Always target the **weakest scoring dimension**. If two are tied, prefer the one earlier in the Voice→Need→Context→Reframe sequence.

## Phase 1: Capture Voice (Voice Fidelity)

Goal: Get the exact words, not a summary.

| Pattern | Example |
|---------|---------|
| Quote request | "정확히 뭐라고 했나요? / What were the exact words?" |
| Tone probe | "그때 어떤 톤이었나요? 급한? 짜증난? 의례적인?" |
| Channel context | "이걸 어디서 들었나요? Slack? 미팅? 유저 리뷰?" |
| Frequency | "이 말을 처음 들은 건가요, 여러 번 반복되는 건가요?" |

## Phase 2: Excavate Need (Need Identification)

Goal: Find the immediate purpose behind the request.

| Pattern | Example |
|---------|---------|
| Without-it test | "이 기능 없이 지금 어떻게 하고 있나요?" |
| Behavior change | "이게 생기면 유저 행동이 어떻게 바뀌나요?" |
| Success metric | "이게 '잘 됐다'는 걸 어떻게 알 수 있나요?" |
| Priority trade-off | "속도 vs 정확도 — 어느 쪽이 더 중요한가요?" |
| Alternative path | "이 목표를 다른 방법으로 달성할 수 있다면?" |

## Phase 3: Discover Context (Context Discovery)

Goal: Uncover the real situation, emotion, and environment.

| Pattern | Example |
|---------|---------|
| Day-in-life | "이 요청을 하는 유저의 하루를 설명해주세요" |
| Trigger moment | "이 불편함이 처음 생기는 순간은 언제인가요?" |
| Tolerance test | "이 문제를 '참고 넘기는' 경우는 어떤 때인가요?" |
| Environment | "이걸 쓸 때 유저의 상황은? (이동 중? 집중? 멀티태스킹?)" |
| Workaround | "지금 이 문제를 어떻게 우회하고 있나요?" |
| Emotional probe | "이 상황에서 유저가 느끼는 감정은?" |

## Phase 4: Validate Reframe (Reframe Validity)

Goal: Confirm the reframed problem is more useful than the original.

| Pattern | Example |
|---------|---------|
| Comparison test | "원래 요청대로 하면 vs 이 관점으로 접근하면 — 어느 쪽이 더 효과적?" |
| Stakeholder check | "이 reframe을 이해관계자에게 설명하면 동의할까요?" |
| Risk assessment | "원래 요청대로 진행할 때 가장 큰 리스크는?" |
| Testability | "이 reframe이 맞는지 어떻게 검증할 수 있을까요?" |

## Handling Degraded Answers

| User Response | Action |
|---------------|--------|
| "I don't know" / "모르겠어요" | Score at current level, move to next weakest dimension |
| Contradicts prior answer | Note it, re-score affected dimensions (scores may decrease) |
| Refuses to answer | Offer early exit with Surface Risk warning |
| Off-topic answer | Gently redirect: "유용한 맥락이네요. 다시 {weakest}로 돌아가면..." |
