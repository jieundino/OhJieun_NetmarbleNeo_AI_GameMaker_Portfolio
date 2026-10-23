# Unity QA Companion — AI-Assisted QA Workflow & Tooling

> **Project:** Unity QA Companion  
> **Role:** Solo Developer (Workflow & Specification Design)  
> **Contribution:** QA 워크플로 설계, 데이터 스키마·검증 규칙 정의, AI 프롬프트 명세화 및 단계별 구현·검증  
> **Repository:** [GitHub — Unity-QA-Companion](https://github.com/jieundino/Unity-QA-Companion)  
> **Live Preview:** [Unity QA Companion (Vercel)](https://unity-qa-companion.vercel.app/)

> **Structured Prompt Specification · Defensive JSON Validation · Human-in-the-Loop QA Pipeline**

## 1. 문서 목적

본 문서는 Unity 게임 개발 과정에서 발생한 이슈(`Issues.md`)를 구조화된 테스트 케이스로 전환하고, Windows 빌드 수동 테스트 결과와 버그 리포트 작성까지 하나의 흐름으로 관리하기 위해 제작한 웹 애플리케이션 **Unity QA Companion**의 설계 의도와 AI 활용 방식을 정리합니다.

게임 클라이언트 런타임 코드(C#)와 달리, 개발·QA 생산성을 높이기 위한 보조 도구(Companion Tooling)를 구축할 때 **AI 개발 도구(Vibe Coding)와 생성형 AI 프롬프트 명세화를 어떻게 엔지니어링 통제 하에 활용했는지** 보여주는 데 목적이 있습니다.

---

## 2. 문제 정의

Unity 프로젝트(`<네 발자국>` 등)를 개발·출시하며 기능 검증과 런타임 이슈 수정을 반복하는 과정에서 다음과 같은 워크플로 병목이 있었습니다.

- 개발 중 기록한 Markdown 이슈 목록(`Issues.md`)은 문제 상황을 파악하기에는 좋지만, 실제 빌드 검증용 테스트 케이스(사전 조건, 재현 절차, 기대 결과)로 전환하려면 반복적인 수작업이 필요함
- 동일한 테스트 케이스를 여러 빌드 버전과 실행 환경(해상도, OS 환경)에서 반복 검증할 때 `PASS` / `FAIL` / `BLOCKED` 이력이 문서마다 분산되기 쉬움
- 외부 생성형 AI로 테스트 케이스 초안을 만들더라도, 출력 형식이 일정하지 않거나 필수 항목이 누락되면 바로 활용하기 어려움
- 실패한 테스트 결과를 다시 버그 리포트와 수정 요청 문서로 정리하는 과정에서 중복 작성 비용이 발생함

---

## 3. 요구사항 및 워크플로 분해

QA 진행 과정을 다음 6단계 파이프라인으로 분해하고, 각 단계의 데이터가 서로 참조 무결성을 유지하도록 설계했습니다.

```text
Issues.md Upload & Markdown Parsing
    ↓
Structured AI Prompt Generation (Issue Context + Output Schema)
    ↓
External AI Tool Execution & Response Paste
    ↓
Schema / Field Validation & Test Case Registration
    ↓
Manual Build Test Execution & Result Logging (PASS / FAIL / BLOCKED)
    ↓
Bug Report · Fix Request Draft · Markdown / CSV / JSON Export
```

| 단계 | 핵심 책임 | 엔지니어링 통제 포인트 |
| --- | --- | --- |
| Issue Parsing | `Issues.md` 업로드 및 구조화 파싱 | 원문과 파싱 결과 대조 검수, 잘못된 Markdown 입력 방어 |
| Prompt Generation | 선택 이슈 기반 테스트 케이스 생성용 프롬프트 조립 | 일관된 JSON 스키마로 출력되도록 프롬프트 규칙 명세화 |
| Response Validation | 외부 AI가 생성한 테스트 케이스 결과 붙여넣기 및 등록 | JSON 파싱 오류, 필수 필드 누락, 중복 항목 검수 후 등록 |
| Test Run Logging | Windows 게임 빌드 수동 실행 결과(`Not Run` / `PASS` / `FAIL` / `BLOCKED`) 기록 | 빌드 버전, 해상도, 실행 환경 및 반복 실행 이력 추적 |
| Bug Reporting | `FAIL` 실행 기록을 기반으로 버그 리포트 및 수정 요청 초안 생성 | 원본 이슈 ID · 테스트 케이스 ID · 실행 결과 간 연결 유지 |
| Backup & Export | 로컬 저장소 관리 및 Markdown / CSV / JSON 입출력 | JSON 전체 백업·복원 시 참조 무결성 및 스키마 검증 |

---

## 4. 핵심 설계 결정

### 4.1 Human-in-the-Loop 기반 AI 테스트 케이스 생성

외부 AI API를 클라이언트에 직접 연동하면 API 키 관리와 비용, 프로젝트 보안 정책 문제가 발생할 수 있습니다.

이를 피하기 위해 **앱이 이슈 맥락과 출력 스키마를 포함한 정교한 프롬프트를 생성**하고, 사용자가 외부 AI 도구의 응답을 붙여넣으면 **앱이 스키마를 검증한 뒤 검수 과정을 거쳐 등록**하는 Human-in-the-Loop 방식을 선택했습니다.

```text
Selected Issue Data
→ Prompt Template + Required JSON Schema 결합
→ 외부 AI 도구 실행 (사용자)
→ 응답 JSON 붙여넣기
→ 스키마·필수값 검증 및 사용자 검수
→ Test Case 확정 등록
```

### 4.2 비결정적 AI 출력에 대한 방어적 검증 (Defensive Validation)

생성형 AI의 응답이나 사용자가 수정한 Markdown/JSON 입력은 항상 정상 형식을 보장하지 않습니다.

- 잘못된 Markdown 구조 및 JSON 구문 오류 감지
- 필수 항목 누락 및 잘못된 ID 참조 차단과 사용자 안내
- 중복 데이터 등록 확인
- 백업 JSON 복원 시 데이터 구조 유효성 확인

### 4.3 `<네 발자국>` 실제 개발·QA 데이터 연동

추상적인 더미 데이터 대신, 직접 메인 클라이언트 프로그래머로 개발·출시한 **`<네 발자국 (Four Footsteps)>`의 이슈 및 QA 데이터**를 기본 샘플로 탑재했습니다.

별도의 JSON 파일을 준비하지 않아도 [Live Preview](https://unity-qa-companion.vercel.app/) 접속 즉시 실제 Unity 게임 개발 이슈가 어떻게 테스트 케이스와 실행 기록, 버그 리포트로 이어지는지 확인할 수 있습니다.

### 4.4 AI 보조 개발(Vibe Coding)에서의 단계별 명세와 검증

본 웹 애플리케이션은 AI 코딩 도구를 적극 활용해 구현하되, 다음과 같은 기준으로 엔지니어링 통제를 유지했습니다.

1. **기능 및 상태 명세 선행**: 코드를 생성하기 전에 이슈·테스트 케이스·실행 기록·버그 리포트 간의 데이터 관계와 상태 전이 규칙을 먼저 정의
2. **단계별 구현 및 통합 테스트**: 단일 프롬프트로 전체 앱을 생성하지 않고, 기능 단위로 분할 구현하며 단계마다 입출력 예외를 검증
3. **명확한 책임 경계 설정**: 실제 게임 빌드 실행 자동화나 메일 자동 발송처럼 MVP 범위를 벗어나는 기능은 제외하고, 로컬 저장 기반 QA 워크플로 완성도에 집중

---

## 5. 검증 항목

| 항목 | 확인 내용 |
| --- | --- |
| Markdown 파싱 | `Issues.md` 업로드 시 이슈 목록과 상세 내용이 정확히 분리되는가 |
| 프롬프트 생성 | 선택한 이슈 정보가 테스트 케이스 생성용 프롬프트 형식에 맞게 포함되는가 |
| AI 응답 검증 | 잘못된 JSON 형식이나 필수 필드 누락 시 오류 안내가 정상 동작하는가 |
| 실행 이력 추적 | 동일 테스트 케이스를 여러 빌드 버전에서 반복 실행할 때 이력이 보존되는가 |
| 리포트 연결성 | `FAIL` 결과에서 생성한 버그 리포트가 원본 이슈 및 테스트 케이스와 정확히 연결되는가 |
| 백업 및 복원 | JSON 전체 백업 후 복원했을 때 모든 데이터와 연결 관계가 동일하게 유지되는가 |

---

## 6. 구현 결과

- `<네 발자국>` 등 Unity 프로젝트의 `Issues.md` 문서에서 테스트 케이스 작성, 빌드 검증 기록, 버그 리포트 출력까지 이어지는 단일 QA 워크플로 도구를 완성했습니다.
- 백엔드 서버 없이 브라우저에서 즉시 동작하는 MVP와 단독 실행 파일(`UnityQACompanion-standalone.html`), [Vercel 웹 배포 환경](https://unity-qa-companion.vercel.app/)을 구축했습니다.
- AI를 단순 코드 생성기가 아니라 **구조화된 프롬프트 설계 + 스키마 검증 기반의 워크플로 구성 요소**로 활용하는 실무형 사례를 정리했습니다.

---

## 7. 한계 및 향후 개선 방향

- 브라우저 로컬 저장소 기반이므로 브라우저 데이터 초기화 시 손실 방지를 위해 수동 JSON 백업이 필요함
- 수동 테스트 결과 기록 도구이므로 Unity 빌드 실행이나 클라이언트 로그 수집이 자동으로 연결되어 있지 않음

### 개선 방향

- Unity `Player.log` 및 크래시 로그 파일을 업로드해 오류 스택 트레이스를 버그 리포트에 자동 첨부하는 기능
- 빌드 버전 간 회귀 테스트(Regression Test) 결과 비교 뷰 강화
- 테스트 증거 자료(스크린샷·영상 링크) 첨부 구조 확장
