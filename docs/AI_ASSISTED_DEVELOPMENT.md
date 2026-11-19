# AI 협업과 기능 검증

## Unity Skill Logic Prototype (2026.07)

인터넷 강의에서 배운 Unity 전투 스킬 구조를 바탕으로 Normal·DoT·Area 스킬을 다루는 개인 프로토타입을 만들었습니다. 기대 동작과 오류 상황을 AI 에이전트에 설명해 코드 생성·수정을 요청했고, 제안받은 코드를 Unity 프로젝트에 적용했습니다.

AI가 작성한 QA 목록 초안에서 점검할 항목을 골라 Unity에서 직접 실행했습니다. 대상이 없거나 사거리 밖에 있을 때의 처리, 쿨타임 중 재사용, 사망 대상 제외, 여러 Collider를 가진 적의 중복 피해, DoT·Area 동작과 UI 상태를 확인했습니다. 기대와 다른 동작이 나오면 수정안을 요청한 뒤 같은 조건에서 다시 실행했습니다. 기술 문서와 검증 기록을 정리할 때도 AI의 도움을 받았습니다.

[스킬 시스템 구조와 기능 검증](../03_Technical_Notes/00_UnitySkillLogicPrototype_Architecture_Verification.md)

## Unity QA Companion (2026)

Unity 프로젝트에서 기록한 이슈를 테스트 케이스, 빌드 실행 기록, 버그 리포트로 이어서 관리하는 웹 도구를 만들었습니다. 이슈와 테스트 기록 사이의 데이터 관계, 필수 필드와 예외 처리 기준을 설계하고 웹 코드 생성·수정에는 AI 코딩 도구를 사용했습니다.

도구는 `Issues.md`에서 선택한 이슈를 테스트 케이스 생성용 프롬프트로 바꿉니다. 외부 AI의 응답을 붙여넣으면 JSON 형식, 필수 필드, 참조 관계를 검사합니다. 사용자는 초안을 검토해 등록한 뒤 실제 빌드를 실행하고 `PASS`, `FAIL`, `BLOCKED`를 직접 판정해 기록합니다.

[QA 워크플로와 검증 규칙](../03_Technical_Notes/06_UnityQACompanion_AI_Workflow.md) · [실행 데모](https://unity-qa-companion.vercel.app/)

[팀 프로젝트에서 맡은 작업](../01_Project_Contribution.md)
