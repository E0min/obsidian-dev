### MindGraph (AI 지식 캡처 & 그래프 시각화)

서비스 개요: ChatGPT·Gemini·Claude·Grok 4개 LLM 답변을 캡처해 의미 단위로 묶고 Cytoscape.js로 시각화하는 Chrome Extension·Next.js 웹앱입니다. 기획·설계·개발·QA·내부 검증을 1인이 담당했고 도메인 getmindgraph.com 등록 후 출시 전 1인 프로토타입 단계입니다.

팀원: 1명 (1인 PO·풀스택 개발, 출시 후 응대 대비 인프라 사전 구축 중)

기술 스택: TypeScript, Next.js 16, React 19, Cytoscape.js, React Flow, Claude Code, Chrome Extension Manifest V3, IndexedDB, Supabase, GitHub Actions

- 4 LLM의 잦은 UI 변경에 단일 파일 수정으로 대응하기 위해 답변 DOM 선택자를 detector.ts SELECTORS에 모으고 hostname 자동 감지로 통합 레이어를 만들었습니다.
- 1인 운영이 가능하도록 Claude Code 위에 9개 훅·plan·build·qa·ship 4 phase /sprint·4중 SSOT 자동 동기를 설계해 sprint 라이프사이클 반복 작업을 자동화했습니다.
- LLM 응답 정확도와 응대 속도를 사전 확보하기 위해 7부서·9에이전트별 docs를 분리하고 task_type·코드 path를 must-read doc에 매핑해 워커 위임 시 합집합 5개 내외 doc만 첨부되도록 했습니다.
- 출시 후 사용자 응대 사이클을 단일 동선으로 묶기 위해 PostHog·Sentry·OpenTelemetry·api/feedback·api/error-log 5개 채널을 코드 베이스에 사전 구축했습니다.
- 카페·지하철 환경에서 캡처가 유실되지 않도록 IndexedDB 우선 기록과 Pending Ops 큐(MAX_RETRIES=5) 기반 Write-Behind 동기화로 오프라인 CRUD와 온라인 복귀 자동 flush를 구현했습니다.
- MV3 환경의 Extension 카트 데이터(저장한 LLM 답변 아이템) 릴레이를 허가되지 않은 origin이 가져갈 수 없도록 bridge.ts ALLOWED_ORIGINS 화이트리스트로 postMessage origin을 검증했습니다.
- Supabase RLS 정책 직접 설계와 GitHub Actions CI/CD·next-intl 한·영 다국어 운영까지 1인이 담당했습니다.
