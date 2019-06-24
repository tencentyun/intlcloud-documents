### CVM과 데이터베이스를 같은 지역에 배포하면 Redis에 어떻게 연결하나요?
CVM과 데이터베이스를 동일한 지역에 배포할 경우, 사설망을 사용하여 접근하십시오. 연결은 [연결 가이드](https://cloud.tencent.com/document/product/239/30877)를 참조하십시오.

### CVM과 데이터베이스를 다른 지역에 배포하면 Redis에 어떻게 연결하나요?
기본 네트워크와 VPC의 연결은 [ClassicLink](https://cloud.tencent.com/document/product/215/20083)를 참조하십시오.
VPC 간의 연결은 [피어링 연결](https://cloud.tencent.com/document/product/215/20082)을 참조하십시오.

### TencentDB for Redis가 ping으로 통할 수 없으면 어떻게 처리하나요? 
Redis는 기본적으로 `ping`을 금지합니다. Telnet을 사용하여 연결성을 감지할 수 있습니다.

### Redis의 공중망 접근을 어떻게 활성화하나요? 
TencentDB for Redis는 지금 공중망 접근을 지원하지 않습니다.
공중만 접근을 필요할 경우, 공중망을 갖춘 CVM을 통하고 Iptable 프록시의 방식을 통해 구현할 수 있습니다.

### Redis 비밀번호 없이 로그인은 어떻게 설정하나요? 
현재는 비밀번호 없이 로그인을 지원하지 않습니다.


