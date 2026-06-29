### Fit (사일런트 컨퍼런스 플랫폼)

서비스 개요: 무선 헤드폰을 통해 다중 채널의 발표를 골라 듣는 사일런트 컨퍼런스의 온라인·오프라인 하이브리드 중계 플랫폼

팀원: 5명 (FE 3명, BE 2명)

기술 스택: Vite, React, WebRTC, STOMP, SockJS, Framer Motion, Redux Toolkit, redux-persist, Tailwind CSS

- 현장 저지연 오디오 전송을 위해 RTCPeerConnection API로 발표자·청중 양측 시그널링 클라이언트를 구현하고 STOMP 토픽에서 SDP·ICE 후보를 교환하는 1:N 송수신 흐름을 설계했습니다.

- SDP 협상 전 도착한 ICE 후보가 유실되어 청중이 발표자 음성에 접속하지 못하는 문제를 컴포넌트 ref에 ICE 큐를 두고 setRemoteDescription 직후 일괄 flush하는 버퍼링 로직으로 해결했습니다.

- 모바일 망과 행사장 Wi-Fi의 일시적 단절에 대비해 STOMP 클라이언트에 reconnectDelay 5초와 4초 간격 양방향 heartbeat를 설정하고 자체 TURN 서버를 ICE 후보군에 추가했습니다.

- 시그널링 트래픽과 혼잡도 데이터가 서로의 채널을 점유하지 않도록 혼잡도 전용 STOMP 클라이언트를 별도 구성해 `/sub/session` 토픽만 구독하게 분리했습니다.

- 인증 토큰과 좋아요 세션 목록을 Redux Toolkit으로 관리하고 redux-persist whitelist에 auth만 포함해 새로고침 후 세션 유지와 휘발성 데이터 영속화 방지를 함께 달성했습니다.
