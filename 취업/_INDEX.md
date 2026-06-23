---
type: project-index
status: active
created: 2026-05-23
last-touched: 2026-06-06
repo: ~/깃허브/취업/이력서_포폴/이력서_포폴_v2/pdf-generator
tags:
  - project/취업
  - status/active
  - career/fe
  - career/product-engineer
  - career/fdd
  - career/ai-native
---

# 취업 — 직무 준비 메타 프로젝트

> 4개 직무 동시 준비: **FE / Product Engineer / Forward Deployed Developer / AI-Native Builder**
> `~/깃허브/취업/`의 컨텐츠 자산이 여기서 합류. 코드(pdf-generator)는 깃허브에 유지.

## Status
- 현재: 4 직무 이력서·포폴 본문 정합성·적합성 검증 완료 (2026-06-06). 코드 ground-truth 대조로 룰 A 위반 정리 — INP 식별자 제거·Fit STOMP 채팅/혼잡도 한정·미구현 기능(임베딩 추천·H1/H3·Force 시뮬) 본문 제거·AI-slop/박-어휘/분량 0건. AIN 노출 2 프로젝트(mindgraph+chatGraph)로 확장.
- 다음 액션: target-companies 3~5개 분석, narrative 초안, (선택) 적합성 정량 수치·FE 접근성 보강

## Map
- [[취업/guides/_MOC]] — 이력서·포폴·프롬프트 가이드 (3종)
- [[취업/자소서/_MOC]] — 자기소개서 작업 공간 (회사별 작성·지원동기 가이드)
- [[취업/interviews/_MOC]] — 면접 준비 자료
  - [[fit]] — WebRTC 컨퍼런스 (Fit)
  - [[chatgraph]] — 대화형 데이터 시각화
  - [[xab]] — A/B 테스트 SNS
- [[취업/content/_MOC]] — **이력서·포폴 컨텐츠 SSOT** (옵시디언이 SSOT, pdf-generator/content가 symlink)
- [[취업/outputs/_MOC]] — **pdf-generator 생성 PDF** (최신: FDE/41·PE/39·AIN/40·FE/43, 파일명 `이력서_{role}.pdf`)
- [[취업/jd-analysis/_MOC]] — 채용공고 분석 (2026-05-23, 18건 박제 + 4 직무 분석 + matrix)
- [[취업/오픽/_MOC]] — OPIc IH 목표 준비 자료
- [[target-companies]] — 타겟 회사
- [[portfolio-strategy]] — 직무별 어필 자산 매핑
- [[narrative]] — 내 스토리라인
- [[credentials]] — 증명서류 메타
- [[informations]] — mindgraph 참조 폴더
- [[취업/links-to-code]] — `~/깃허브/취업/` 자산 매핑
- [[legacy-v1]], [[legacy-v2]] — 구버전 이력서·포폴

## 4직무별 핵심 자산

### FE
- pdf-generator: `content/resume/FE/`, `content/portfolio/FE/`
- atomic: [[../../FE/react/_concepts/vercel-react-best-practices]]
- atomic: [[../../FE/d3-visualization/_concepts/opacity-ssot-pattern]] (evergreen)
- atomic: [[../../FE/d3-visualization/_concepts/d3-chunk-runner-ric-raf]] (evergreen, INP)
- atomic: [[../../FE/nextjs/middleware-proxy/nextjs-16-middleware-to-proxy]]

### Product Engineer
- pdf-generator: `content/resume/Product-Engineer/`, `content/portfolio/Product-Engineer/`
- atomic: [[../../AI-Native/agents/swarm-workflow-real-issues]] (evergreen)
- atomic: [[../../AI-Native/_concepts/5-layer-backpropagation]] (evergreen)
- atomic: [[../../FE/d3-visualization/force-simulation/fx-fy-dual-semantics]] (의미 설계)

### Forward Deployed Developer (FDE)
- pdf-generator: `content/resume/FDE/`, `content/portfolio/FDE/`
- atomic: [[../../AI-Native/tools/codex/pair-programming-root-fix]] (evergreen)
- atomic: [[../../BE/api-design/empty-set-antipattern]]
- atomic: [[../../FE/d3-visualization/_concepts/d3-chunk-runner-ric-raf]]

### AI-Native Builder
- pdf-generator: `content/resume/AI-Native-Builder/`, `content/portfolio/AI-Native-Builder/`
- atomic: [[../../AI-Native/_concepts/5-layer-backpropagation]] (evergreen)
- atomic: [[../../AI-Native/claude-code/workflows/build-pr-block-backpropagation]] (evergreen)
- atomic: [[../../AI-Native/skills/_MOC]] — 184개 스킬 운영

## 프로젝트 어필 매핑

| 프로젝트 | FE | PE | FDD | AI-N | 면접 자료 |
|----------|----|----|-----|------|----------|
| [[../mindgraph/_INDEX]] | ◎ | ◎ | ○ | ◎ | — |
| [[../FiT/_INDEX]] | ◎ | ○ | ○ | — | [[fit]] |
| [[../chatGraph-FE-local/_INDEX]] | ◎ | ◎ | ○ | ○ | [[chatgraph]] |
| [[../xab/_INDEX]] | ○ | ◎ | — | ○ | [[xab]] |
| [[../pdf-generator/_INDEX]] | ○ | ◎ | ○ | ◎ | — |
| [[../virtual-company/_INDEX]] | ○ | ○ | ◎ | ◎ | — |

## pdf-generator와의 관계

- 이력서·포폴 MD의 **유일 SSOT** = `~/obsidian/Dev/취업/content/` (옵시디언 vault). `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/pdf-generator/content`가 symlink로 가리킴
- 옵시디언은 이력서·포폴 본문 + **메타 지식**(어필 매핑, JD 분석, 면접 기록, narrative)을 함께 보유
- 작성 규칙: `이력서_포폴_v2/pdf-generator/CLAUDE.md` + `docs/{writing,resume,portfolio,pdf-build}.md` + `content/CLAUDE.md` ↔ [[../../CLAUDE]] §11 sync

## See also
- [[Projects/_MOC]]
- [[../../_now]]
- [[../pdf-generator/_INDEX]]
