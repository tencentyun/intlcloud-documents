
### 전체 아키텍처
이 섹션에서는 TKE 시스템의 설계 및 구현에 대해 설명합니다. 제품 아키텍처는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/8ecde8fe39d8f4cc65b9622823ab1058.png)

### 아키텍처 설명
1.  TKE는 Kubernetes를 기반으로 조정 및 확장되므로 기본 Kubernetes 기능을 지원합니다.
2.  Tencent Cloud의 Kubernetes 플러그인을 사용하면 Tencent Cloud에서 Kubernetes 클러스터를 빠르게 구축할 수 있습니다.
3.  TKE는 Kubernetes의 상위 계층에서 클러스터 관리, 애플리케이션 관리, CI/CD 및 기타 고급 기능을 제공합니다.



### 모듈 설명
1. **TKE 콘솔 및 TencentCloud API**: 콘솔, kubectl 또는 API를 사용하여 클러스터 및 서비스를 조작할 수 있습니다.
2. **이미지 서비스 CCR 모듈**: Tencent Cloud에서 제공하는 이미지 서비스 모듈을 통해 이미지를 업로드 및 다운로드할 수 있습니다.
3. **TKE 모듈**: TKE의 핵심 모듈이며 클러스터 및 서비스 CRUD 작업을 포함합니다.

