### MindGraph (AI 지식 캡처 & 그래프 시각화)

서비스 개요: ChatGPT·Gemini·Claude·Grok 4개 LLM 답변을 hostname 자동 감지로 캡처해 의미 단위로 묶고 지식 그래프로 시각화하는 Chrome Extension·Next.js 웹앱입니다. 도메인 getmindgraph.com 등록 후 출시 전 1인 프로토타입 단계입니다.

팀원: 1명 (1인 AI 협업 운영)

기술 스택: TypeScript, Next.js 16, React 19, D3.js, Claude Code, Chrome Extension Manifest V3, IndexedDB, Supabase, GitHub Actions, LLM API (OpenAI·Anthropic·Google·xAI)

- 4 LLM의 잦은 UI 변경에 단일 파일 수정으로 대응하기 위해 답변 DOM 선택자를 detector.ts SELECTORS에 모으고 hostname 자동 감지로 통합 레이어를 만들었습니다.
- Claude Code 위에 9개 훅(차단 4·보조 5)과 plan·build·qa·ship 4 phase /sprint·4중 SSOT 자동 동기를 설계해 sprint 라이프사이클 반복 작업을 한 명령 흐름으로 자동화했습니다.
- 매 prompt에 전체 docs가 끌려오는 컨텍스트 과부하를 줄이기 위해 7부서·9에이전트별 docs를 분리하고 task_type·코드 path glob을 must-read doc에 매핑해 첨부량을 5개 내외로 좁혔습니다.
- 네트워크 단절 시 LLM 답변 캡처 유실을 막기 위해 IndexedDB 우선 기록과 Pending Ops 큐(MAX_RETRIES=5) 기반 Write-Behind 동기화로 오프라인 CRUD와 온라인 복귀 자동 flush를 구현했습니다.
