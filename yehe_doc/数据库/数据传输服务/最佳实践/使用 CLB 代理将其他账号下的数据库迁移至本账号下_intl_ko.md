## 작업 시나리오
이 시나리오에서는 로드 밸런싱(CLB)을 통한 프록시 서비스, 원본 데이터베이스와 DTS의 네트워크 연결을 소개합니다. 다른 Tencent Cloud 계정과 연결된 IDC 자체구축 데이터베이스 또는 다른 클라우드 벤더의 데이터베이스를 이 계정으로 마이그레이션/동기화하는 데 적합하며 동시에 작업을 수행할 수 있는 계정의 권한이 제한되는 시나리오를 예시로 들면 다음과 같습니다.

- VPC-A와 VPC-B는 그룹사 네트워크이고, VPC-C는 자회사 네트워크이며, 계정 C는 A와 B의 리소스를 운용할 수 있는 권한이 없습니다.
- 계정 A 아래에 자체 구축된 IDC 네트워크 또는 타사 클라우드 벤더 네트워크에 연결하기 위한 전용선을 구축하고, 계정 B는 클라우드 네트워킹을 통해 VPC-A, VPC-B, VPC-C에 연결하므로 점선 박스 안의 네트워크가 모두 연결되었으며 계정 C는 원본 데이터베이스에 액세스할 수 있습니다.
- 계정 C를 사용하여 DTS 마이그레이션/동기화합니다. <br>

이 시나리오에서는 CLB가 계정 간에 네트워크를 연결하는 기능이 있고 CLB가 라우팅 및 전달을 위한 DTS 프록시 서비스로 사용되기 때문에 원본 데이터베이스를 CLB와 연결할 수 있습니다. 주요 구성 원칙은 다음과 같습니다.
1. C 계정을 사용하여 CLB 인스턴스를 생성합니다.
2. CLB에서 백엔드 서비스를 구성하고 원본 데이터베이스 IP를 백엔드 서비스에 바인딩합니다.
3. 마이그레이션/동기화 작업을 생성하고 원본 데이터베이스의 IP 주소와 포트, CLB의 주소와 포트를 입력합니다.

## 작업 단계
### C 계정으로 CLB 인스턴스 생성
1. C 계정을 사용하여 Tencent Cloud [CLB 구매 페이지](https://buy.intl.cloud.tencent.com/lb)에 로그인합니다.
2. CLB와 관련된 매개변수를 설정합니다. **종량제** 및 **사설망** 유형을 선택합니다.
3. CLB **인스턴스 관리** 페이지로 돌아가서, 후속 DTS 구성에서 사용될 VIP를 확인합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/ba3f69595bf2f21ae8df95e88bad5fdb.png)

### 원본 데이터베이스 IP를 CLB 백엔드 서비스에 바인딩
> ? 아래 설명의 CLB 작업은 참고용이며 실제 콘솔 인터페이스와 다를 경우 [CLB 공식 웹사이트 문서](https://intl.cloud.tencent.com/document/product/214/38442)를 참고하십시오.

1. CLB **인스턴스 관리** 페이지에서 방금 구매한 CLB 인스턴스를 찾아 인스턴스 ID를 클릭합니다.
2. **기본 정보** 페이지의 **백엔드 서비스** 영역에서, VPC가 아닌 바인딩 IP 기능을 활성화하고 **구성 클릭**을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/70adcb0459a06a353058098f23b25a5f.png)
3. 팝업 창에서 **제출**을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c00934610178e8b32719aee58a86c4a5.png) 
4. 새 SNAT IP가 활성화되면 백엔드 서비스 모듈에 표시됩니다. **SNAT IP 추가**를 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/84735d9ce8f922c8fd3fd9a73b21dbdb.png)
5. 팝업 창에서 서브넷을 선택한 다음 **추가**를 클릭하여 IP를 할당하고 마지막으로 **저장**을 클릭합니다.
6. SNAT IP를 설정한 후의 페이지는 다음과 같습니다.
7. CLB 리스너를 생성합니다. 인스턴스 세부 정보 페이지에서 **리스너 관리** 탭을 클릭한 다음 TCP/UDP/TCP SSL/QUIC 리스너에서 **생성**을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7dc7b16f1020912d5c8b57cc030cad26.png)
8. 팝업 창에서 TCP 리스너를 구성합니다. 상태 확인 및 세션 보존, 활성화 여부를 선택할 수 있습니다.
9. 모니터 설정이 완료되면 생성된 구성자를 클릭하고 우측의 **바인딩**을 클릭하여 원본 데이터베이스의 IP 주소를 바인딩합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/91b459e636f74b5df223efa75459a2e8.png)
10. 팝업 창에서 **기타 사설망 IP**를 선택하고 바인딩할 원본 데이터베이스 IP 주소를 입력하고 포트와 가중치를 입력하고 마지막으로 **확인**을 클릭합니다.
      ![](https://qcloudimg.tencent-cloud.cn/raw/0b54092cef7ff8884a9c3254eb433ce3.png)
11. 바인딩된 원본 데이터베이스 IP를 보려면 **바운딩된 백엔드 서비스** 영역으로 돌아갑니다.

### DTS 작업 구성
CLD 프록시를 이용한 DTS 설정 단계는 기본적으로 일반 [DTS 데이터 마이그레이션 작업](https://intl.cloud.tencent.com/document/product/571/42645) 또는 [DTS 데이터 동기화 작업](https://intl.cloud.tencent.com/document/product/571/47344) 설정 단계와 동일하며 여기에서는 차이점만 자세히 소개합니다.

C 계정으로 데이터 마이그레이션/동기화 작업 구매 후 **원본 및 대상 데이터베이스 설정** 단계에서 **사설망 VPC**를 액세스 방식으로 선택(활성화 신청 시 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 필요)하고, 사설망 및 서브넷의 경우 계정 C의 VPC 및 서브넷을 선택하고 호스트 주소에 CLB 인스턴스의 VIP 주소를 입력합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/b0a64971c3df79f56f9d851c69e3c802.png)
