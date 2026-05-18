# Contributing — 에이전트 행동 강령

> 이 파일은 **Claude Code를 포함한 모든 AI 에이전트**가 이 레포지토리에서 작업할 때 반드시 따라야 하는 규칙입니다.

---

## 세션 시작 시 — 어떤 파일을 읽어야 하는가?

```
AGENT_BOOTSTRAP.md가 존재하는가?
        │
       YES → §1 최초 초기화 프로토콜 실행
        │
        NO → AGENT_STATE.md가 존재하는가?
                    │
                   YES → §2 일반 세션 프로토콜 실행
                    │
                    NO → 사용자에게 문의 (비정상 상태)
```

---

## §1. 최초 초기화 프로토콜 (AGENT_BOOTSTRAP.md 존재 시)

> 이 프로토콜은 프로젝트 생애 **딱 한 번**만 실행됩니다.

1. `AGENT_BOOTSTRAP.md` 전체를 읽는다
2. 루트 `README.md`의 Progress Tracker와 Next Roadmap을 읽는다
3. `AGENT_BOOTSTRAP.md §5`의 지시에 따라 `AGENT_STATE.md`를 생성한다
4. `AGENT_BOOTSTRAP.md`를 **삭제**한다
5. 사용자에게 초기화 완료를 보고하고 작업 지시를 기다린다

**이후 모든 세션은 §2 프로토콜만 따릅니다. BLUEPRINT.md는 읽지 않습니다.**

---

## §2. 일반 세션 프로토콜 (매 세션, AGENT_STATE.md 존재 시)

### 세션 시작 (읽기)

1. `AGENT_STATE.md` 전체를 읽는다
   - **누적 사용자 요구사항** → 이미 처리된 것 확인, 중복 방지
   - **현재 작업 상태** → 이어받을 Feature 파악
   - **다음 할 일** → 이번 세션의 작업 범위 확인
   - **핵심 규칙 스냅샷** → 이번 세션에 적용할 제약 확인
   - **세션 로그** → 직전 세션 인계 사항 확인

2. 사용자의 이번 세션 요청을 받는다

3. 요청이 **누적 사용자 요구사항**에 이미 있으면 → 완료 여부 확인 후 불필요한 재작업 방지

### 작업 중

4. 작업 대상 폴더의 `README.md`를 읽는다 (DFD + Agent Control 확인)
5. Agent Control **금지 규칙** 위반 여부 확인 후 코드 작성
6. 구조 변경 시 → 해당 레벨부터 루트까지 DFD 연쇄 업데이트

### 세션 종료 (갱신)

7. 루트 `README.md` **Progress Tracker** 업데이트 (🔄 시작, ✅ 완료)
8. 루트 `README.md` **Next Roadmap** 갱신
9. `AGENT_STATE.md`를 아래 순서로 갱신한다:

```
a. 누적 사용자 요구사항  → 이번 세션에서 처리한 새 요구사항 행 추가
b. 현재 작업 상태        → 루트 Tracker 내용과 동기화
c. 다음 할 일            → 루트 Roadmap 내용과 동기화
d. 핵심 규칙 스냅샷      → 새로 추가/변경된 규칙 반영
e. 세션 로그             → 오늘 날짜, 수행 작업, 변경 파일, 인계 사항 기록
                           (10개 초과 시 가장 오래된 행 삭제)
```

---

## §3. AGENT_STATE.md 갱신 상세 규칙

### 누적 사용자 요구사항 — 언제 추가하는가

- 사용자가 새로운 구조적 요청을 하고 이를 반영 완료했을 때
- 새로운 Agent Control 규칙이 추가되었을 때
- 폴더 구조가 변경되었을 때

> 사소한 버그 수정이나 단순 코드 변경은 추가하지 않습니다.  
> "이 프로젝트의 방향과 규칙에 영향을 주는 결정"만 기록합니다.

### Progress Snapshot — 동기화 기준

- 루트 `README.md` Tracker와 **항상 동일**해야 합니다
- 세션 종료 전 두 파일을 비교해 불일치가 없는지 확인합니다

### 세션 로그 — 기록 형식

```markdown
| 2026-05-18 | DFD 레벨링 적용, 폴더 소유권 모델 정의 | BLUEPRINT.md, templates/* | 하위 폴더 DFD 연쇄 업데이트 미완료 |
```

---

## §4. 절대 금지 행동

| 금지 행동 | 이유 |
|-----------|------|
| 매 세션 `BLUEPRINT.md` 전체 읽기 | 불필요한 토큰 낭비 |
| `AGENT_BOOTSTRAP.md` 삭제 없이 세션 종료 | 다음 세션이 중복 초기화 실행 |
| `AGENT_STATE.md` 미갱신 세션 종료 | 맥락 단절, 다음 세션이 처음부터 재파악 |
| `AGENT_STATE.md`에 코드 내용 기록 | 파일 비대화, 토큰 낭비 |
| 이미 처리된 요구사항 재처리 | 누적 사용자 요구사항 미확인에서 발생 |
| `Progress Snapshot`과 루트 Tracker 불일치 유지 | 맥락 오염 |

---

## §5. 커밋 메시지 규칙

```
<type>(<scope>): <description>
```

| Type | 사용 시점 |
|------|-----------|
| `feat` | 새 기능 추가 |
| `fix` | 버그 수정 |
| `docs` | 문서 수정 (README, DFD, AGENT_STATE 등) |
| `refactor` | 기능 변경 없는 구조 개선 |
| `chore` | 빌드, 의존성 등 기타 |

**AGENT_STATE.md 갱신은 기능 커밋에 포함하거나 `docs` 커밋으로 분리합니다.**

예: `feat(auth): add JWT refresh endpoint + update agent state`
