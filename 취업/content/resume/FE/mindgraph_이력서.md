### MindGraph (AI 지식 캡처 & 그래프 시각화)

서비스 개요: ChatGPT·Gemini·Claude·Grok의 답변을 캡처 즉시 의미 단위로 묶어 D3.js로 시각화하는 Chrome Extension·Next.js 웹앱입니다.

팀원: 1명 (1인 개발, 도메인 getmindgraph.com 등록 후 출시 전)

기술 스택: TypeScript, Next.js 16 App Router, React 19, D3.js, Tailwind CSS, Chrome Extension Manifest V3, IndexedDB, Supabase, next-intl, GitHub Actions

- D3.js 직접 DOM 조작과 Next.js SSR 충돌을 막기 위해 그래프 엔진을 'use client' 전용 레이어로 격리하고 reactStrictMode를 비활성화해 zoom 이중 바인딩을 차단했습니다.
- Service Worker·Content Script·bridge 번들을 분리하기 위해 3개 vite 설정(extension·content·bridge)과 Next.js webpack 빌드를 공존시켰습니다.
- 네트워크 단절 시 캡처 노드 유실을 막기 위해 IndexedDB 우선 기록과 Pending Ops 큐 기반 Write-Behind 동기화로 오프라인 CRUD와 온라인 복귀 자동 flush를 구현했습니다.
- 4 LLM의 잦은 DOM 변경에 단일 파일 수정으로 대응하기 위해 답변 선택자를 detector.ts SELECTORS에 모으고 hostname 자동 감지로 통합했습니다.
- MV3 Content Script와 Web 사이 Extension 카트 데이터(저장한 LLM 답변 아이템) 릴레이는 bridge.ts ALLOWED_ORIGINS 화이트리스트로 origin을 검증해 허가되지 않은 origin이 카트 데이터를 가져갈 수 없게 차단했습니다.
- Supabase RLS 정책 직접 설계와 GitHub Actions CI/CD·next-intl 한·영 다국어 라우트를 1인이 구축했습니다.
