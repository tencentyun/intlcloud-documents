### FTP 기능은 어떻게 활성화합니까?

COS는 일종의 Web 방식의 요청을 지원하는 지속성을 지닌 스토리지이며, 네이티브 FTP 액세스 방식을 제공하지 않습니다. FTP 프로토콜을 사용하는 경우 반드시 경유를 거쳐야 하며 **Tencent Cloud 공식 홈페이지에서 제공하는 [FTP Server 툴](https://www.qcloud.com/document/product/436/7214)에 따라 자체적으로 서비스를 구축하여 사용하시기 바랍니다.**
FTP 프로토콜은 오래된 프로토콜로, 데이터 완전성을 인증할 수 없고 전송 보안성을 보장할 수 없으며, CAM 권한 시스템과 연결할 수도 없습니다. 따라서 지속적인 FTP 프로토콜 액세스 사용은 매우 권장하지 않습니다. 또한 Tencent Cloud는 FTP 프로토콜 및 경유 소프트웨어에 대해 향후 지원하지 않을 수 있습니다. 
데이터 동기화가 필요한 경우 [COS Migration 툴 ](https://intl.cloud.tencent.com/document/product/436/15392) 또는 [COSCMD 툴](https://www.qcloud.com/document/product/436/10976)을 직접 사용하는 것을 권장합니다.

### 구성 파일 중 masquerade_address 선택 항목은 어떤 작용을 합니까? 어떤 경우 masquerade_address를 설정합니까?

masquerade_address는 클라이언트에 서버 주소를 제공하는 설정입니다. NAT를 통해 공인 IP에 매핑되는 호스트에서 FTP server가 실행되는 경우, masquerade_address 선택 항목을 클라이언트가 액세스할 수 있는 FTP Server 공인 IP로 설정하여 클라이언트에 해당 IP를 사용하여 서버와의 데이터 통신을 완료하도록 알릴 필요가 있습니다.

예를 들어 FTP Server가 실행되는 기기에서 ifconfig를 실행하여 외부 네트워크에 매핑된 ENI IP 10.xxx.xxx.xxx를 획득하였고, 매핑된 공인 IP를 119.xxx.xxx.xxx로 가정하면, 이 때 FTP Server에 masquerade_address를 클라이언트가 server에 액세스할 때의 공인 IP(119.xxx.xxx.xxx)로 명시적으로 설정하지 않은 경우 FTP Server는 Passive 모드에서 클라이언트에 내부 네트워크 주소(10.xxx.xxx.xxx)를 사용하여 반환하게 됩니다. 이 때 클라이언트에서 FTP Server에 연결할 수 있게 되지만 정상적으로 클라이언트에 데이터 패킷을 반환하지 않게 됩니다.

따라서 일반적으로 masquerade_address를 클라이언트에서 Server 연결 시 사용하는 해당 IP로 설정하는 것을 권장합니다.

### masquerade_address 선택 항목을 정확하게 설정한 후 ftp server에 정상적으로 로그인은 되지만 FTP 명령어인 list 또는 get 등 데이터 검색 명령어 실행 시 "서버에서 경유할 수 없는 주소를 반환했습니다." 또는 "ftp: connect: No route to host" 등의 오류가 발생합니다. 어떻게 처리해야 합니까?

해당 case는 대부분 ftp server 머신 iptables 또는 방화벽 정책 설정이 모든 ICMP 프로토콜을 reject하거나 drop하여 발생합니다. FTP 클라이언트가 FTP Server 수동 모드에서 리턴되는 데이터 연결 IP를 획득한 후 먼저 ICMP 패킷을 발송해 IP의 연결성을 확인하므로 클라이언트에 "서버에서 경유할 수 없는 주소를 반환했습니다." 등의 오류가 발생하게 됩니다.

권장 솔루션: iptables 정책을 필요에 따라 제한할 ICMP 패킷 유형만 reject 또는 drop하도록 설정합니다. 외부 ping 유형의 ICMP 패킷만 reject/drop하고 싶은 경우 정책을 다음과 같이 설정할 수 있습니다. iptables -A INPUT -p icmp --icmp-type 8 -s 0/0 -j [REJECT/DROP]
또는 독립적으로 액세스할 ftp server의 클라이언트 IP를 개방할 수 있습니다.

### 큰 용량의 파일 업로드 시 중도에 취소했는데 COS에 이미 업로드한 파일이 남아 있는 이유는 무엇입니까?

COS에 사용되는 최신 버전의 FTP Server에서는 완전한 플로우 방식의 업로드 특성을 제공하여 사용자가 파일 업로드를 취소하거나 중단하는 경우 대용량 파일의 업로드 완료 작업을 트리거합니다. 따라서 COS는 사용자 데이터 플로가 업로드 완료된 것으로 알고 이미 업로드된 데이터를 하나의 완벽한 파일로 구성합니다. 사용자가 다시 업로드하고 싶은 경우 직접 원본 파일 이름으로 업로드하여 덮어쓰거나 수동으로 불완전 파일을 삭제하고 다시 업로드할 수 있습니다.

### 왜 FTP Server 설정에서 업로드 파일의 최대 크기를 설정해 제한해야 합니까?

COS의 멀티파트 업로드 수는 최대 10000개까지 가능하며, 블록당 크기는 1MB~5G로 제한됩니다. 해당 설정으로 업로드 파일 최대 크기를 제한하는 것은 업로드 파일 블록의 크기를 합리적으로 계산하기 위해서입니다.
FTP Server는 기본적으로 200GB 이내의 단일 파일 업로드를 지원합니다. 그러나 너무 크게 설정하는 것은 권장하지 않습니다. 단일 파일 크기를 크게 설정할수록 업로드 시 멀티파트 버퍼도 그에 따라 늘어나게 되며, 이 경우 사용자의 메모리 리소스를 소모할 수도 있습니다. 따라서 사용자의 실제 상황에 따라 단일 파일 크기 제한을 합리적으로 설정하시기 바랍니다.

### 업로드한 파일이 최대 제한을 초과하면 어떻게 됩니까?

실제 업로드한 단일 파일 크기가 구성 파일 상의 제한을 초과하게 되면 시스템에서 IOError 오류를 리턴하며 로그에 오류 정보를 기록합니다.

기타 문제가 발생하는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의하십시오. 티켓 제출 시 전체 `cos_v5.log` 로그를 첨부하면 문제를 진단하고 해결하는 데 더욱 도움이 됩니다.
