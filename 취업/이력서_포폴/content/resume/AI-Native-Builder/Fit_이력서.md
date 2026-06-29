### Fit (사일런트 컨퍼런스 플랫폼)

서비스 개요: 무선 헤드폰을 통해 다중 채널의 발표를 골라 듣는 사일런트 컨퍼런스의 온라인/오프라인 하이브리드 중계 플랫폼

팀원: 5명 (FE 3명, BE 2명)

기술 스택: Vite, React, WebRTC, STOMP, SockJS, Framer Motion, Redux Toolkit, redux-persist, Tailwind CSS

- 5인 협업에서 클라이언트와 서버 메시지 흐름이 어긋나지 않도록 백엔드 팀과 발표자·청중·혼잡도 토픽 네이밍과 STOMP `Bearer` 헤더 규약을 합의해 인증 검증과 시그널링 명세를 문서화하고 양쪽 구현 기준으로 고정했습니다.

- SDP 협상이 끝나기 전에 도착한 ICE 후보가 유실되지 않도록 컴포넌트 ref에 ICE 큐를 두고 setRemoteDescription 직후 일괄 flush하는 명시적 버퍼링 게이트를 적용해 비동기 시그널링 이벤트의 순서 의존성을 코드 경계로 흡수했습니다.

- 시그널링 트래픽과 혼잡도 데이터가 서로 채널을 점유해 디버깅을 어렵게 하지 않도록 혼잡도 전용 STOMP 클라이언트를 별도로 구성해 `/sub/session` 토픽만 구독하도록 분리하고 채널별 책임을 모듈 경계로 명시했습니다.

- 인증 토큰과 좋아요 세션 목록을 Redux Toolkit으로 관리하고 redux-persist whitelist에 auth만 포함하는 정책을 명시해 새로고침 이후에도 세션 컨텍스트는 유지하면서 휘발성 데이터까지 영속화되는 부작용을 코드 단에서 차단했습니다.

- 모바일 망과 행사장 Wi-Fi의 일시적 단절에 대비해 STOMP 클라이언트에 reconnectDelay 5초와 4초 양방향 heartbeat를 설정하고 자체 운영 TURN 서버를 ICE 후보군에 추가해 NAT 환경에서도 연결률을 유지했습니다.

- 현장 청취를 위한 수백 밀리초 단위 저지연 오디오 전송이 필요해 RTCPeerConnection API를 직접 사용해 발표자·청중 양측 시그널링 클라이언트를 구현하고 STOMP 토픽 위에서 SDP와 ICE 후보를 교환하는 1:N 오디오 송수신 흐름을 설계했습니다.

- 긴 안내 페이지에서 핵심 정보가 끝까지 노출되도록 react-intersection-observer 기반의 페이드인 인터랙션을 Framer Motion과 결합하여 구현했습니다.
