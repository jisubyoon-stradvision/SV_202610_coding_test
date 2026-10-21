# STRADVISION 라이브 코딩 테스트 (2026-10)

## 안내

- 시간: 60분. 문제는 2개이며, 문제 1부터 푸는 것을 권합니다.
- 언어: 자유입니다 (C, C++, Python 등). 표준 라이브러리만으로 풀 수 있습니다.
- 진행: 화면을 공유한 상태로 코드를 작성합니다. 생각하는 과정을 말로 설명해 주세요.
- 질문: 문제에 애매한 부분이 있으면 언제든 질문해도 됩니다. 질문하는 것도 평가에 긍정적으로 반영됩니다.
- 허용: 언어 문법과 표준 라이브러리 공식 문서 검색
- 금지: AI 도구 (ChatGPT, Claude, Copilot 등), AI 자동 완성
- 입력은 표준 입력(stdin)으로 받아 표준 출력(stdout)으로 내보내는 형태를 기본으로 합니다. 함수로 구현하고 예시를 직접 넣어 실행하는 방식도 괜찮습니다.
- 완벽한 정답보다 접근 방법과 코드를 다듬어 가는 과정을 봅니다.

---

## 문제 1. 에이전트 로그 집계

여러 에이전트의 로그가 한 줄씩 들어옵니다. 한 줄의 형식은 다음과 같습니다.

```
<시각> <에이전트ID> <레벨> <메시지>
```

- 메시지에는 공백이 들어갈 수 있습니다.
- 형식이 깨진 줄과 빈 줄은 건너뜁니다.

에이전트·레벨 조합별 로그 건수를 세어 출력하세요.

- 출력 형식: `<에이전트ID> <레벨> <건수>`
- 정렬 순서: 건수 내림차순. 건수가 같으면 에이전트ID 오름차순, 그다음 레벨 오름차순

### 입력 예시

```
2026-10-21T10:00:01 agent-01 INFO start
2026-10-21T10:00:02 agent-02 ERROR disk full
2026-10-21T10:00:03 agent-01 WARN slow
2026-10-21T10:00:04 agent-02 ERROR disk full

2026-10-21T10:00:05 agent-01 INFO done
broken-line
2026-10-21T10:00:06 agent-03 ERROR timeout
```

### 출력 예시

```
agent-01 INFO 2
agent-02 ERROR 2
agent-01 WARN 1
agent-03 ERROR 1
```

---

## 문제 2. 장비 명령 상태 머신

장비는 `IDLE`, `MOVING`, `FAULT` 세 가지 상태를 가집니다. 시작 상태는 `IDLE`입니다.

명령 목록을 순서대로 처리하세요.

- 현재 상태에서 허용되는 명령이면 `ACK,<명령>`을 출력하고 상태를 바꿉니다.
- 허용되지 않는 명령이면 `NACK,<명령>,<현재 상태>`를 출력하고 상태는 그대로 둡니다.
- 모든 명령을 처리한 뒤 `final: <마지막 상태>`를 출력합니다.

### 상태 전이 규칙

| 현재 상태 | 명령 | 다음 상태 |
| --- | --- | --- |
| IDLE | MOVE | MOVING |
| MOVING | STOP | IDLE |
| MOVING | DONE | IDLE |
| IDLE | FAULT | FAULT |
| MOVING | FAULT | FAULT |
| FAULT | RESET | IDLE |

표에 없는 (상태, 명령) 조합은 허용되지 않는 명령입니다.

### 입력 예시

명령이 공백으로 구분되어 한 줄로 들어옵니다.

```
MOVE MOVE DONE STOP MOVE FAULT MOVE RESET MOVE
```

### 출력 예시

```
ACK,MOVE
NACK,MOVE,MOVING
ACK,DONE
NACK,STOP,IDLE
ACK,MOVE
ACK,FAULT
NACK,MOVE,FAULT
ACK,RESET
ACK,MOVE
final: MOVING
```
