# Prompt Reframing Patterns

## Common Ambiguous Requests and Their Reframes

### "리팩토링해줘" / "Refactor this"

| Voice | Possible Need | Possible Context |
|-------|--------------|-----------------|
| "리팩토링해줘" | 코드 가독성 향상 | 새 팀원 온보딩이 느리다 |
| | 성능 개선 | 유저 불만으로 응답 속도 이슈 |
| | 새 기능 준비 | 현재 구조로는 확장 불가 |
| | 테스트 가능성 | CI가 느리고 테스트가 깨진다 |

**Clarifying question:** "리팩토링으로 뭘 달성하려는 건가요? 가독성? 성능? 확장성?"

### "고쳐줘" / "Fix this"

| Voice | Possible Need | Possible Context |
|-------|--------------|-----------------|
| "고쳐줘" | 에러 해결 | 배포가 블록됨 |
| | 동작 수정 | 유저가 잘못된 결과를 받고 있음 |
| | 코드 품질 | 코드리뷰에서 반려됨 |

**Clarifying question:** "어떤 종류의 문제인가요? 에러? 잘못된 동작? 코드 품질?"

### "개선해줘" / "Improve this"

| Voice | Possible Need | Possible Context |
|-------|--------------|-----------------|
| "개선해줘" | UX 개선 | 전환율이 떨어지고 있음 |
| | 코드 품질 | 유지보수 비용이 증가 |
| | 성능 | 유저 이탈이 늘고 있음 |

**Clarifying question:** "개선의 기준이 뭔가요? 유저 경험? 코드 품질? 성능?"

## Passive Mode Detection Heuristics

### High-Confidence Ambiguity Signals

These patterns almost always benefit from clarification:
- Bare verb without object: "정리해줘" (organize what?)
- Vague scope: "이거 좀 봐줘" (look at what aspect?)
- Missing success criteria: "더 좋게 만들어줘" (better how?)
- Multiple interpretations: "업데이트해줘" (update code? docs? deps?)

### Low-Confidence Signals (Stay Silent)

These are usually clear enough to proceed:
- Specific file + action: "src/auth.ts에서 타입 에러 고쳐줘"
- Concrete criteria: "응답 시간 200ms 이하로 최적화해줘"
- Step in a workflow: "다음 단계 진행해줘" (context from prior conversation)
- Explicit preference: "그냥 해줘" / "just do it"

## Inline Confirmation Templates

### Standard Confirmation
```
I understood your context as:
  Said:      "{voice}"
  Intent:    {need}
  Situation: {context}

  Is this right?
  [Yes] [No, actually...] [Partially]
```

### Partial Confirmation (When Multiple Interpretations Remain)
```
I see a few possible interpretations:

  A) Intent: {interpretation_1} | Situation: {context_1}
  B) Intent: {interpretation_2} | Situation: {context_2}

  Which is closer? Or is it something else?
```

### Quick Passive Mode Confirmation
```
Quick check: "{voice}" — are you looking to {most_likely_need}?
  [Yes] [No, I mean...]
```
