# 오지은 | AI Game Maker — 게임 개발·AI 협업 포트폴리오

**넷마블네오 2026 AI 인턴십 지원용 | Unity/C# · AI 보조 개발 · QA**

> [지원용 Notion 포트폴리오](https://rich-ulna-bb7.notion.site/AI-Game-Maker-Portfolio-2026-AI-41cdb6505b7c804dab74fba580f52a40) · [기존 코드 포트폴리오](https://github.com/jieundino/OhJieun_Game-Programmer_Source-Code-Portfolio)

## 우선 볼 프로젝트

| 순서 | 프로젝트 | 코드·기술 문서·영상 | 담당 작업 |
| --- | --- | --- | --- |
| 1 | **Unity Skill Logic Prototype** (2026.07) | [스킬 실행 코드](./05_SourceCode/00_UnitySkillLogicPrototype/) · [기술 노트](./03_Technical_Notes/00_UnitySkillLogicPrototype_Architecture_Verification.md) · [시연](https://youtu.be/QM03HsZIwEM) | 인터넷 강의로 스킬 구조를 학습하고 AI 에이전트의 도움으로 코드를 생성·수정했습니다. Unity에서 직접 검증했습니다. |
| 2 | **네 발자국** (제작·출시 2025.03–2026.02) | [이벤트·Save/Load·로그 코드](./05_SourceCode/02_FourFootsteps_DataDrivenSystems/) · [기술 노트](./03_Technical_Notes/04_FourFootsteps_SaveLoad_System.md) · [플레이 영상](https://youtu.be/013OU2ZJlbk) | 4인 공동개발. 메인 클라이언트 프로그래머 및 초기 콘셉트 기획. **논문 후속 연구는 2026.04까지 별도 진행**. |
| 3 | **필연과 우연** (2024.03–2026.01) | [행동력·퍼즐·SFX 코드](./05_SourceCode/01_Fate_RuntimeSystems/) · [런타임 이슈 기록](./04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md) · [플레이 영상](https://youtu.be/kjaH9fDRmMo) | 6인 공동개발. 클라이언트·시스템 개발, 출시·전시 QA 및 변경 의도 공유. |
| 4 | **Unity QA Companion** (2026) | [독립 저장소](https://github.com/jieundino/Unity-QA-Companion) · [실행 데모](https://unity-qa-companion.vercel.app/) · [QA 워크플로 문서](./03_Technical_Notes/06_UnityQACompanion_AI_Workflow.md) | AI 코딩 도구로 웹 구현을 보조받고, 이슈 → 테스트 케이스 → 검증 → 버그 리포트의 워크플로·데이터 규칙 설계. |
| 5 | **Hey Cheese!** (2025.03–2025.07) | [미니게임 코드](./05_SourceCode/03_HeyCheese_MinigamePrototypes/) · [기술 노트](./03_Technical_Notes/05_HeyCheese_Minigame_Logic.md) · [플레이 영상](https://youtu.be/4RVUEoXP8Yw) | 4인 공동개발. 미니게임 4종의 클라이언트 개발과 Android 파일럿 테스트를 맡았습니다. |

코드 생성·수정에 AI를 활용한 과정과 직접 수행한 테스트는 [AI 협업과 기능 검증](./docs/AI_ASSISTED_DEVELOPMENT.md)에 정리했습니다.

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
- **Hey Cheese!:** Android 테스트 빌드, 일반 초등학생 30명 파일럿 테스트, 관련 JCCT 논문 **제3저자**([DOI](https://doi.org/10.17703/JCCT.2025.11.6.321)).

파일럿 테스트에서는 일반 초등학생의 조작성과 후속 검증 항목을 살폈습니다. 출시 페이지와 논문은 [프로젝트 성과 및 참고 자료](./docs/EVIDENCE_AND_SCOPE.md)에서 확인할 수 있습니다.

## 코드 검토 순서 및 저장소 안내

1. [프로젝트별 기여 범위](./01_Project_Contribution.md)에서 맡은 작업과 AI 코딩 도움을 확인합니다.
2. [스킬 시스템 코드](./05_SourceCode/00_UnitySkillLogicPrototype/)와 [기술 노트](./03_Technical_Notes/00_UnitySkillLogicPrototype_Architecture_Verification.md)를 비교합니다.
3. [네 발자국 코드](./05_SourceCode/02_FourFootsteps_DataDrivenSystems/)와 [필연과 우연 코드](./05_SourceCode/01_Fate_RuntimeSystems/)의 실제 개발 사례를 검토합니다.
4. [소스코드 인덱스](./02_SourceCode_Index.md) 및 [런타임 이슈](./04_Runtime_Issue_Analysis/Runtime_Issue_Analysis.md)를 참고합니다.

이 저장소에는 검토용 C# 소스와 기술 문서를 담았습니다. Unity에서 실행하려면 원본 프로젝트의 Scene, Prefab, 데이터와 리소스가 필요합니다.
