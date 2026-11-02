# Changelog

이 파일은 Blueprint Framework 자체의 변경 이력입니다.  
버전은 [Semantic Versioning](https://semver.org/lang/ko/)을 따릅니다 — 템플릿 구조를 깨는 변경은 메이저, 기능 추가는 마이너, 문구 수정은 패치.

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
