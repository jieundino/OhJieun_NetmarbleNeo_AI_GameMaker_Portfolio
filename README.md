# 오지은 | AI Game Maker — 게임 개발·AI 협업 포트폴리오

**넷마블네오 2026 AI 인턴십 지원용 | Unity/C# · AI-assisted development · QA**

> [지원용 Notion 포트폴리오](https://rich-ulna-bb7.notion.site/AI-Game-Maker-Portfolio-2026-AI-41cdb6505b7c804dab74fba580f52a40) · [기존 코드 포트폴리오](https://github.com/jieundino/OhJieun_Game-Programmer_Source-Code-Portfolio)

## 우선 볼 프로젝트

| 우선순위 | 프로젝트 | 이 저장소에서 확인할 것 | 역할과 AI 사용 범위 |
| --- | --- | --- | --- |
| 1 | **Unity Skill Logic Prototype** (2026.07) | [스킬 실행 코드](./05_SourceCode/00_UnitySkillLogicPrototype/) · [기술 노트](./03_Technical_Notes/00_UnitySkillLogicPrototype_Architecture_Verification.md) · [시연](https://youtu.be/QM03HsZIwEM) | 인터넷 강의 학습 + **AI 에이전트 코드 생성·수정** + **본인 Unity QA 실행**. 개인 학습·제작 프로젝트. |
| 2 | **네 발자국** (제작·출시 2025.03–2026.02) | [이벤트·Save/Load·로그 코드](./05_SourceCode/02_FourFootsteps_DataDrivenSystems/) · [기술 노트](./03_Technical_Notes/04_FourFootsteps_SaveLoad_System.md) · [플레이 영상](https://youtu.be/013OU2ZJlbk) | 4인 공동개발. 메인 클라이언트 프로그래머 및 초기 콘셉트 기획. **논문 후속 연구는 2026.04까지 별도 진행**. |
| 3 | **필연과 우연** (2024.03–2026.01) | [행동력·퍼즐·SFX 코드](./05_SourceCode/01_Fate_RuntimeSystems/) · [런타임 이슈 기록](./04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md) · [플레이 영상](https://youtu.be/kjaH9fDRmMo) | 6인 공동개발. 클라이언트·시스템 개발, 출시·전시 QA 및 변경 의도 공유. |
| 4 | **Unity QA Companion** (2026) | [독립 저장소](https://github.com/jieundino/Unity-QA-Companion) · [실행 데모](https://unity-qa-companion.vercel.app/) · [QA 워크플로 문서](./03_Technical_Notes/06_UnityQACompanion_AI_Workflow.md) | AI 코딩 도구로 웹 구현을 보조받고, 이슈 → 테스트 케이스 → 검증 → 버그 리포트의 워크플로·데이터 규칙 설계. |
| 5 | **Hey Cheese!** (2025.03–2025.07) | [미니게임 코드](./05_SourceCode/03_HeyCheese_MinigamePrototypes/) · [기술 노트](./03_Technical_Notes/05_HeyCheese_Minigame_Logic.md) · [플레이 영상](https://youtu.be/4RVUEoXP8Yw) | 4인 공동개발. 4종 미니게임 클라이언트와 Android 파일럿 테스트. 얼굴·표정 인식은 본인 직접 구현 범위가 아님. |

> **프로젝트 코드의 소유·기여는 유형마다 다릅니다.** 특히 Unity Skill Logic Prototype은 개인 프로젝트지만 코드 생성·수정 과정에 AI 에이전트가 참여했습니다. `1인 프로젝트`가 `C# 코드 100% 직접 작성`을 뜻하지 않습니다. 상세 내용은 [AI 사용 기록](./docs/AI_ASSISTED_DEVELOPMENT.md)과 [프로젝트별 기여 범위](./01_Project_Contribution.md)에 있습니다.

## AI 활용 사례

**Unity Skill Logic Prototype — AI와 함께 게임 기능 구현**

인터넷 강의로 관련 개념을 학습한 후, 오류와 목표 동작을 AI 에이전트에 설명해 코드를 생성·수정했습니다. AI가 제안한 QA 목록에 따라 대상 없음, 사거리 초과, 쿨타임, DoT·Area, 다중 Collider, UI 상태를 **실제 Unity에서 직접 점검**했습니다. QA 항목 작성과 기술 문서 정리에도 AI의 도움을 받았습니다. AI 작성 코드 비율은 측정하지 않았습니다.

**Unity QA Companion — AI 활용을 위한 검증 워크플로 설계**

`Issues.md`를 테스트 케이스 생성 프롬프트로 변환하고, 외부 AI 응답의 JSON 구조·필수 값·참조 관계를 검증한 뒤 수동 빌드 테스트를 기록합니다. **AI가 생성한 테스트 케이스와 사람이 판단한 테스트 결과를 구분**합니다. 웹 구현에는 AI 코딩 도구의 도움을 받았습니다.

## 실제 게임 개발에서 해결한 문제

| 사례 | 원인·판단 | 검증할 코드·문서 |
| --- | --- | --- |
| 저장 실패와 데이터 복원 | 임시 파일 교체(Atomic Write), 백업, 역직렬화 예외 처리 | [네 발자국 Save/Load](./03_Technical_Notes/04_FourFootsteps_SaveLoad_System.md) |
| 행동력 중복 차감 | 반복 입력과 상태 전환 시점이 충돌하지 않도록 가드 | [필연과 우연 상태 흐름](./03_Technical_Notes/01_Fate_ActionPointManager.md) |
| 효과음 누락 | 유한한 `AudioSource`의 우선순위·예약 채널·반복 클릭 제어 | [SFX 채널 정책](./03_Technical_Notes/02_Fate_SFX_Priority_Channel.md) |
| 스킬 발동과 쿨타임 불일치 | 스킬 종류별 발동 성공 조건을 나누고 실패 요청의 상태 변화 차단 | [Skill Logic 검증](./03_Technical_Notes/00_UnitySkillLogicPrototype_Architecture_Verification.md) |

## 주요 산출물과 성과

- **필연과 우연:** STOVE·App Store 출시, 2025 BIC·Beaver Rocks 전시(팀 공동 성과).
- **네 발자국:** 2026.02 STOVE 출시. 2026.04까지 후속 연구 진행. 연구용 빌드에서 엔딩 로그를 수집했습니다. [관련 학술지 논문 (제1저자)](https://doi.org/10.22819/kscg.2026.39.4.002)
- **Hey Cheese!:** Android 테스트 빌드, 일반 초등학생 30명 파일럿 테스트, 관련 JCCT 논문 **제3저자**([DOI](https://doi.org/10.17703/JCCT.2025.11.6.321)). 정식 출시를 확인하지 않아 출시작으로 표시하지 않음.

실적의 근거와 한계는 [성과 증빙 안내](./docs/EVIDENCE_AND_SCOPE.md)에 기재했습니다. 30명 파일럿 결과는 실제 경계선 지능 아동의 학습 효과를 입증하는 자료가 아닙니다.

## 코드 검토 순서 및 저장소 안내

1. [프로젝트별 기여 범위](./01_Project_Contribution.md)에서 맡은 작업과 AI 코딩 도움을 확인합니다.
2. [스킬 시스템 코드](./05_SourceCode/00_UnitySkillLogicPrototype/)와 [기술 노트](./03_Technical_Notes/00_UnitySkillLogicPrototype_Architecture_Verification.md)를 비교합니다.
3. [네 발자국 코드](./05_SourceCode/02_FourFootsteps_DataDrivenSystems/)와 [필연과 우연 코드](./05_SourceCode/01_Fate_RuntimeSystems/)의 실제 개발 사례를 검토합니다.
4. [소스코드 인덱스](./02_SourceCode_Index.md) 및 [런타임 이슈](./04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md)를 참고합니다.

**범위:** 이 저장소는 게임 전체의 독립 실행 Unity 프로젝트가 아닙니다. 코드 리뷰를 위해 선별한 C# 소스, 일부 폴더별 설명, 기술 문서로 구성됩니다. 특정 기능은 원본 프로젝트의 Scene, Prefab, 데이터, 리소스, 매니저에 의존합니다. 코드가 존재한다고 해서 이 저장소만으로 게임 전체를 실행할 수 있다는 뜻은 아닙니다.
