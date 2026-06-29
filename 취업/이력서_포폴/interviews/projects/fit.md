---
title: Fit (WebRTC 컨퍼런스) 기술 면접 준비
aliases:
  - fit interview prep
  - WebRTC interview
type: interview-prep
project: Fit
status: budding
created: 2026-05-23
updated: 2026-05-23
tags:
  - career
  - interview-prep
  - project/Fit
  - status/budding
  - career/fe
  - career/product-engineer
related:
  - "[[취업/_INDEX]]"
  - "[[../../../FiT/_INDEX]]"
  - "[[이력서가이드]]"
source:
  - ~/깃허브/취업/이력서_포폴/이력서_포폴_v2/fit_interview_prep.md
migrated-from: 깃허브/취업/이력서_포폴/이력서_포폴_v2/fit_interview_prep.md
---

# Fit (WebRTC 컨퍼런스) 기술 면접 및 포트폴리오 상세 설명서

이 문서는 `Fit_portfolio.md`의 각 케이스에 대한 기술 근거(Rationale), 예상 면접 질문, 그리고 실제 코드 구현 위치를 정리한 자료입니다.

---

## Case 1. WebRTC & STOMP 기반 실시간 스트리밍

### 📌 핵심 기술 근거
- **P2P Necessity**: 서버를 거치는 미디어 서버(SFU/MCU) 방식은 비용이 높고 지연 시간이 발생합니다. 1:N 사일런트 컨퍼런스(현장 내 송출) 특성상 P2P(Mesh) 방식이 지연 시간(Latency) 최소화에 유리했습니다.
- **Signaling Logic**: WebRTC 연결을 위해선 서로의 SDP와 ICE Candidate를 교환해야 하는데, 이를 위해 HTTP Polling보다는 양방향 통신이 가능한 **WebSocket(STOMP)**이 적합했습니다.

### ❓ 예상 면접 질문
1. **Q: WebRTC 연결 과정(Signaling)을 설명해주실 수 있나요?**
   - **A:** (1) 발표자(Presenter)가 SDP Offer를 생성하여 STOMP로 서버에 보냅니다. (2) 서버는 이를 시청자(Audience)에게 중계합니다. (3) 시청자는 SDP Answer를 생성하여 다시 서버를 통해 발표자에게 보냅니다. (4) 동시에(병렬적으로) ICE Candidate를 교환하여 네트워크 경로를 찾으면 P2P 연결이 성립됩니다.

2. **Q: ICE Candidate가 SDP보다 먼저 도착하면 어떻게 처리했나요?**
   - **A:** `RemoteDescription`(상대방 정보)이 설정되기 전에 ICE 후보가 도착하면 에러가 발생합니다. 이를 막기 위해 `pendingCandidates` 배열(Queue)에 미리 도착한 후보들을 저장해두고, SDP 설정(`setRemoteDescription`)이 완료된 직후에 일괄 추가하는 방어 로직을 구현했습니다.

### 📍 코드 구현 (Code References)
- **`presenter-streaming.jsx` (@/frontend/frontend/src/components/streaming/presenter-streaming.jsx)**
    - `line 19-73`: STOMP 클라이언트 설정 및 구독(Subscribe).
    - `line 76-119`: `RTCPeerConnection` 초기화, 미디어 트랙 추가, Offer 생성 및 전송 로직.
    - `line 93`: `onicecandidate` 이벤트를 통해 ICE 후보를 STOMP로 전송.
- **`audience-streaming.jsx` (@/frontend/frontend/src/components/streaming/audience-streaming.jsx)**
    - `line 49-55`: `pendingCandidates`를 사용하여 Race Condition 해결.
    - `line 105`: `RTCPeerConnection` 초기화 (수신 전용 `recvonly`).

---

## Case 2. Scroll-telling Interaction (Intersection Observer)

### 📌 핵심 기술 근거
- **Performance**: `scroll` 이벤트 리스너는 메인 스레드에서 빈번하게 실행되어 성능 저하를 유발합니다. `Intersection Observer API`는 비동기적으로 관찰하므로 리플로우(Reflow)를 최소화하고 성능에 유리합니다.

### ❓ 예상 면접 질문
1. **Q: 스크롤 이벤트를 사용하지 않고 Intersection Observer를 쓴 이유는?**
   - **A:** `scroll` 이벤트는 스크롤 할 때마다 동기적으로 호출되어 레이아웃 계산 비용이 높은 반면, Observer는 브라우저 레벨에서 최적화되어 교차 시점만 알려주기 때문에 훨씬 가볍고 정확합니다.

### 📍 코드 구현 (Code References)
- **(추정) `LandingPage.jsx` 또는 `InfoSection.jsx`**
    - `useInView` (react-intersection-observer) 훅 사용.
    - `threshold: 0.2` (20% 진입 시 트리거).
    - Framer Motion `variants` (`hidden` -> `visible`) 정의 및 적용.

---

## Case 3. CSS Optimization (Tailwind JIT & Hardware Acceleration)

### 📌 핵심 기술 근거
- **Bundle Size**: 기존 CSS/SCSS는 사용하지 않는 클래스도 모두 포함되지만, Tailwind JIT(Just-In-Time) 모드는 소스 코드를 스캔하여 실제 사용된 클래스만 CSS 파일로 생성합니다.
- **Compositing**: `transform`이나 `opacity` 같은 속성은 GPU가 처리할 수 있는 컴포짓 레이어(Composite Layer)에서 동작하여 리페인트(Repaint)를 유발하지 않습니다.

### ❓ 예상 면접 질문
1. **Q: 애니메이션 최적화를 위해 어떤 속성을 주로 사용했나요?**
   - **A:** `left`, `top`, `width` 같은 Layout 속성 대신 `transform: translate3d()`나 `scale()`을 사용하여 GPU 가속을 유도하고 레이아웃 재계산(Reflow)을 방지했습니다.

### 📍 코드 구현 (Code References)
- **`tailwind.config.js`**
    - `content: ["./src/**/*.{js,jsx,ts,tsx}"]` 설정을 통해 사용된 파일 스캔.
- **`audience-streaming.jsx`**
    - `line 216`: Tailwind 유틸리티 클래스(`animate-wave`, `origin-bottom`)를 사용하여 CSS 애니메이션 적용.
