# Worked Examples

## Example 1: The Elevator Mirror (Classic Reframe)

**Voice:** "엘리베이터가 느려요"

| Round | Question | Answer | Surface Risk |
|-------|----------|--------|-------------|
| 1 | "정확히 뭐라고 했나요?" | "주민들이 관리사무소에 '엘리베이터가 너무 느리다'고 항의" | 72% |
| 2 | "빠른 엘리베이터가 있으면 뭘 하려는 건가요?" | "빨리 올라가고 싶다. 특히 출근 시간에" | 55% |
| 3 | [Mirror] "진짜 불편한 건 속도인가요, 기다림인가요?" | "생각해보니 기다리는 게 지루한 거지, 이동 시간은 괜찮아요" | 28% |
| 4 | "기다리는 동안 뭘 하고 있나요?" | "멍하니 서 있어요. 핸드폰도 안 보게 되고" | 15% |

**Report:**
```
Voice:   "엘리베이터가 느려요"
Need:    빨리 이동하고 싶다
Context: 기다림이 지루하다 — 할 게 없는 빈 시간

Voice Solution:   모터 교체 (수천만원, 6개월 공사)
Need Solution:    층별 정차 최적화
Context Solution: 거울 설치 (10만원, 당일 설치) <- Recommended
```

## Example 2: The Filter Request (Product Domain)

**Voice:** "검색 필터를 더 늘려주세요"

| Round | Question | Answer | Surface Risk |
|-------|----------|--------|-------------|
| 1 | "유저가 정확히 뭐라고 했나요?" | "리뷰에 '필터가 부족하다'고 여러 건 올라옴" | 70% |
| 2 | "필터를 써서 뭘 하려는 건가요?" | "원하는 상품을 빠르게 찾고 싶어함" | 50% |
| 3 | "현재 필터 없이 어떻게 찾고 있나요?" | "카테고리 들어가서 스크롤하며 하나씩 봄" | 38% |
| 4 | "유저가 상품 찾는 데 보통 얼마나 걸리나요?" | "평균 세션 7분, 이탈률 높음" | 25% |
| 5 | [Levitt] "빠르게 찾는 것 뒤의 진짜 상황은?" | "출퇴근길에 핸드폰으로 쇼핑하는데 시간이 없음" | 12% |

**Report:**
```
Voice:   "검색 필터를 더 늘려주세요"
Need:    원하는 상품을 빠르게 찾고 싶다
Context: 출퇴근길 한정된 시간에 모바일로 탐색하며 헤매는 중

Voice Solution:   필터 옵션 50개로 확장
Need Solution:    검색 알고리즘 개선
Context Solution: 큐레이션 + 탐색 동선 단축 <- Recommended
```

## Example 3: Voice Confirmed (Edge Case)

**Voice:** "로그인 API 응답이 5초 이상 걸려요"

| Round | Question | Answer | Surface Risk |
|-------|----------|--------|-------------|
| 1 | "정확한 에러나 로그가 있나요?" | "타임아웃 로그: avg 5.2s, p99 8.1s" | 65% |
| 2 | "왜 빠른 로그인이 필요한가요?" | "유저 이탈: 3초 넘으면 40% 이탈" | 40% |
| 3 | [Mirror] "느린 건 진짜 문제인가요, 기다림이 문제인가요?" | "아니, 진짜 느린 거. SLA 위반이고 로그인 자체를 못 함" | 18% |

**Result: VOICE CONFIRMED**
```
Voice:   "로그인 API 응답이 5초 이상"
Context: SLA 위반 + 유저 이탈 — 실제로 속도가 문제

Verdict: Voice-level solution IS the Context-level solution.
Recommended: Proceed with performance optimization.
```

## Example 4: Inconclusive Exit (Edge Case)

After 15 rounds, Surface Risk still at 34%:

```
Result: INCONCLUSIVE (Surface Risk: 34.2%)

Hypotheses:
  H1: 탐색 동선이 길다 (confidence: 60%)
  H2: 카테고리 구조가 혼란스럽다 (confidence: 30%)
  H3: 검색어 매칭이 부정확하다 (confidence: 10%)

Recommended: Gather more data.
  [1] User research (interview/observation)
  [2] Analytics review (search logs, click paths)
  [3] Proceed with H1 (highest confidence, accept risk)
```
