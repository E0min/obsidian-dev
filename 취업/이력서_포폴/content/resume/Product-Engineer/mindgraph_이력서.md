### MindGraph (AI 지식 캡처 & 그래프 시각화)

서비스 개요: ChatGPT·Gemini·Claude·Grok의 답변을 캡처 즉시 의미 단위로 묶어 Cytoscape.js로 시각화하는 Chrome Extension·Next.js 웹앱입니다. 기획·설계·개발·QA 전 구간을 1인 PO로 수행했고 도메인 getmindgraph.com 등록 후 출시 전 1인 프로토타입 단계입니다.

팀원: 1명 (1인 PO·풀스택 개발)

기술 스택: TypeScript, Next.js 16 App Router, React 19, Cytoscape.js, React Flow, Chrome Extension Manifest V3, IndexedDB, Supabase, Claude Code, GitHub Actions

- 1인 PO 환경에서 가설을 빠르게 검증하기 위해 Claude Code 위에 9개 훅·plan·build·qa·ship 4 phase /sprint·4중 SSOT 자동 동기를 설계해 sprint 라이프사이클 반복 작업을 자동화했습니다.
- 매 prompt에 전체 docs가 끌려오는 컨텍스트 과부하를 줄이려고 7부서·9에이전트별 docs를 분리하고 task_type·코드 path glob을 must-read doc에 매핑해 첨부량을 5개 내외로 좁혔습니다.
- 출시 후 가설 검증 인프라를 사전 구축하기 위해 PostHog·Sentry·OpenTelemetry·api/feedback·api/error-log 5개 채널을 코드 베이스에 모았습니다.
- 네트워크 불안정 환경에서 캡처가 유실되지 않도록 IndexedDB 우선 기록과 Pending Ops 큐(MAX_RETRIES=5) 기반 Write-Behind 동기화로 오프라인 CRUD와 온라인 복귀 자동 flush를 구현했습니다.
- TopicNode·QANode 분리 구조의 교차 조회 비용을 해결하기 위해 nodeType·parentId·path·childIds·depth 메타데이터를 가진 UnifiedNode 단일 모델을 설계해 조상 경로 조회를 path 한 번 분해로 처리했습니다.
- Supabase RLS 정책 직접 설계와 GitHub Actions CI/CD·next-intl 한·영 다국어·MV3와 Web origin 화이트리스트 검증까지 1인이 운영했습니다.
