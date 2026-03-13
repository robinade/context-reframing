# Debug Reframing Patterns

## Symptom → Cause → Design Flaw Chains

### Authentication Failures
```
Voice:   "로그인이 안 돼요"
Need:    세션 토큰이 만료됨
Context: 토큰 갱신 로직이 네트워크 에러를 무시하는 설계 결함

L1 Fix: try/catch에 retry 추가 (HIGH recurrence)
L2 Fix: refreshToken에 에러 핸들링 (MEDIUM recurrence)
L3 Fix: Offline-tolerant auth architecture (LOW recurrence)
```

### Performance Issues
```
Voice:   "페이지가 느려요"
Need:    렌더링에 3초 이상 소요
Context: N+1 쿼리 패턴 + 캐시 미적용 설계

L1 Fix: 로딩 스피너 추가 (HIGH recurrence)
L2 Fix: 쿼리 최적화 (MEDIUM recurrence)
L3 Fix: 캐싱 레이어 + 데이터 접근 패턴 재설계 (LOW recurrence)
```

### Data Inconsistency
```
Voice:   "숫자가 안 맞아요"
Need:    두 화면에서 다른 값 표시
Context: 단일 진실 원천(SSOT) 없이 여러 곳에서 계산하는 설계

L1 Fix: 두 화면의 계산 로직 동기화 (HIGH recurrence)
L2 Fix: 공유 계산 함수 추출 (MEDIUM recurrence)
L3 Fix: SSOT 기반 데이터 아키텍처 (LOW recurrence)
```

## Auto-Exploration Strategy

### What to Explore First
1. **Error origin**: Stack trace의 최초 발생 지점
2. **Call chain**: 에러를 발생시키는 전체 호출 경로
3. **Similar patterns**: 같은 패턴이 쓰인 다른 파일들
4. **Recent changes**: `git log --oneline -20` 관련 파일 변경 이력
5. **Test coverage**: 해당 경로에 테스트가 있는지

### What to Look For
- **Error handling gaps**: catch 블록이 에러를 삼키는 곳
- **Implicit assumptions**: null 체크 없이 접근하는 곳
- **Shared mutable state**: 여러 곳에서 동시에 수정하는 데이터
- **Missing boundaries**: 외부 입력을 검증 없이 사용하는 곳

## Debug-Specific Challenge Mode Adaptations

### Mirror Mode for Debugging
Challenge whether the "error" is the real problem:
- "이 에러가 실제로 문제인가요, 아니면 다른 문제의 증상인가요?"
- "이 에러를 완벽히 고쳐도 유저 경험이 나아지나요?"

### Levitt Mode for Debugging
Push past the immediate cause:
- "이 버그를 고치면 비슷한 버그가 다른 곳에서 발생할 가능성은?"
- "이 코드가 이렇게 작성된 근본적인 이유는?"

### Inversion Mode for Debugging
Question whether the failing component should exist:
- "이 컴포넌트가 아예 없으면 시스템이 더 단순해지나요?"
- "이 기능을 다르게 설계하면 이 에러 클래스 자체가 사라지나요?"
