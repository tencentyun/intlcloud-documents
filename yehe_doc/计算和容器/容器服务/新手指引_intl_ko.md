본 문서는 지침에 따라 Tencent Kubernetes Engine(TKE)을 빠르게 이해하고 시작하는 데 도움이 됩니다.

## 1. TKE란 무엇입니까?


기본 Kubernetes 시스템을 기반으로 [TKE](https://intl.cloud.tencent.com/document/product/457/6759)(Tencent Kubernetes Engine)는 확장성이 뛰어난 컨테이너 중심의 고성능 컨테이너 관리 서비스를 제공합니다. 호스팅된 CVM 인스턴스 클러스터에서 애플리케이션을 쉽게 실행할 수 있습니다. Tencent Cloud는 [EKS](https://intl.cloud.tencent.com/document/product/457/34040)(Elastic Kubernetes Service)와 [TKE Edge](https://intl.cloud.tencent.com/document/product/457/35390)(Tencent Kubernetes Engine for Edge)도 제공하므로 필요한 서비스를 선택할 수 있습니다.


TKE를 사용하면 [TKE 콘솔](https://console.cloud.tencent.com/tke2/overview)인 [Kubectl](https://intl.cloud.tencent.com/document/product/457/30639)을 통해 클러스터와 서비스를 조작할 수 있습니다.




## 2. TKE 결제
TKE 서비스 자체는 현재 무료이지만 실제로 사용하는 클라우드 리소스에 대해서는 요금이 부과됩니다. TKE 사용 중 관련 제품에서 발생하는 리소스 요금에 대한 자세한 내용은 [과금 안내](https://intl.cloud.tencent.com/document/product/457/6770)를 참고하십시오.




## 3. TKE 사용
#### 3.1 가입 및 인증
TKE를 사용하기 전에 [Tencent Cloud 계정에 가입](https://intl.cloud.tencent.com/register)하고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료해야 합니다.

#### 3.2 역할 권한 부여
다른 Tencent Cloud 서비스 리소스에 액세스하기 전에 현재 서비스 역할을 승인하고 TKE에 대한 작업 권한을 부여해야 합니다.
Tencent Cloud 콘솔을 열고 **제품**>**Tencent Kubernetes Engine**을 선택하여 [TKE 콘솔](https://console.cloud.tencent.com/tke2/cluster?rid=1)로 들어가 프롬프트에 따라 TKE를 승인합니다. 그 다음 관련 리소스 작업 권한을 얻고 클러스터 생성을 시작할 수 있습니다.



#### 3.3 클러스터 생성
더 많은 유형의 클러스터가 필요한 경우 [탄력적 클러스터 생성](https://intl.cloud.tencent.com/document/product/457/34048) 및 [에지 클러스터 생성](https://intl.cloud.tencent.com/document/product/457/35385)을 참고하십시오.


#### 3.4 워크로드 배포
이미지를 배포하거나 YAML 파일을 조정하여 워크로드를 배포할 수 있습니다.
- 이미지 템플릿을 통해 상태 비저장 워크로드를 배포(Deployment)하려는 경우 단일 포드로 [간단한 Nginx 서비스 생성](https://intl.cloud.tencent.com/document/product/457/7851) 또는 [단일 포드 WordPress 생성](https://intl.cloud.tencent.com/document/product/457/7205)을 참고하십시오.
- 사용자 지정 이미지를 통해 워크로드를 배포하려는 경우 [Hello World 서비스 수동 구축](https://intl.cloud.tencent.com/document/product/457/7204) 지침을 참고하십시오.




#### 3.5 클러스터 작업
TKE는 클러스터, 애플리케이션, 스토리지 및 네트워크를 위한 관리 플랫폼입니다. 더 자세한 정보나 지침은 아래 표를 참고하십시오.

| 필요한 기능 | 참조 페이지 |
|---------|---------|
| Kubernetes 명령줄 도구인 Kubectl을 사용하여 로컬 클라이언트에서 TKE 클러스터에 연결 | [클러스터에 연결](https://intl.cloud.tencent.com/document/product/457/30639) |
| 실행 중인 Kubernetes 클러스터 업그레이드 | [클러스터 업그레이드](https://intl.cloud.tencent.com/document/product/457/30640) |
| 생성된 Kubernetes 클러스터에 포드 추가 | [노드 추가](https://intl.cloud.tencent.com/document/product/457/30652) |
| Kubernetes 클러스터에서 노드 관리| [노드 풀 생성](https://intl.cloud.tencent.com/document/product/457/35901) |
| 콘솔에서 기본 Kubernetes 객체 작업 | [Kubernetes 객체 관리 ](https://intl.cloud.tencent.com/document/product/457/30658) |
| Service를 통해 컨테이너 집합에 대한 고정 액세스 항목 제공 | [Service 기본 기능](https://intl.cloud.tencent.com/document/product/457/36833) |
| Ingress 리소스를 통해 다른 전달 규칙 구성 | [Ingress 관리](https://intl.cloud.tencent.com/document/product/457/37013) |
| TKE의 스토리지 기능 활용 | [스토리지 관리 개요](https://intl.cloud.tencent.com/document/product/457/37769) |
| 컨테이너 네트워크 주소 범위 내의 IP 주소를 클러스터의 컨테이너에 할당 | [컨테이너 네트워크 개요](https://intl.cloud.tencent.com/document/product/457/38966) |
| Kubernetes 클러스터에서 서비스 로그 저장 및 분석 | [로그 수집](https://intl.cloud.tencent.com/document/product/457/32419) |
| Tencent Container Registry(TCR)에서 호스팅되는 프라이빗 이미지를 사용하여 애플리케이션 배포 | [TCR 엔터프라이즈 인스턴스의 컨테이너 이미지를 사용하여 워크로드 생성](https://intl.cloud.tencent.com/document/product/457/36838) |



















## 4. 초보자 가이드	

- **클래식 네트워크에서 TKE를 사용할 수 있습니까?**
아니요. 현재 VPC에서는 TKE를 사용할 수 있지만 클래식 네트워크에서는 사용할 수 없습니다.

- **클러스터에 기존 CVM을 추가할 수 있습니까?**
네. 클러스터를 생성한 후 기존 CVM을 클러스터에 추가할 수 있습니다. 자세한 내용은 [노드 추가](https://intl.cloud.tencent.com/document/product/457/30652#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9)를 참고하십시오.

- **내 서비스가 계속 시작 중인 이유는 무엇입니까?**
컨테이너에서 실행 중인 프로세스가 없으면 서비스가 계속 시작될 수 있습니다. 서비스 시작에 대한 자세한 내용은 [이벤트 FAQ](https://intl.cloud.tencent.com/document/product/457/8187)를 참고하십시오.

- **클러스터를 생성하기 전에 네트워크 계획을 수행하려면 어떻게 해야 합니까?**
클러스터 생성 시 클러스터 네트워크와 컨테이너 네트워크의 IP 범위가 겹치지 않도록 합니다. 일반적으로 VPC 인스턴스의 서브넷을 클러스터의 노드 네트워크로 선택할 수 있습니다. 자세한 내용은 [컨테이너 네트워크 개요](https://intl.cloud.tencent.com/document/product/457/38966)를 참고하십시오.

- **생성된 서비스에 어떻게 액세스합니까?**
다른 액세스 방법에는 다른 액세스 항목이 있습니다. 자세한 내용은 [서비스 관리 개요](https://intl.cloud.tencent.com/document/product/457/36832)의 서비스 액세스 섹션을 참고하십시오.

- **컨테이너는 공용 네트워크에 어떻게 액세스합니까?**
컨테이너가 상주하는 호스트에 공용 IP 주소와 공용 네트워크 대역폭이 있는 경우 컨테이너는 공용 네트워크에 직접 액세스할 수 있습니다. 그렇지 않으면 공용 네트워크에 액세스하기 위해 NAT 게이트웨이가 필요합니다.

- **이미지 생성 방법을 모르는 경우 TKE를 사용할 수 있습니까?**
TKE에 통합된 Helm 3.0과 관련된 기능을 사용하면 helm chart, TCR 및 소프트웨어 서비스와 같은 제품 및 서비스를 만들 수 있습니다. 생성된 애플리케이션은 해당 기능을 제공하기 위해 지정한 클러스터에서 실행됩니다. 자세한 내용은 [애플리케이션 관리](https://intl.cloud.tencent.com/document/product/457/30683)를 참고하십시오.

- **내 서비스에 대한 구성 파일 또는 환경 변수를 어떻게 관리합니까?**
[구성 항목](https://intl.cloud.tencent.com/document/product/457/30675)을 편집하여 구성 파일을 관리할 수 있습니다.

- **서비스는 서로 어떻게 액세스합니까?**
클러스터에서 Namespace가 동일한 서비스는 서로 직접 액세스할 수 있지만 Namespace가 다른 서비스는 `<service-name>.<namespace-name>.svc.cluster.local`을 사용하여 액세스합니다.

## 5. 피드백 및 의견	

TKE 제품 및 서비스를 사용하면서 의문점이나 제안 사항이 있는 경우 다음 채널을 통해 피드백을 제출할 수 있습니다. 전담 직원이 귀하의 문제를 해결하기 위해 연락을 드릴 것입니다.
- 링크, 내용, API 오류 등 제품 문서에 문제가 발생하는 경우 문서 페이지 오른쪽 [문서 피드백]을 클릭하거나 문제가 있는 내용을 선택하여 피드백을 보낼 수 있습니다.
- 제품 관련 문제가 발생한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청할 수 있습니다.

