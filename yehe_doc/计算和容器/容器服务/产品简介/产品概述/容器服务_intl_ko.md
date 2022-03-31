## 제품 소개
Tencent Kubernetes Engine(TKE)은 관리되는 CVM 인스턴스 클러스터에서 애플리케이션을 쉽게 실행할 수 있도록 하는 높은 확장성과 성능을 갖춘 컨테이너 관리 서비스입니다. 이 서비스를 사용하면 클러스터 관리 인프라의 설치, OPS 및 확장에서 해방됩니다. 또한 간단한 API 호출을 통해 Docker 애플리케이션을 시작 및 종료하고 클러스터 상태를 쿼리하고 다양한 Tencent Cloud 서비스를 사용할 수 있습니다. 리소스 및 가용성 요구 사항을 기반으로 클러스터의 컨테이너를 정렬하여 비즈니스 또는 애플리케이션별 요구 사항을 충족할 수 있습니다.

기본 Kubernetes를 기반으로 하는 TKE는 개발, 테스트 및 OPS 동안 운영 환경 문제를 해결하고 비용을 절감하고 효율성을 개선하는 데 도움이 되는 컨테이너 지향 솔루션을 제공합니다. 기본 Kubernetes API와 완벽하게 호환되며 Tencent Cloud에서 CBS 및 CLB와 같은 Kubernetes 플러그인을 확장합니다. 또한 TKE는 Tencent Cloud VPC를 기반으로 높은 안정성과 성능을 갖춘 네트워크 솔루션을 제공합니다.

## 용어 사전
다음은 TKE와 관련된 주요 용어에 대한 설명입니다.
- **클러스터**: CVM 인스턴스 및 CLB와 같은 여러 Tencent Cloud 리소스를 포함하여 컨테이너를 실행하는 데 필요한 클라우드 리소스 모음입니다.
- **Pod**: 동일한 저장소 및 네트워크 공간을 공유하는 하나 이상의 연결된 컨테이너 그룹입니다.
- **워크로드**: 전체 라이프사이클 동안 Pod 복제본의 생성, 스케쥴링 및 자동 제어를 관리하는 데 사용되는 Kubernetes 리소스 객체입니다.
- **Service**: 동일한 구성과 이러한 Pod에 액세스하기 위한 규칙을 가진 여러 Pod로 구성된 마이크로 서비스 그룹입니다.
- **Ingress**: Ingress는 외부 HTTP(S) 트래픽을 서비스(Service)로 라우팅하기 위한 규칙 모음입니다.
- **애플리케이션**: helm chart, Tencent Container Registry(TCR), 소프트웨어 서비스를 비롯한 다양한 제품 및 서비스 기능을 제공하는 TKE에 통합된 Helm 3.0과 관련된 기능입니다.
- **이미지 레지스트리**: TKE를 배포하는 데 사용되는 Docker 이미지를 저장합니다.


## 사용 프로세스
다음 그림은 TKE 사용 순서도를 보여줍니다.
![](https://main.qcloudimg.com/raw/4a7b3a025c99e264eda78431ee964552.png)

1. 역할 승인
   TKE 콘솔에 가입하고 로그인한 다음 TKE를 시작할 수 있도록 역할에 관련 리소스에 대한 작업을 수행할 수 있는 권한을 부여합니다.
2. 클러스터 생성
   클러스터를 사용자 지정하거나 템플릿에서 클러스터를 생성할 수 있습니다.
3. 워크로드 배포
   이미지를 배포하거나 YAML 파일을 오케스트레이션하여 워크로드를 배포할 수 있습니다. 자세한 내용은 [워크로드](https://intl.cloud.tencent.com/document/product/457/30662)를 참고하십시오.
4. 모니터링, 업그레이드, 스케일링 등의 작업을 통해 Pod의 라이프사이클을 관리합니다.



## 제품 가격
TKE는 이제 무료이지만 관련 Tencent Cloud 리소스 사용에 대한 비용을 지불해야 합니다. 청구 및 가격 책정에 대한 자세한 내용은 [과금 안내](https://intl.cloud.tencent.com/document/product/457/6770)를 참고하십시오.

## 관련 서비스

- 여러 CVM 인스턴스를 구입하여 TKE 클러스터를 형성할 수 있습니다. 컨테이너는 CVM에서 실행됩니다. 자세한 내용은 [Cloud Virtual Machine 문서](https://intl.cloud.tencent.com/document/product/213)를 참고하십시오.
- 클러스터는 VPC에서 생성할 수 있습니다. 클러스터의 CVM 인스턴스는 서로 다른 가용존의 서브넷에 할당할 수 있습니다. 자세한 내용은 [Virtual Private Cloud 문서](https://intl.cloud.tencent.com/document/product/215)를 참고하십시오.
- CLB를 사용하여 CVM 인스턴스에서 클라이언트의 요청 트래픽을 자동으로 할당한 다음 CVM 인스턴스에서 실행되는 컨테이너로 전달할 수 있습니다. 자세한 내용은 [Cloud Load Balancer 문서](https://cloud.tencent.com/doc/product/214)를 참고하십시오.
– Cloud Monitor를 사용하여 TKE 클러스터 및 Pod의 작업 통계를 모니터링할 수 있습니다. 자세한 내용은 [Cloud Monitor 문서](https://intl.cloud.tencent.com/document/product/248)를 참고하십시오.




