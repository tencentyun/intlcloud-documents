Linux 커널은 소켓을 수신하는 동안 3방향 핸드 셰이크의 ACK 패키지를 받는 경우, SYN_REVC 상태에서 TCP_ESTABLISHED 상태로 전환합니다. 이때 커널은 tcp_v4_syn_recv_sock 함수를 호출합니다.
Hook 함수 tcp_v4_syn_recv_sock_toa는 기존의 tcp_v4_syn_recv_sock 함수를 우선적으로 호출한 뒤, get_toa_data 함수를 호출하여 TCP OPTION에서 TOA OPTION을 추출하고 sk_user_data 필드에 저장합니다.

위의 호출이 완료되면 inet_getname_toa hook inet_getname이 호출됩니다. 오리진 IP 주소와 포트를 획득할 때, 기존의 inet_getname을 우선적으로 호출한 뒤, sk_user_data가 공백 여부를 판단합니다. 실제 IP 및 포트를 필드에서 추출할 수 있으면 inet_getname의 반환값을 이 두 값으로 대체합니다.

클라이언트 프로그램은 사용자 상태에서 getpeername을 호출하고 반환한 IP와 포트는 클라이언트의 기존 IP와 포트가 됩니다.

