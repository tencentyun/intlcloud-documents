본 문서에서는 TKE를 사용하여 컨테이너 클러스터를 빠르게 생성하는 방법을 설명합니다.


## 1단계: Tencent Cloud 계정 생성
이미 Tencent Cloud 계정이 있는 경우는 이 단계를 생략할 수 있습니다.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/378/17985" target="_blank"  style="color: white; font-size:13px;">가입하려면 여기를 클릭</a></div>

## 2단계: 온라인 충전
TKE 서비스 자체는 현재 무료이지만 실제로 사용하는 클라우드 리소스에 대해서는 요금이 부과됩니다. 본 문서에서 생성할 것은 ‘관리 클러스터’이며 클러스터의 작업자 노드, 영구 저장소 및 서비스에 바인딩된 CLB 등에 대해 비용을 지불해야 합니다. 관련 작업에 대한 자세한 내용은 [결제 방법](https://intl.cloud.tencent.com/document/product/555/7425)을 참고하십시오.



## 3단계: TKE 승인
[Tencent Cloud 콘솔](https://console.cloud.tencent.com/)을 열고 **Tencent Cloud 서비스** > **TKE**를 선택하여 TKE 콘솔로 들어가 프롬프트에 따라 TKE를 인증합니다. 이미 TKE를 승인했다면 이 단계를 건너뛰십시오.

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster?rid=1" target="_blank"  style="color: white; font-size:13px;">승인하려면 여기를 클릭</a></div>


## 4단계: 클러스터 생성
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster/create?rid=1" target="_blank"  style="color: white; font-size:13px;">입력하려면 여기를 클릭</a></div>

### 클러스터 정보
‘클러스터 정보’ 페이지에서 클러스터 이름을 입력하고 클러스터 지역, 클러스터 네트워크, 컨테이너 네트워크를 선택합니다. 다른 기본 옵션을 변경하지 않은 상태로 유지하고 아래와 같이 **다음**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/48966b45ba60fe9116bb58edec3c58dd.png)

 - **클러스터 이름**: 클러스터 이름을 입력합니다. 이 문서에서는 ‘test’를 클러스터 이름으로 사용합니다.
 - **리전**: 가장 가까운 리전을 선택합니다. 
 - **클러스터 네트워크**: 노드 네트워크 주소 범위 내의 IP 주소를 클러스터의 서버에 할당합니다. 여기에서 VPC를 선택합니다.
 - **컨테이너 네트워크**: 컨테이너 네트워크 주소 범위 내의 IP 주소를 클러스터의 컨테이너에 할당합니다. 여기에서 사용 가능한 컨테이너 네트워크를 선택합니다.


### 모델 선택
‘모델 선택’ 페이지에서 청구 모드를 확인하고, 가용존과 해당 서브넷을 선택하고, 노드 모델을 확인하고 아래와 같이 **다음**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ef0eddd2e2a0ea044774c4ee65d0a2ef.png)

- **노드 소스**: **노드 추가** 또는 **기존 노드**를 선택할 수 있습니다. 여기에서 ‘노드 추가’를 선택합니다.
- **Master 노드**: **관리** 및 **자체 배포**의 두 가지 클러스터 모드 중에서 선택할 수 있습니다. 여기에서 ‘관리”를 선택합니다.
- **청구 모드**: **종량제**만 선택할 수 있습니다. 여기에서 ‘종량제’를 선택합니다.
- **Worker 구성**: 가용존과 해당 서브넷을 선택하고 노드 모델을 확인하기만 하면 됩니다. 다른 기본 설정은 변경하지 마십시오.
  - **가용존**: 여기에서 ‘광저우 영역3’을 선택합니다.
  - **노드 네트워크**: 여기에서 현재 VPC의 서브넷을 선택합니다.
  - **모델**: 여기에서 ‘S1.SMALL1(표준 S1, 1코어1GB)’을 선택합니다.

### CVM 설정
‘CVM 구성’ 페이지에서 로그인 방법을 선택하고 다른 기본 설정을 변경하지 않고 **다음**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/83501db19590eccb230c482ae37bd3a9.png)

- **로그인 방법**: **SSH 키 쌍**, **임의 비밀번호** 또는 **사용자 정의 비밀번호**를 선택할 수 있습니다. 여기서 ‘임의의 비밀번호’를 선택합니다.

### 컴포넌트 구성
‘컴포넌트 구성’ 페이지에서 스토리지, 모니터링, 이미지 등 필요한 컴포넌트를 선택할 수 있습니다. 이러한 컴포넌트가 필요하지 않은 경우 **다음**을 직접 클릭합니다. 여기서 컴포넌트를 설치하지 않고 다른 기본 설정을 변경하지 않도록 선택합니다.

### 정보 확인
‘정보 확인’ 페이지에서 클러스터에 대해 선택한 구성 정보 및 청구 모드를 확인하고 아래 그림과 같이 **완료**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bebdbb0524ba191175daa935b9d7d986.png)


요금을 지불한 후 첫 번째 클러스터를 생성할 수 있습니다. 그런 다음 [TKE 콘솔](https://console.cloud.tencent.com/tke2/cluster?rid=1)에서 생성한 관리형 클러스터를 볼 수 있습니다.

## 5단계: 클러스터 보기
[클러스터 목록](https://console.cloud.tencent.com/tke2/cluster?rid=1)에서 생성된 클러스터를 볼 수 있습니다. 클러스터 ID를 클릭하여 세부 정보 페이지로 들어가면 아래와 같이 ‘기본 정보’ 페이지에서 클러스터, 노드 및 네트워크 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0f36c74372186d3efdf1ba2f1751f228.png)




## 6단계: 클러스터 삭제
일단 시작되면 클러스터는 리소스를 소비하기 시작합니다. 불필요한 비용을 피하기 위해 아래 단계에 따라 모든 리소스를 지울 수 있습니다.

1. 왼쪽 사이드바에서 **클러스터**를 선택합니다. ‘클러스터 관리’ 페이지에서 삭제할 클러스터가 있는 raw의 오른쪽에 있는 **더 보기** > **삭제**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9431c8e5c0038ec85e1e04edbc217b0c.png)
2. ‘클러스터 삭제’ 팝업 창에서 관련 정보를 확인하고 **확인**을 클릭하면 클러스터가 삭제됩니다.





## 후속 작업: 클러스터 사용
이제 본 문서를 읽은 후 TKE에서 클러스터를 생성 및 삭제하는 방법을 알게 되었습니다. 생성된 클러스터에서 워크로드를 설정하고 서비스를 생성할 수 있습니다. 일반적인 작업은 다음과 같습니다.
- [간단한 Nginx 서비스 생성](https://intl.cloud.tencent.com/document/product/457/7851)
- [단일 포드 WordPress](https://intl.cloud.tencent.com/document/product/457/7205)
- [TencentDB를 사용하는 WordPress 서비스](https://intl.cloud.tencent.com/document/product/457/7447)
- [수동으로 Hello World 서비스 구축](https://intl.cloud.tencent.com/document/product/457/7204)
- [간단한 Web 애플리케이션 구축](https://intl.cloud.tencent.com/zh/document/product/457/6996)


## 문제 해결
전체 과정에서 문제가 발생하면 [티켓 제출](https://console.intl.cloud.tencent.com/workorder)하여 저희에게 연락하십시오.
