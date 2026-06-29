# 콘텐츠 작성 가이드 — 직무별 분기 SSOT

> 본 파일은 `content/resume/{role}/`·`content/portfolio/{role}/` 작성·수정 시 참조하는 직무별 SSOT입니다.
> 상위 규칙은 `../CLAUDE.md` (공통 원칙·작성 수준·포트폴리오 헤더 형식). 본 파일은 그 위에 **직무별 강조·노출·금지**를 더합니다.
> 충돌 시: `../CLAUDE.md` 공통 원칙이 우선, 본 파일이 직무 분기 규칙 우선.

## 1. 참조 자료 (외부 vault, 반드시 확인 후 작성)

직무별 자격요건·우대사항·빈도 분석·사용자 자산 매칭은 vault 안에서 단일 진실 원천으로 관리합니다. 콘텐츠 분기·재작성 전 다음을 먼저 읽습니다.

| 자료 | 위치 | 용도 |
|------|------|------|
| 직무별 자격·우대 모음 (zighang 30건 표본) | `~/obsidian/Dev/취업/이력서_포폴/jd-analysis/requirements/{role}.md` | 직무 빈출 자격요건·우대사항 인용 근거 |
| 직무별 빈도 분석 | `~/obsidian/Dev/취업/이력서_포폴/jd-analysis/0{1-4}-{role}.md` | 키워드 빈도(Top 5)·회사 분포·경력 분포 |
| 사용자 자산 매칭 매트릭스 | `~/obsidian/Dev/취업/이력서_포폴/jd-analysis/matrix.md` | 4 프로젝트 × 4 직무 적합도·Gap·코드 매칭 근거 |
| 직무별 업그레이드 가이드 | `~/obsidian/Dev/취업/이력서_포폴/jd-analysis/upgrade-guide/{role}.md` | 직무 자격 강화용 mindgraph 업그레이드 후보 (현재 미구현 항목, 본문에 쓰지 말 것) |

작성 원칙:

- 새 직무 콘텐츠를 만들거나 강조점을 바꿀 때, 먼저 `requirements/{role}.md`에서 빈출 자격·우대 5건을 추려 메모합니다.
- 본문에 쓰는 키워드는 `requirements/{role}.md` 또는 `matrix.md §4 키워드 매칭 표`에 등장한 것만 허용. 이 두 곳에 없으면 사용자 코드 근거가 없는 키워드로 간주합니다.
- 업그레이드 가이드(`upgrade-guide/{role}.md`)의 항목은 "앞으로 할 일" 목록입니다. mindgraph 코드에 아직 없는 기능이므로 본문에 쓰지 않습니다.

## 2. 직무별 적합도 매트릭스 (`matrix.md` 요약)

| 프로젝트 | FDE | Product-Engineer | AI-Native-Builder | FE |
|----------|-----|------------------|-------------------|-----|
| mindgraph | ◎ | ◎ | ◎◎ | ◎ |
| chatGraph | △ | ◎ | △ | ◎ |
| Fit | × | ○ | × | ◎ |
| xAB | × | ○ | × | ◎ |

표기: ◎◎ = 직무 시그니처 자산과 1:1 대응 / ◎ = 다수 키워드 직접 매칭 / ○ = 부분 매칭 / △ = 단편적 매칭 / × = 매칭 없음

직무별 노출 프로젝트 (`pdf.config.json` 기준):

- **FDE**: mindgraph + chatGraph (2 프로젝트)
- **Product-Engineer**: 4 프로젝트 모두
- **AI-Native-Builder**: mindgraph + chatGraph (2 프로젝트, chatGraph는 △ 등급이나 최소 2개 노출 규정 충족)
- **FE**: 4 프로젝트 모두

× 등급 프로젝트는 해당 직무 노출에서 제외합니다. △ 등급은 노출하되 직무 시각으로 어순을 조정합니다.

## 3. 직무별 강조 키워드·어순 가이드

각 직무 본문 작성 시 다음 키워드를 어순 앞쪽에 배치합니다. 키워드는 `requirements/{role}.md` Top 5와 `matrix.md §4`에서 도출.

### FDE (Forward Deployed Engineer)

**zighang 자격 Top 6** (`requirements/FDE.md` — Forward Deployed + AI 솔루션 + Customer Engineer 합본 104건):

1. 영어·한국어 유창성 (customer-facing, local stakeholder 소통)
2. 클라우드·온프레미스·가상화·컨테이너 엔지니어링 경험
3. 프로그래밍·디버깅·시스템 디자인·프로토타이핑·데모·고객 워크숍 경험
4. 기술 스테이크홀더·임원 대상 발표·소통 경험
5. 프로덕션 코드를 직접 작성하고 운영해 본 경험
6. 협업·소통 능력

**강조 어순**: 1인 LLM 솔루션 프로토타입(출시 전) → 출시 후 응대 인프라 사전 구축 → 4 LLM 통합 신뢰도 → 프로토타이핑·데모 → 프로덕션 운영 안정성

**사용자 매칭 자산**:

- mindgraph 1인 LLM 솔루션 프로토타입 (getmindgraph.com 도메인 등록 후 출시 전) → ◎
- Claude Code 9훅·3 phase sprint·4중 SSOT AI 운영 자산 → ◎
- 4 LLM 서비스 통합 (detector.ts) → ◎
- 출시 후 응대 인프라 사전 구축 (PostHog·Sentry·OpenTelemetry·api/feedback·api/error-log 5개 채널) → ◎
- 부서·에이전트 분리 + RULES/context-map.md + SYSTEM/schemas/code-doc-mapping.yaml 자동 라우팅 → ◎
- chatGraph LLM 응답 통합 클라이언트 → △

**본문에 쓰지 않는 것**:

- "영어 native·fluent" — 사용자 확인 필요 (Anthropic·Google 글로벌 공고 다수라 강조 표현 등장하지만 사용자 영어 수준은 별도 확인)
- "Bachelor's degree·CS 학위" — 글로벌 공고 빈출이나 본문에 명시 불필요
- "엔터프라이즈 고객·B2B AX" — 외부 고객사 사례 없음
- 음성 AI·SIP·VoIP·텔레포니 — mindgraph 도메인과 거리 멀음

### Product-Engineer

**zighang 자격 Top 6** (`requirements/Product-Engineer.md` — Product Engineer + Product Builder + 프로덕트 엔지니어 합본 78건):

1. 코드부터가 아니라 정의부터 시작하는 문제 정의 우선 사고
2. 직접 만들고 검증하는 빌더 정신
3. 주도적 오너십 (복잡한 문제 해결을 주도, 제품 개발 사이클을 이끌어)
4. 좋은 설계와 나쁜 설계를 자기 기준으로 판단
5. "무엇을 할지 / 무엇을 버릴지" 판단 (제한된 시간)
6. 작은 팀에서 끝까지 책임지고 마무리한 경험 + 풀스택 엔지니어 지향

**강조 어순**: 1인 PO·문제 정의 → 직접 만들고 검증 → AI 워크플로우 자산 → 풀스택 라이프사이클 → 정량 검증

**사용자 매칭 자산**:

- mindgraph 1인 PO·출시 전 프로토타입·문제 정의-구현-검증 사이클 → ◎
- Claude Code 9훅·3 phase sprint·4중 SSOT AI 워크플로우 자산 → ◎ (PE 시그니처)
- 출시 후 가설 검증 인프라 사전 구축 (PostHog·Sentry·OpenTelemetry·api/feedback 4채널) → ◎
- 부서·에이전트 분리 + context-map 자동 라우팅 → ◎
- chatGraph Optimistic·useSuspenseQuery 사용자 흐름 → ◎
- Fit·xAB 풀스택 라이프사이클 → ○

**본문에 쓰지 않는 것**:

- 임베딩 추천(auto-link)·H1/H3 정량 측정(telemetry)·풀텍스트+임베딩 통합 검색 — mindgraph 코드 미구현 (2026-06-03 확인)
- "GraphQL·Temporal" 같은 회사별 스택 — 사용자 확인 필요
- "YoY 3배 성장·5개 프로덕트" — 정량 근거 없음

### AI-Native-Builder

**zighang 자격 Top 6** (`requirements/AI-Native-Builder.md` — ai native + builder 합본 74건. 이전 LLM Engineer 표본 대체):

1. **컨텍스트 엔지니어링·하네스 엔지니어링·에이전트 환경 설계** (사용자 자산과 정확 매칭)
2. 직접 만들고 검증
3. 빠른 의사결정·실행
4. "무엇을 할지 / 무엇을 버릴지" 판단
5. 영역 무관 1년 이상의 치열한 업무 경험
6. (우대) 자기 힘으로 높은 허들을 넘어 본 경험·세상을 변화시킨 경험 (Antler·Amazon 어조)

**강조 어순**: 컨텍스트 엔지니어링·하네스 → 4 LLM 통합 표면 → 임베딩 추천·정량 측정 → AI 운영 자산 → 빠른 검증·릴리즈

**사용자 매칭 자산**:

- Claude Code 위 5층 컨텍스트 영속화·9훅·3 phase sprint → ◎◎ (컨텍스트 엔지니어링·하네스 엔지니어링 시그니처)
- 부서·에이전트 분리(7부서·9에이전트) + context-map 자동 라우팅(RULES/context-map.md + SYSTEM/schemas/code-doc-mapping.yaml) → ◎◎ (에이전트 환경 설계 시그니처)
- 4 LLM 서비스 통합 표면 (detector.ts SELECTORS) → ◎
- 1인 출시 전 프로토타입 (getmindgraph.com 도메인 등록 후 출시 전) → ◎

**본문에 쓰지 않는 것**:

- 임베딩 추천(auto-link)·H1/H3 정량 측정(telemetry)·풀텍스트+임베딩 통합 검색 — mindgraph 코드 미구현 (2026-06-03 확인). 향후 업그레이드 후보는 `~/obsidian/Dev/취업/이력서_포폴/jd-analysis/upgrade-guide/AI-Native-Builder.md` Gap·§3에 둠.
- "PyTorch·TensorFlow 모델 학습" — 사용자 코드 없음
- "Custom Backbone·LLM 파인튜닝" — 사용자 코드 없음
- "Vector DB(Faiss·Milvus·Weaviate)" — pgvector만 사용
- "Langfuse·Vellum" — 사용자 코드 없음
- "Top-tier 학회 논문·Top-tier AI 학회" — 사용자에게 없음
- "용병 아닌 선교사" 같은 외부 인용은 본문에 직접 쓰지 말 것. 자산 매핑이 아닌 culture-fit 표현임

### FE (Frontend Engineer)

**zighang 자격 Top 6** (`requirements/FE.md` — depthTwos=프론트엔드 + keyword=frontend 합본 93건):

1. HTML5·CSS3·JavaScript(ES6+) 깊은 이해 및 내부 동작 원리
2. Git 활용 협업 및 코드 리뷰 프로세스
3. TypeScript 정적 타입 기반 견고한 코드 작성
4. 빌드 도구 (ESBuild·Vite·Webpack·SWC·Babel) 이해
5. 반응형 웹·크로스 브라우저·웹 접근성·웹 표준
6. 테스트·배포 자동화·프로젝트 리딩 경험

**강조 어순**: HTML/CSS/JS 내부 동작 → React·Next.js App Router → Vite·빌드 설정 결정 → SSR/RSC 경계 → 테스트·접근성 → 프로젝트 책임

**사용자 매칭 자산**:

- 4 프로젝트 모두 React+TypeScript+Next.js → ◎
- mindgraph D3+SSR 격리·Force 시뮬레이션·Tiptap 통합·[locale] 다국어·MV3 브리지 → ◎
- chatGraph useSuspenseQuery·Optimistic 라우팅·D3 cleanup → ◎
- Fit WebRTC·STOMP·useRef 큐 → ◎
- xAB App Router 병렬·인터셉팅 라우트·Realtime → ◎

**본문에 쓰지 않는 것**:

- "마이크로프론트엔드" — 적용 안 함
- "Storybook·visual regression" — 사용자 코드 없음
- "axe-core·Lighthouse CI" — 사용자 코드 없음
- Force 시뮬레이션·alphaDecay 튜닝·정착 tick 단축 — mindgraph 코드 미구현 (2026-06-03 확인)

## 4. 직무 분기 시 점검 체크리스트

새 직무 콘텐츠를 만들거나 기존 콘텐츠를 직무별로 바꿀 때 다음을 순서대로 확인합니다.

1. **노출 프로젝트 확인** — §2 매트릭스에서 ◎/○만 노출. × 등급은 `pdf.config.json`의 `roles.{role}.{resume|portfolio}.files`에서 제외.
2. **강조 어순 점검** — §3 직무별 어순 앞쪽 키워드가 첫 2~3 항목에 등장하는가?
3. **사실 근거 확인** — 본문 모든 키워드가 `requirements/{role}.md` 또는 `matrix.md §4`에 있는가? 없는 키워드는 제거.
4. **본문에 쓰지 않는 것** 검출 — §3 각 직무 마지막 목록을 grep으로 확인 (예: `grep -rE "PyTorch|GraphQL|Storybook" content/{resume,portfolio}/{role}/`).
5. **상위 작성 수준 가이드** — `../CLAUDE.md`의 5개 점검 기준(고유명사 3개 이하 / 수치 1개 이상 / 첫 문장 한 줄 요약 / 마지막 문장 의미 / 사외 독자 기준) 통과.
6. **mermaid lint** — `npm run lint:mermaid` 통과.
7. **PDF 생성 + 텍스트 해시 비교** — 4 직무 PDF 해시가 모두 다른가? 같으면 분기 안 됨.

## 5. 직무별 차별화의 정도 기준

같은 사실(코드·수치·다이어그램)을 직무별로 다르게 표현하는 4가지 레벨:

- **L1 어순 조정**: 핵심 키워드 순서만 바꿈. 본문 내용 동일.
- **L2 결과·배운 점 직무 시각**: Case `3. 결과` 부분만 직무 시각 어휘로 재서술.
- **L3 Case 본문 시각 차별화**: Case `1. 문제 원인` + `3. 결과`를 직무 시각으로 재작성. `2. 해결 과정`의 코드·수치는 유지.
- **L4 Case 셋 자체 차별화**: Case 자체를 직무별로 다르게 선별·재배치·추가. 다이어그램도 직무 시각으로 다름.

현재 mindgraph는 L4, chatGraph·Fit·xAB는 L2~L3 적용. AIN은 mindgraph L4 + chatGraph L2 (최소 2개 노출 규정 충족).

## 6. 작업 흐름 권장

새 직무 콘텐츠 작성·기존 직무 톤 변경 시:

```
1. requirements/{role}.md 읽기 → Top 5 자격·우대 메모
2. matrix.md §4 키워드 매칭 표 확인 → 사용자 자산 매칭
3. §3 직무별 강조 어순·금지 목록 확인
4. 본문 작성·수정
5. §4 체크리스트 7개 모두 통과
6. npm run pdf 실행 (lint·빌드·렌더 자동)
7. 텍스트 해시 4 직무 모두 다른지 비교
```

## 7. 변경 이력

- 2026-05-26: 초안 작성. 직무별 강조 어순·노출 프로젝트·금지 키워드 매트릭스화.
- 2026-05-30: 4 직무 requirements 재수집 (zighang 다중 키워드 합본, 표본 30→74~104건). AIN을 LLM Engineer 표본에서 "AI Native + Builder" 표본으로 교체 — 컨텍스트 엔지니어링·하네스 키워드가 사용자 자산과 정확 매칭. PE에 "문제 정의 우선·작은 팀 끝까지 책임" 추가, FE에 "빌드 도구(ESBuild·Vite·Webpack)" 추가, FDE에 "프로토타이핑·고객 워크숍·임원 발표" 추가.
- 2026-05-31: mindgraph handbook 2026-05-28~29 재편 반영. §3 모든 직무 매칭 자산: 6단계 → 3 phase, "실서비스 운영" → "1인 출시 전 프로토타입(도메인 등록 후 출시 전)"로 정정. AIN·PE·FDE에 부서·에이전트 분리 + context-map 자동 라우팅 매칭 추가. PE·FDE에 "출시 후 응대 인프라 사전 구축" 매칭 추가. 실제 mindgraph hooks 디렉토리 확인 결과 commit-user-gate 폐기로 9개 훅(차단 4 + 보조 5)이 정확. 이전 표기였던 "10훅·차단 5"는 정정.
