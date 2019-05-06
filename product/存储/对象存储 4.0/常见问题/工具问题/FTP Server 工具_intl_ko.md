### FTP 기능을 어떻게 사용합니까?

COS는 Web 방식 요청을 지원하는 장기화 스토리지이고 원본 FTP 접근 방식을 제공하지 않습니다. FTP 프로토콜을 사용하려면 반드시 중간 전송이 필요합니다. **Tencent Cloud에서 제공하는 [FTP Server 도구](https://www.qcloud.com/document/product/436/7214)에 따라 서비스를 자체로 설정하는 것을 권장합니다.**
FTP 프로토콜은 오래된 것으로 인해 데이터 무결성을 확인하거나 전송 보안을 보장하거나 CAM 권한 시스템과 도킹할 수 없습니다. 따라서 FTP 프로토콜을 계속 사용하여 접근하는 것은 좋지 않으며 Tencent Cloud는 FTP 프로토콜과 중간 전송 소프트웨어에 대해 후속 지원을 제공하지 않습니다.
데이터 동기화할 경우 [COS Migration 도구](https://www.qcloud.com/document/product/436/7133) 또는 [COSCMD 도구](https://www.qcloud.com/document/product/436/10976)를 직접 사용하는 것을 권장합니다.

### 구성 파일의 masquerade_address 옵션은 어떤 역할을 합니까? 언제 masquerade_address를 구성해야 합니까?

FTP Server가 여러 ENI가 있는 Server에서 운행하며 FTP Server가 PASSIVE 모드로 실행되고 있을 때(일반적으로 FTP 클라이언트가 NAT 게이트웨이 뒤에 있을 때 PASSIVE 모드를 시동해야 합니다.) masquerade_address 옵션을 사용하여 passive 모드에서 reply를 위해 유일한 IP를 바인딩해야 합니다.

예를 들어, FTP Server에는 여러 개의 IP 조소가 있는데, 사설 IP는 10.XXX.XXX.XXX이고 공인 IP가 123.XXX.XXX.XXX입니다. 클라이언트는 공인 IP를 통해 FTP Server에 연결하는 동시에 PASSIVE 모드에서 데이터를 전송합니다. 이때 FTP Server가 masquerade_address가 공인 IP에 구체적으로 바인딩되는 것을 지정하지 않으면 Server는 PASSIVE 모드에 있을 때 사설 IP를 통해 reply를 할 수 있습니다. 이 경우 클라이언트가 Ftp server에 연결할 수 있지만 Server에서 데이터에 대해 아무 응답을 가져올 수는 없습니다.

masquerade_address를 구성할 경우, 클라이언트가 Server에 연결할 때 사용하는 IP 주소로 설정하는 것을 권장합니다.

### masquerade_address 옵션을 정확하게 설정한 후에 ftp server에 정상적으로 로그인할 수 있지만 FTP 명령: list 또는 get과 같은 데이터 검색 명령을 실행할 때 "서버가 라우팅할 수 없는 주소로 되돌아갑니다" 또는 "ftp: connect: o route to host" 등 오류가 발생하면 어떻게 처리해야 합니까?

이 경우는 대부분 ftp server 서버 iptables 또는 방화벽 정책이 모든 ICMP 프로토콜 패킷을 거부하거나 삭제하도록 구성되어 있지만 FTP 클라이언트가 수동 모드에서 FTP 서버가 반환한 데이터 연결 IP를 받은 후, 먼저 IP의 연결을 확인하기 위해 ICMP 패킷을 보내기 때문입니다. 따라서 클라이언트가 "서버가 라우팅 할 수 없는 주소로 되돌아갑니다."와 같은 오류를 보고합니다.

제안 설루션: 차단하려는 ICMP 패킷 유형만 거부하거나 삭제하도록 iptables 정책을 구성하십시오. 외부 ping 유형의 ICMP 패킷만 차단하려는 경우 정책을 다음과 같이 변경할 수 있습니다. iptables -A INPUT -p icmp -icmp-type 8 -s 0/0 -j [REJECT/DROP].
또는 ftp server에 접근할 클라이언트의 IP를 개별적으로 허용할 수도 있습니다.

### 대용량 파일의 업로드가 중간에 취소되면 COS에서 업로드된 부분이 왜 유지됩니까?

COS 최신 버전의 FTP Server는 전체적인 스트리밍 업로드 특성을 제공하기 때문에 사용자가 파일 업로드의 취소 또는 차단은 대용량 파일 업로드 작업을 완료하는 것을 촉발시킬 수 있습니다. 이 경우 COS는 사용자 데이터 스트림이 업로드된 것으로 간주하고 업로드된 데이터를 완전한 파일로 결합합니다. 사용자가 업로드를 다시 시작하려면 원래 파일 이름으로 업로드하여 원래 파일을 덮어쓰거나 불완전한 파일을 수동으로 삭제하고 다시 업로드하십시오.

### FTP Server 구성에서 업로드할 파일의 크기 제한을 설정해야 하는 이유는 무엇입니까?

COS에서 멀티파트 업로드하는 최대 수는 10000이며 각 멀티파트의 크기는 1 MB - 5 G로 제한됩니다. 최대 업로드 파일 제한을 부과하는 목적은 하나의 멀티파트를 업로드하면 크기를 합리적으로 계산하는 것입니다.
FTP Server는 기본적으로 200 GB 미만의 단일 파일 업로드를 지원합니다. 그러나 파일 크기 제한이 클수록 업로드 중에 멀티파트에 대한 버퍼가 커져서 사용자의 메모리 자원이 소모하므로 제한 값을 너무 크게 설정하는 것은 좋지 않습니다. 따라서 자신의 실제 상황에 따라 적절한 단일 파일 크기 제한을 설정하는 것이 좋습니다.

### 업로드된 파일의 크기가 한도를 초과하면 어떻게 됩니까?

업로드된 단일 파일의 크기가 구성 파일에 설정된 제한을 초과하면 시스템은 IOError 이상을 반환하고 오류 정보를 로그에 표시합니다.

다른 질문이 있으시면, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 하십시오. 더불어 문제를 더욱 정확하게 해결하기 위해 완전한 `cos_v5.log` 로그를 첨부하십시오.
