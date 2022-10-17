>?
>- IPv6 NAT64 CLB는 베이징, 상하이, 광저우의 세 리전에서만 생성할 수 있습니다.
>- IPv6 구현은 인터넷 전반에 걸쳐 아직 예비 단계에 있습니다. 접속 실패 시 [티켓을 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1)하십시오. SLA는 베타 테스트 기간 동안 보장되지 않습니다.
>

CLB는 IPv6 NAT64 CLB 인스턴스 생성을 지원합니다. Tencent Cloud는 IPv6 공개 IP 주소, 즉 IPv6 에디션의 VIP를 인스턴스에 할당하고 VIP는 IPv6 클라이언트의 요청을 실제 IPv4 CVM 인스턴스로 포워딩합니다.

## IPv6 NAT64 CLB 인스턴스란 무엇입니까?
IPv6 NAT64 CLB 인스턴스는 IPv6 NAT64 전환 기술을 기반으로 구현된 로드 밸런서입니다. IPv6 NAT64 CLB 인스턴스를 통해 IPv6 사용자는 IPv6 수정 없이 리얼 서버에 빠르게 액세스할 수 있습니다.

## IPv6 NAT64 CLB 아키텍처
IPv6 NAT64 CLB 아키텍처는 아래와 같습니다.
![](https://main.qcloudimg.com/raw/e86896cc8286b53e8198facc8d28076f.png)
IPv6 NAT64 CLB가 IPv6 네트워크에서 액세스되면 CLB는 IPv6 주소를 IPv4 주소로 원활하게 변환하여 기존 서비스에 적응할 수 있습니다.

## IPv6 NAT64 CLB 장점
Tencent Cloud IPv6 NAT64 CLB는 비즈니스가 IPv6에 빠르게 연결할 수 있도록 지원할 때 다음과 같은 이점이 있습니다.
- **빠른 액세스:** CLB를 사용하면 몇 초 만에 IPv6에 연결할 수 있으며 구입 즉시 사용할 수 있습니다.
- **원활한 비즈니스 전환:** 비즈니스를 IPv6으로 원활하게 전환하려면 리얼 서버에 필요한 수정 없이 클라이언트만 전환하면 됩니다. IPv6 NAT64 CLB는 IPv6 클라이언트의 액세스를 지원하고 IPv6 메시지를 IPv4 메시지로 변환합니다. IPv6 전환은 여전히 원래 방식으로 작동하는 리얼 서버의 애플리케이션에서는 감지할 수 없습니다.
- **사용 용이성:** IPv6 NAT64 CLB는 IPv4 CLB 순서도와 호환되며 추가 학습 비용이 발생하지 않고 사용하기 쉽습니다.

## 운영 가이드
### IPv6 NAT64 CLB 인스턴스 생성
1. Tencent Cloud 콘솔에 로그인하여 [CLB 구매 페이지](https://buy.intl.cloud.tencent.com/lb)로 이동합니다.
2. 다음 매개변수에 대한 옵션을 올바르게 선택하십시오.
 - 과금 방식: 종량제를 지원합니다.
 - 리전: 베이징, 상하이, 광저우만 지원됩니다.
 - 인스턴스 유형: CLB.
 - 네트워크 유형: 공중망.
 - IP 버전: IPv6 NAT64.
 - 네트워크: VPC.
 - 기타 구성은 일반 인스턴스 구성과 동일합니다.
3. 위의 항목을 구성한 후 **즉시 구매**를 클릭하고 방금 구매한 IPv6 CLB 인스턴스를 볼 수 있는 [인스턴스 관리 페이지](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)로 돌아갑니다.


### IPv6 NAT64 CLB 사용
[CLB 콘솔](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)에 로그인하고 인스턴스 ID를 클릭하여 세부 정보 페이지로 이동합니다. 리스너 관리 탭에서 리스너 및 포워딩 규칙을 구성하고 CVM 인스턴스를 바인딩할 수 있습니다. 자세한 내용은 [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975)를 참고하십시오.
![](https://main.qcloudimg.com/raw/2cacac7c34a7fa241dbd6f9127570391.png)

## 관련 문서
[Obtaining Real Client IPs via TOA in Hybrid Cloud Deployment ](https://intl.cloud.tencent.com/document/product/214/45530)
