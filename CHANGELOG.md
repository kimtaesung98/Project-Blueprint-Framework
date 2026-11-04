# Changelog

이 파일은 Blueprint Framework 자체의 변경 이력입니다.  
버전은 [Semantic Versioning](https://semver.org/lang/ko/)을 따릅니다 — 템플릿 구조를 깨는 변경은 메이저, 기능 추가는 마이너, 문구 수정은 패치.

---

## [2.1.0] — 2026-11-04

### Added
- **ARCHITECTURE 층**: `templates/ARCHITECTURE_TEMPLATE.md` 추가. 기술 스택(버전·상태·근거 ADR), 허용 라이브러리 목록, 구성도, 모듈 맵·의존 규칙, 내부 인터페이스, 런타임 시나리오, 배포·환경변수, 횡단 관심사, 품질 속성 대응, ADR, 진화 계획, 기술 부채
- 파일 머리에 "이런 작업을 할 때 → 읽을 절" 표 — 에이전트가 세션마다 전체를 읽지 않도록
- ADR 상태(제안/승인/대체됨/폐기)와 "에이전트는 제안만" 규칙
- `FIRST_PROMPTS.md` "ARCHITECTURE.md 함께 작성하기", `MIGRATION_GUIDE.md` Step 1-4(의존성·import 역공학)
- `FOLDER_CHECKLIST.md` 6번째 검증 질문 (import 가능한 모듈·라이브러리)

### Changed
- 정보 소유 규칙을 네 층으로 확장: 명세(SPEC) · **구조(ARCHITECTURE)** · 진행(Tracker) · 흐름(폴더 README)
- **ADR을 SPEC.md §8 → ARCHITECTURE.md §9로 이동**. SPEC §8은 절 번호 유지를 위해 링크만 남김
- 루트 README Tech Stack은 **이름만 적은 요약 + 링크** (버전은 ARCHITECTURE.md §2.1에만)
- 폴더 README Tech Stack은 ARCHITECTURE.md §2.2 허용 목록 안에서만
- `BLUEPRINT.md` §2를 "명세 문서 규칙"으로 바꾸고 §2-1 SPEC, §2-2 ARCHITECTURE로 나눔 (다른 절 번호는 유지)
- CLAUDE.md·CONTRIBUTING·BOOTSTRAP 세션 프로토콜에 ARCHITECTURE 확인 단계 추가 (CONTRIBUTING §2 작업 중 단계 번호가 하나씩 밀림)
- 새 외부 의존성 연쇄 업데이트 규칙에 ARCHITECTURE.md §2.1 · §3.1 추가

### 기존 프로젝트 업그레이드
1. `templates/ARCHITECTURE_TEMPLATE.md`를 루트 `ARCHITECTURE.md`로 복사
2. SPEC.md §8 ADR 표를 ARCHITECTURE.md §9로 옮기고, 각 ADR에 상태 열 추가 (기존 것은 "승인")
3. 루트 README Tech Stack의 버전·이유를 ARCHITECTURE.md §2.1로 옮기고 README에는 이름 + 링크만
4. `CLAUDE.md`에 "구조" 규칙 블록 추가 (`templates/CLAUDE_TEMPLATE.md` 참고)

---

## [2.0.0] — 2026-11-02

### Added
- **SPEC 층**: `templates/SPEC_TEMPLATE.md` 추가. 기능 ID(F-001)·사용자 스토리·수용 기준을 정의하고, 루트 README Tracker·폴더 README와 기능 ID로 연결
- Progress Tracker에 `ID` 열 추가. `✅ Done`의 기준을 "SPEC.md 수용 기준 전부 통과"로 정의
- `FIRST_PROMPTS.md`에 "SPEC.md 함께 작성하기" 프롬프트 추가
- `MIGRATION_GUIDE.md`에 SPEC.md 최소 작성 단계(Step 1-3) 추가
- `CLAUDE_TEMPLATE.md`에 "이 프로젝트 전용 규칙" 섹션 추가
- 이 `CHANGELOG.md`

### Changed (Breaking)
- **DFD 레벨 정의를 "분해 깊이"로 통일**: 레벨 = 상위 README의 레벨 + 1. README가 없는 중간 폴더는 레벨을 소비하지 않음. 기존 문서에서 "폴더 깊이 = 레벨" 규칙과 예시(`/src/auth` = Level 1)가 서로 모순되던 문제 해결
- **AGENT_STATE.md의 Progress Snapshot을 Current Focus(최대 3개)로 교체**: 전체 Tracker 복사를 없애 두 표가 어긋나는 문제 제거
- `AGENT_BOOTSTRAP.md` §5의 내장 AGENT_STATE 템플릿 제거 → `templates/AGENT_STATE.md`를 복사하도록 변경 (두 벌이 이미 달라져 있던 문제 해결)
- `BLUEPRINT.md` 절 번호 변경: §2 SPEC 규칙 신설로 이후 절이 하나씩 밀림 (§3-1 → §4-1 등)
- `mvp_agent_spec.md` → `templates/AGENT_SESSION_GUIDE.md`로 이동·재작성. 시간이 지나면 틀려지는 요금제·모델별 수치를 제거하고 프레임워크 문서와 연결

### Fixed
- README 빠른 시작이 폐기된 `README_TEMPLATE.md`를 안내하던 문제
- README·BLUEPRINT·templates/README의 구조도와 DFD에 빠져 있던 파일 반영
- `templates/README.md`가 하위 폴더인데 자기 Progress Tracker를 갱신하라고 하던 모순, 폐기 템플릿 기준 금지 규칙
- `MIGRATION_GUIDE.md`가 CONTRIBUTING에 없는 규칙을 인용하던 문제 → CONTRIBUTING §2에 "README 없는 폴더는 작업 시 생성" 규칙 실제로 추가
- `CLAUDE_TEMPLATE.md`의 "모든 폴더에 README 필수"가 점진 적용 원칙과 충돌하던 문제
- `BLUEPRINT.md` 적용 예시에서 코드 블록 중첩으로 GitHub 렌더링이 깨지던 문제 (바깥 펜스를 백틱 4개로)
- mermaid 라벨 줄바꿈 `\n` → `<br>` (렌더러 호환성)
- 플레이스홀더 표기를 `[[ ]]`로 통일
- HTTP 상태 코드 참조 RFC 7231 → RFC 9110 (7231은 2022년 폐기)

---

## [1.x] — 2026-05 ~ 2026-10

- DFD 레벨링, 폴더 소유권 모델(TOP/SUB), AGENT_BOOTSTRAP/STATE 세션 관리, 드리프트 감지, 팀 협업 규칙 도입
