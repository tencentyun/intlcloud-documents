## 기능 소개
CDN이 제공한 IP 바인딩 조회 툴을 통해 IP가 위치한 가속 서비스 가용 영역, 행정구역 및 통신사와 지정된 IP는 Tencent Cloud CDN의 글로벌 가속 노드인지를 조회할 수 있습니다.
## 적용 시나리오
해당 툴을 사용하여 환경 문제를 해결할 수 있으므로 사용자 액세스에 이상이 있을 경우 클라이언트가 요청한 실제 액세스 IP를 여기서 조회합니다.
- Tencent Cloud CDN에 속하지 않으면 리졸브 구성이 비정상적일 수 있으므로 도메인 리졸브 서비스를 ISP에 연결하여 CNAME 구성이 정상인지 확인하십시오.
- Tencent Cloud CDN에 속할 경우 노드 서비스 상태를 조회하여 노드 활성화/비활성화 요청이 중단되었는지 확인할 수 있습니다.

## 운영 가이드
### 조회 방식
[CDN Console](https://console.cloud.tencent.com/cdn)에 로그인하고 왼쪽 목록에서 [Inspect Tool]>[Verify Tencent Cloud CDN IP]를 선택하여 기능 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/7c72a39a1c0f33e633057d02af9c3a6f.png)
### 사용 규제
- 텍스트 상자에 검증이 필요한 IP 주소를 한 줄에 하나씩 입력하십시오.
- 한 번에 최대 IP 20개를 검증할 수 있습니다.
- IPV4, IPV6 주소 검증을 지원합니다.
- 전 세계적으로 가속 노드 검증을 지원하며 중국 국내 노드는 지역 소재 통신사 데이터로 리턴되고 해외 노드는 소재 국가 데이터로 리턴됩니다.
- 노드 조회로 **3시간 내**에 서비스 상태를 변경할 수 있으므로 활성화/비활성화에 변경이 있는 경우 대응하는 작업 시간을 조회할 수 있습니다.

## 사용 사례
### IP가 중국에 바인딩되는 경우
![](https://main.qcloudimg.com/raw/92a04bfdc0905c9be0465d3dc4825dd3.png)
### IP가 해외에 바인딩되는 경우
![](https://main.qcloudimg.com/raw/6a2e1b6f94362d5508ed98a52bd2d125.png)
### IPv6 바인딩 조회
> IPv6 가속은 현재 베타 신청 단계에 있으며 IPv6가 가속 수요가 있는 경우 [신청 제출](https://cloud.tencent.com/apply/p/own2eu41dg8)을 클릭하십시오.
>
![](https://main.qcloudimg.com/raw/7e88553e81f01e86fd4325c3d433fbca.png)







