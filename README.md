# Unity C# Game Programmer Source Code Portfolio

**오지은 | Unity C# Game Programmer**

Unity C# 기반 개인 기술 프로토타입과 팀 게임 프로젝트에서
직접 설계·구현·수정한 주요 소스코드를 선별한 포트폴리오입니다.

게임 기능을 단순히 동작시키는 데서 끝내지 않고,
**요구사항 → 데이터/상태 구조 → 조건 검증 → 실행 → 피드백**의 흐름으로 나누어 구현하고,
반복 입력, 상태 불일치, 저장 실패, 자원 충돌과 같은 런타임 문제를
재현·분석·수정·검증해 온 과정을 함께 정리했습니다.

공동 프로젝트는 지원자가 직접 작성하거나 수정한 코드만 선별했으며,
프로젝트별 역할, 기여 비중, 코드 소유 범위와 협업 경계는
[`01_Project_Contribution.md`](./01_Project_Contribution.md)에서 확인할 수 있습니다.

---

## Featured Projects

### 1. Unity C# Client Systems (본 Repository 수록 코드)

| 프로젝트 | 형태 / 역할 | 주요 기술 | 핵심 구현 및 문제 해결 |
| --- | --- | --- | --- |
| **Unity Skill Logic Prototype** | 개인 / Solo Developer | Unity, C#, ScriptableObject, Coroutine, Physics Query, UGUI | 스킬 설정 데이터와 Runtime State 분리, 실행 조건 검증, Normal·DoT·Area 실행 구조 |
| **&lt;필연과 우연&gt;** | 6인 / Client · System Programmer | Unity, C#, UI Event System, Coroutine, AudioSource | 퍼즐, 행동력·날짜 진행, SFX 우선순위 채널, 입력·상태 예외 대응 |
| **&lt;네 발자국&gt;** | 4인 / Main Client Programmer | Unity, C#, CSV, Dictionary, Newtonsoft.Json, UnityWebRequest | 데이터 기반 이벤트, Dialogue Queue, Save/Load 안정화, 로그 재시도 |
| **&lt;Hey Cheese!&gt;** | 4인 / Mini-game Client Programmer | Unity, C#, Touch Input, Coroutine, UGUI | 4종 미니게임, 모바일 입력·완료 조건, 사용자 테스트 |

### 2. AI-Assisted Game QA & Workflow Tooling (연계 워크플로 도구)

| 프로젝트 | 형태 / 역할 | 주요 기술 | 핵심 구현 및 문제 해결 | 바로가기 |
| --- | --- | --- | --- | --- |
| **Unity QA Companion** | 개인 / Workflow & Spec Designer | HTML/CSS/JS, Prompt Spec, JSON Schema Validation | `<네 발자국>`의 `Issues.md` 파싱 → AI 프롬프트 생성 및 응답 검증 → 빌드 수동 테스트 기록 → 버그 리포트 생성 | [Live Preview](https://unity-qa-companion.vercel.app/) · [GitHub](https://github.com/jieundino/Unity-QA-Companion) · [기술 노트](./03_Technical_Notes/06_UnityQACompanion_AI_Workflow.md) |

### 주요 결과

- **<필연과 우연>** — STOVE · App Store 출시, BIC · Beaver Rocks 전시
- **<네 발자국>** — STOVE 출시, 학술발표 및 학술지 논문 제1저자
- **<Hey Cheese!>** — 초등학생 30명 파일럿 테스트, JCCT 논문 제2저자
- **Unity Skill Logic Prototype** — 개인 설계·구현 및 정상·실패·경계 조건 검증
- **Unity QA Companion** — `<네 발자국>` 실데이터 기반 QA 워크플로 웹 도구 구축 및 배포

---

## Core Skills

### Game System Design

- 기능 요구사항을 데이터, Runtime State, Validation, Execution 단계로 분해
- 설정 데이터와 플레이 중 변경되는 상태를 분리해 관리
- 공통 실행 흐름과 콘텐츠별 예외 규칙 분리
- 기능 실행 성공 여부에 따라 후속 상태와 피드백을 적용

### Data & State Management

- CSV·ID 기반 데이터 중심 이벤트 구조
- `Dictionary`, `Queue`, `HashSet`을 목적에 맞게 활용
- Save/Load 데이터와 Runtime State의 일관성 관리
- 선택·이벤트·멀티엔딩 상태를 데이터와 연결

### Runtime Stability

- 반복 입력과 중복 실행 방어
- 저장·복원 과정의 상태 불일치 분석
- Coroutine 및 Scene 수명주기 관련 문제 확인
- 한정된 AudioSource 자원의 우선순위 배분
- 정상 조건뿐 아니라 실패·경계 조건을 포함한 검증

### AI-Assisted Development & Workflow Design

- **게임 런타임 코드(Unity/C#)**: AI를 설계 대안 비교·예외 케이스 점검 보조로 활용하되, 아키텍처 결정·코드 작성·런타임 검증은 직접 수행
- **개발·QA 보조 도구(`Unity QA Companion`)**: 단계별 기능·상태 명세를 바탕으로 AI 코딩 도구(Vibe Coding)를 통제하여 빠르게 워크플로 도구 구축
- 비결정적 AI 응답을 바로 신뢰하지 않고, 출력 JSON 스키마 명세화와 필수 필드·참조 무결성 방어 검증(Defensive Validation) 적용

### Documentation & Collaboration

- 문제 상황과 재현 조건을 구체화
- 원인, 수정 내용, 확인 결과를 문서로 기록
- 공동 프로젝트의 직접 구현 범위와 협업 경계를 명시
- 구조적 한계와 후속 개선 방향을 구분해 정리

---

## Recommended Review Order

코드 리뷰 시 아래 순서로 확인하면  
개인 프로토타입의 설계부터 실제 팀 프로젝트의 문제 해결 과정까지 빠르게 파악할 수 있습니다.

### 1. Unity Skill Logic Prototype

[`05_SourceCode/00_UnitySkillLogicPrototype/README.md`](./05_SourceCode/00_UnitySkillLogicPrototype/README.md)

개인 기술 프로토타입으로,  
스킬 명세를 다음 단계로 구조화했습니다.

```text
Skill Data
    ↓
Runtime State
    ↓
Validation
    ↓
Execution
    ↓
Feedback
```

주요 확인 포인트:

- ScriptableObject 설정 데이터와 슬롯별 Runtime 쿨타임 상태 분리
- 대상 탐색과 사거리 검증
- Normal / DoT / Area 스킬 실행
- 실행 성공 시에만 쿨타임 적용
- 사망 대상 제외
- 다중 Collider 대상의 중복 피해 방지
- DoT 재적용 처리
- Health / Cooldown UI와 Runtime 상태 연결

---

### 2. Source Code Index

[`02_SourceCode_Index.md`](./02_SourceCode_Index.md)

전체 코드 중 우선 검토할 파일과  
각 코드에서 확인할 수 있는 설계 포인트를 정리했습니다.

대표 검토 순서:

1. Skill Data / Runtime
2. Skill Activation Pipeline
3. Target / Status Handling
4. Combat Feedback
5. Event / Result Pipeline
6. Save Reliability
7. Log Retry
8. Action Point State Flow
9. SFX Channel Policy
10. Puzzle Validation
11. Mini-game Logic

---

### 3. Project Contribution & AI Usage Scope

[`01_Project_Contribution.md`](./01_Project_Contribution.md)

공동 프로젝트에서 실제 담당 범위를 명확히 하기 위해 다음 기준을 구분했습니다.

- 전체 프로젝트 기준 기여 비중
- 개발 파트 기준 기여 비중
- 제출 코드의 직접 작성·수정 범위
- 직접 담당 기능
- 협업 경계
- 제출 자료에서 제외한 영역

생성형 AI 및 AI 개발 도구를 활용한 프로젝트는  
AI가 담당한 범위와 지원자가 직접 판단·수정·검증한 범위를 해당 문서에 별도로 명시합니다.

---

### 4. AI-Assisted QA Workflow Tool (`Unity QA Companion`)

- **기술 노트:** [`03_Technical_Notes/06_UnityQACompanion_AI_Workflow.md`](./03_Technical_Notes/06_UnityQACompanion_AI_Workflow.md)
- **Live Preview (Vercel):** [https://unity-qa-companion.vercel.app/](https://unity-qa-companion.vercel.app/) (`<네 발자국>` 데모 데이터 기본 탑재)
- **GitHub Repository:** [https://github.com/jieundino/Unity-QA-Companion](https://github.com/jieundino/Unity-QA-Companion)

Unity 게임 개발 중 기록한 `Issues.md` 문서를 체계적인 테스트 케이스로 전환하고, Windows 빌드 수동 검증 결과와 버그 리포트를 한곳에서 추적하기 위해 제작한 보조 웹 애플리케이션입니다.

```text
Issues.md Parsing
    ↓
Structured AI Prompt Generation
    ↓
External AI Response & Schema Validation
    ↓
Manual Build Test Logging (PASS / FAIL / BLOCKED)
    ↓
Bug Report & Fix Request Export
```

---

## Representative Problem Solving

### 1. SFX 채널 포화로 핵심 효과음이 누락되는 문제  
**<필연과 우연>**

빠른 반복 클릭과 이벤트 효과음이 동시에 요청될 때  
낮은 중요도의 반복음이 한정된 `AudioSource` 채널을 점유해  
핵심 연출음이 재생되지 않는 문제가 발생했습니다.

```text
Repeated SFX Requests
        ↓
AudioSource Channel Saturation
        ↓
Priority Classification
        ↓
Reserved Channels
        ↓
Voice Stealing + Debounce
        ↓
Regression Verification
```

적용한 방식:

- Low / High 두 단계의 SFX 우선순위
- 중요 SFX를 위한 예약 채널
- 높은 우선순위 요청의 Voice Stealing
- 반복 클릭 요청 Debounce
- Round-robin 방식의 채널 분산

관련 문서:

- [`03_Technical_Notes/02_Fate_SFX_Priority_Channel.md`](./03_Technical_Notes/02_Fate_SFX_Priority_Channel.md)
- [`04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md`](./04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md)

---

### 2. Save/Load 데이터 손상과 복원 실패  
**<네 발자국>**

저장 과정의 실패나 일부 데이터의 역직렬화 오류가  
전체 게임 진행을 복구할 수 없는 상황으로 이어지지 않도록  
저장 안정성을 개선했습니다.

주요 구현:

- 임시 파일 작성 후 교체하는 Atomic Write
- 기존 저장본 `.bak` 백업
- 복합 타입 전용 직렬화
- 손상 데이터 fallback
- 저장 후 Runtime State와 View 상태 동기화

관련 문서:

- [`03_Technical_Notes/04_FourFootsteps_SaveLoad_System.md`](./03_Technical_Notes/04_FourFootsteps_SaveLoad_System.md)

---

### 3. 행동력 시스템의 공통 흐름과 Room별 규칙 분리  
**<필연과 우연>**

스테이지마다 행동력 규칙이 달라지면서  
하나의 클래스에 조건문을 계속 추가하는 방식의 유지보수성이 낮아졌습니다.

공통적인

```text
Action Point Update
→ UI Update
→ Date Check
→ Transition
```

흐름은 상위 구조에서 관리하고,  
Room별 특수 규칙은 하위 클래스에서 처리하도록 분리했습니다.

관련 문서:

- [`03_Technical_Notes/01_Fate_ActionPointManager.md`](./03_Technical_Notes/01_Fate_ActionPointManager.md)

---

## Source Code Structure

```text
README.md
01_Project_Contribution.md
02_SourceCode_Index.md

03_Technical_Notes/
├─ 00_UnitySkillLogicPrototype_Architecture_Verification.md
├─ 01_Fate_ActionPointManager.md
├─ 02_Fate_SFX_Priority_Channel.md
├─ 03_FourFootsteps_CSV_Event_System.md
├─ 04_FourFootsteps_SaveLoad_System.md
├─ 05_HeyCheese_Minigame_Logic.md
└─ 06_UnityQACompanion_AI_Workflow.md

04_Runtime_Issue_Analysis/
└─ Runtime_Issue_Analysis.md

05_SourceCode/
├─ 00_UnitySkillLogicPrototype/
│  ├─ SkillDataRuntimeSystem/
│  ├─ SkillExecutionSystem/
│  ├─ CombatFeedbackSystem/
│  └─ PlayerControlSystem/
│
├─ 01_Fate_RuntimeSystems/
├─ 02_FourFootsteps_DataDrivenSystems/
└─ 03_HeyCheese_MinigamePrototypes/
```

---

## Code Ownership & Scope

### Unity Skill Logic Prototype

개인 기술 프로토타입으로,  
요구사항 정의, 구조 설계, 코드 작성·수정 및 실행 검증을 직접 수행했습니다.

생성형 AI를 활용한 부분은  
설계 대안 비교, API 및 구현 방식 검토, 디버깅과 테스트 케이스 점검 등  
개발 보조 범위로 구분하고,  
최종 구조 선택과 코드 통합, 예외 조건 정의 및 실행 결과 검증은 직접 수행했습니다.

구체적인 AI 활용 범위는  
[`01_Project_Contribution.md`](./01_Project_Contribution.md)에 명시했습니다.

### Team Projects

공동 프로젝트 폴더에는 지원자가 직접 작성하거나 직접 수정한 코드만 선별했습니다.

일부 코드는 원본 Unity 프로젝트의 다음 요소에 의존합니다.

- Scene
- Prefab
- 다른 Manager
- CSV / 콘텐츠 데이터
- 외부 패키지

따라서 본 Repository는 전체 Unity 프로젝트의 독립 실행본이 아니라  
**지원자의 주요 구현과 문제 해결 과정을 확인하기 위한 코드 리뷰용 포트폴리오**입니다.

### AI-Assisted QA Workflow Tool (`Unity QA Companion`)

`05_SourceCode/` 내 Unity C# 클라이언트 코드의 성격과 명확히 구분하기 위해,  
AI 코딩 도구(Vibe Coding)를 활용해 제작한 웹 기반 QA 보조 도구는 [별도 Repository](https://github.com/jieundino/Unity-QA-Companion)로 분리하고  
본 포트폴리오에는 워크플로 설계·프롬프트 명세·스키마 검증 구조를 정리한 [기술 노트](./03_Technical_Notes/06_UnityQACompanion_AI_Workflow.md)를 수록했습니다.

---

## Runtime Issue Analysis

[`04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md`](./04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md)

개발·출시·전시·사용자 테스트 중 실제 발생한 런타임 이슈를 다음 기준으로 정리했습니다.

```text
Impact
→ Reproduction
→ Observation
→ Root Cause
→ Fix
→ Verification
→ Follow-up
```

대표 사례:

- 행동력 연속 입력에 따른 중복 차감
- 퍼즐 오브젝트의 잘못된 DropZone 배치
- 핵심 효과음 누락
- Dialogue / Event 실행 순서 충돌
- Save/Load 직렬화 오류
- 저장 상태와 UI 상태 불일치
- BGM 전환 중 오디오 자원 누적

`Follow-up` 항목은 현재 구현된 기능과 혼동되지 않도록  
추후 리팩터링 또는 테스트 개선 시 검토할 방향으로 구분했습니다.
