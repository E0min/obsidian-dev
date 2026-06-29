### Fit (사일런트 컨퍼런스 플랫폼)

서비스 개요: 무선 헤드폰을 통해 다중 채널의 발표를 골라 듣는 사일런트 컨퍼런스의 온라인/오프라인 하이브리드 중계 플랫폼

팀원: 5명 (FE 3명, BE 2명)

기술 스택: Vite, React, WebRTC, STOMP, SockJS, Framer Motion, Redux Toolkit, redux-persist, Tailwind CSS

- 현장 청취에 필요한 수백 밀리초대 저지연 오디오를 위해 RTCPeerConnection API를 직접 사용하고 STOMP 토픽 위에서 SDP·ICE를 교환하는 1:N 송수신 흐름을 발표자·청중 양측 클라이언트에 구현했습니다.

- SDP 협상 이전에 도착한 ICE 후보가 유실되는 문제를 해결하기 위해 컴포넌트 ref에 ICE 큐를 두고 setRemoteDescription 직후 일괄 flush하는 버퍼링 로직을 적용해 PeerConnection 성공률을 끌어올렸습니다.

- 모바일 망과 행사장 Wi-Fi 단절에 대비해 STOMP 클라이언트에 reconnectDelay 5초와 4초 간격 양방향 heartbeat를 설정하고 자체 운영 TURN 서버를 ICE 후보군에 추가해 NAT 환경 연결률을 확보했습니다.

- 시그널링과 혼잡도 트래픽이 서로의 채널을 점유하지 않도록 혼잡도 전용 STOMP 클라이언트를 별도 구성해 `/sub/session` 토픽만 구독하게 분리하고 채널별 인원 변동을 실시간 화면에 반영했습니다.

- 인증 토큰과 좋아요 세션 목록을 Redux Toolkit으로 관리하고 redux-persist whitelist에 auth만 포함해, 새로고침 이후 세션을 유지하면서 휘발성 데이터의 영속화 부작용을 차단했습니다.

- 백엔드 팀과 발표자·청중·혼잡도 토픽 네이밍과 STOMP `Bearer` 헤더 규약을 합의해 인증 검증과 시그널링 명세를 정렬하고 클라이언트·서버 메시지 흐름을 일관되게 유지했습니다.
