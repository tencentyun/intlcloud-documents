## VPC에서 가용 영역 간 접근

여러 대의 CVM이 지역 내 다른 가용 영역에 분포되어 있지만 파일 저장을 공유해야 할 때, CVM과 CFS를 동일한 VPC에 설정하면 가용 영역 간의 리소스 상호 접근을 실현할 수 있습니다.

광저우를 예로 들면, 광저우 1지역의 CVM이 있는데 이때 CFS를 사용해야 하지만 광저우 1지역은 리소스가 매진되어 파일 시스템을 바로 생성할 수 없습니다.
CVM이 VPC의 "광저우 1지역" 서브넷에 있으면 [VPC 콘솔](https://console.cloud.tencent.com/vpc)에 로그인하여 해당 VPC를 위해 가용 영역이 "광저우 2지역"인 서브넷을 생성할 수 있습니다.
![](https://main.qcloudimg.com/raw/d25fc9283b76f114a772bebb1b703548.png)
![](https://main.qcloudimg.com/raw/74ffa38cc8774e6534617aed6f4476df.png)
![](https://main.qcloudimg.com/raw/344f0c3bfce47031137fa66351bbb11c.png)

서브넷 생성 완료 후 CFS 콘솔로 돌아와 광저우 2지역의 리소스를 생성할 때 해당 VPC 및 방금 생성한 서브넷을 선택합니다. 이러면 기존에 VPC 광저우 1지역 서브넷에 있는 CVM은 CFS 파일 시스템에 바로 탑재됩니다. [파일 시스템 탑재 도움말](https://cloud.tencent.com/document/product/582/11523)을 참조하십시오.


## VPC 간 및 영역 간 접근
CFS는 다음 시나리오를 지원하기 때문에 리소스 접근을 진행할 수 있습니다.

- 여러 대의 CVM이 각기 다른 VPC에 분포되어 있지만 파일 저장을 공유해야 할 경우. 
- CVM과 CFS가 다른 VPC에 있는 경우.
- CVM과 CFS가 다른 지역에 분포되어 있는 경우(다만, 최상의 접근 성능을 위해 CVM은 CFS와 동일 지역에 있길 권장함)

VPC-A/VPC-B에 분포한 CVM과 VPC-C에 분포한 CFS는 "피어링 연결"을 설정하여 VPC-A, VPC-B, VPC-C 간 상호 접근을 실현할 수 있습니다. [피어링 연결 설정 방법](https://cloud.tencent.com/document/product/215/5000)을 참조하십시오.


## 네트워크 간 접근
여러 대의 CVM이 기본 네트워크 또는 VPC에 분포되어 있으며 파일 저장을 공유해야 할 때, VPC에서 CFS 파일 시스템을 생성할 수 있습니다.
- 기본 네트워크의 CVM과 VPC 간 CFS 공유: "기본 네트워크 상호 연결" 설정을 통해 기본 네트워크의 CVM과 VPC 간의 리소스 상호 접근을 실현할 수 있습니다. [기본 네트워크 상호 연결 설정 방법](https://cloud.tencent.com/document/product/215/5002)을 조회하십시오.
- VPC-A의 CVM과 VPC-B 간 CFS 공유: 이전 섹션의 설정 방식을 참조하십시오.

>!
>- 기본 네트워크에 있는 CFS는 VPC 내 CVM과의 상호 연결을 지원하지 않습니다.
>- 클라이언트와 CFS는 각자 기본 네트워크와 VPC 네트워크에 있지만 다른 지역에 있으며 상호 연결을 지원하지 않습니다.

