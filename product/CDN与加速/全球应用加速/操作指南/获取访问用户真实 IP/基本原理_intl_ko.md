패킷이 가속 연결을 통해 포워딩되면 SNAT 및 DNAT가 패킷에서 수행되어 소스 주소 및 대상 주소를 모두 수정합니다. 오리진 서버에 표시된 데이터 패킷의 소스 주소는 실제 클라이언트 IP가 아닌 가속 연결의 포워딩 IP입니다. 클라이언트 IP를 서버에 보내기 위해 가속 연결은 클라이언트 IP와 포트를 다음과 같은 사용자 지정 "tcp option" 필드에 넣습니다.
```
#define TCPOPT_ADDR  200    
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
 * insert client ip in tcp option, now only support IPV4,
 * must be 4 bytes alignment.
 */
struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
};
```

