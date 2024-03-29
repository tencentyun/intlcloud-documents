## 소개

클라우드 네이티브 데이터 레이크 스토리지를 사용하면 TKE(Tencent Kubernetes Engine)에 COS(Cloud Object Storage) 기반 데이터 레이크 스토리지 서비스를 빠르게 배포할 수 있으며, 그 다음 TKE 또는 EKS 클러스터에서 다양한 비즈니스에 필요한 빅 데이터 및 AI 서비스 응용 프로그램을 배포할 수 있습니다. 또한 GooseFS를 사용하여 대규모 분산 스토리지 서비스에 연결할 수도 있습니다.


### 개념 및 용어

다음은 클라우드 네이티브 데이터 레이크 스토리지의 몇 가지 기본 **개념 및 용어**입니다.
- **환경**: 컴퓨팅 클러스터와 스토리지 서비스 간의 매핑을 유지합니다. 환경에서 컴퓨팅 클러스터 및 스토리지 서비스를 균일하게 관리하는 것이 좋습니다.
>! TKE 콘솔에서 컴퓨팅 클러스터를 삭제해야 하는 경우 먼저 데이터 레이크 환경을 지우는 것이 좋습니다.
>
- **컴퓨팅 클러스터**: 다양한 컴퓨팅 비즈니스를 운영하기 위한 컨테이너 클러스터입니다. TKE 또는 EKS 클러스터를 생성할 수 있습니다.
- **스토리지 서비스**: 컴퓨팅을 위해 다양한 유형의 데이터를 저장하는 COS를 말합니다.
- **애플리케이션 마켓**: Flink 및 Spark와 같은 다양한 컴퓨팅 비즈니스를 위한 애플리케이션 구성 요소가 있습니다. 환경을 생성할 때 필요에 따라 애플리케이션을 선택할 수 있습니다.
>! 컨테이너 클러스터가 종료되면 해당 클러스터에 배포된 애플리케이션도 종료됩니다. 유의하여 진행하십시오.
>
- **GooseFS**: 다양한 기본 버킷을 관리하고 컴퓨팅 클러스터에서 자주 액세스하는 데이터를 캐시하여 컴퓨팅을 가속화합니다.

다음 문서에서 몇 가지 기본 정보를 얻을 수 있습니다.
- COS: [시작하기](https://intl.cloud.tencent.com/document/product/436/32955)에서 버킷을 생성하고 버킷에서 파일을 업로드/다운로드하는 방법을 설명합니다.
- TKE: [시작하기](https://intl.cloud.tencent.com/document/product/457/40029)에서 TKE 또는 EKS 클러스터를 생성하는 방법을 설명합니다.
- 애플리케이션 시장: [Application Market](https://intl.cloud.tencent.com/document/product/457/37706)은 TKE 클러스터에서 애플리케이션을 생성하고 배포하는 방법을 설명합니다.
- GooseFS: [GooseFS on TKE 클라우드 네이티브 활용](https://www.tencentcloud.com/document/product/436/42228)은 클러스터에서 GooseFS를 관리하는 방법을 설명합니다.


## 전제 조건

- 현재 클라우드 네이티브 데이터 레이크 스토리지는 얼로우리스트를 통해 제공됩니다. 사용하시려면 [문의하기](https://intl.cloud.tencent.com/contact-sales)에서 신청하십시오.
- 클라우드 네이티브 데이터 레이크 스토리지는 TKE 및 COS에 의존하며 **컴퓨팅 및 스토리지 서비스 작업 권한**이 필요합니다. 서브 계정으로 로그인하는 경우 서브 계정에 최소한 다음 권한이 있는지 확인하십시오.
 - COS 버킷 및 파일을 조작할 수 있는 권한입니다.
    - 버킷 조작 권한: 버킷 구성을 관리해야 하는 경우 루트 계정에서 해당 권한을 얻습니다. 일반적으로 이 권한은 데이터 읽기/쓰기에 영향을 미치지 않으며 추가 구성이 필요하지 않습니다. [QcloudCOSBucketConfigRead](https://console.cloud.tencent.com/cam/policy/detail/5295084&QcloudCOSBucketConfigRead&2) 정책과 같은 읽기 권한만 부여하면 됩니다.
    - 파일 조작 권한: 일반적으로 컴퓨팅 작업을 수행하려면 버킷에서 파일을 읽거나 써야 합니다. 루트 계정에서 [QcloudCOSDataFullControl](https://console.cloud.tencent.com/cam/policy/detail/5294998&QcloudCOSDataFullControl&2) 정책과 같은 전체 액세스 권한을 얻을 수 있습니다. 또는 루트 계정은 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 권한을 부여할 수 있습니다.
 - 컨테이너 클러스터 관리 권한:
    - 클러스터 작업 권한: 일반적으로 클러스터 생성 및 조작 권한을 부여해야 합니다. 자세한 지침은 [Using TKE Preset Policy Authorization](https://intl.cloud.tencent.com/document/product/457/37363)을 참고하십시오.
    - 클러스터 관리 권한: TKE는 Kubernetes RBAC에 연결할 수 있는 권한 부여 모드를 제공하므로 서브 계정 액세스를 세분화된 방식으로 제어할 수 있습니다. 서브 계정 작업에도 TKE Kubernetes 객체 레벨 권한 제어가 적용됩니다.
    - 애플리케이션 마켓 조작 권한: 애플리케이션 마켓은 TCR 서비스의 운영에 의존합니다. 서브 계정을 인증하는 방법에 대한 자세한 지침은 [TKE Image Registry Resource-level Permission Settings](https://intl.cloud.tencent.com/document/product/457/11527)를 참고하십시오.


## 작업 단계

다음은 환경 생성, 클러스터 연결, 컴퓨팅 애플리케이션 배포, 스토리지 서비스 연결 및 환경 관리를 포함한 단계를 자세히 설명합니다.

1.  [COS 콘솔](https://console.cloud.tencent.com/cos)에 로그인합니다.
2.  왼쪽 사이드바에서 **클라우드 네이티브 데이터 레이크 스토리지**를 클릭합니다.
3.  클라우드 네이티브 데이터 레이크 스토리지 페이지에서 기능 개요 및 배포 가이드를 볼 수 있습니다.
 - 배포 가이드는 기본적으로 표시되며, 오른쪽 상단 모서리의 **가이드 닫기**를 클릭하여 사용하지 않도록 설정할 수 있습니다.
 - 환경 목록 페이지에서 검색이 가능합니다. 다음과 같이 기존 환경을 조작할 수 있습니다.
     - **환경 이름**을 클릭하면 환경 세부 정보 페이지로 이동하여 환경을 관리할 수 있습니다.
     - **관련 클러스터**를 클릭하여 TKE 콘솔에서 클러스터 세부 정보 페이지로 들어갑니다.
     - 관련 버킷을 클릭하면 버킷 페이지로 이동하여 파일 정보를 볼 수 있습니다.
4.  **환경 생성**을 클릭합니다.
환경을 생성하기 전에 대상 컨테이너 컴퓨팅 클러스터를 선택하고 다음 매개변수를 구성합니다.
 - **환경 이름**: 최대 63자를 포함할 수 있으며 전역적으로 고유해야 합니다.
 - **리전**: 컨테이너 클러스터의 리전을 선택합니다.
 - **클러스터 유형**: TKE 또는 EKS일 수 있습니다. 현재 리전에 클러스터가 없는 경우 **컨테이너 클러스터 생성**을 클릭하여 TKE 콘솔에서 클러스터를 생성할 수 있습니다.
 - **클러스터**: **지정된 리전** 및 **지정된 클러스터 유형** 조건에 따라 컴퓨팅 애플리케이션을 배포하고 컴퓨팅 작업을 실행하기 위한 클러스터의 이름입니다.
 - **컴퓨팅 애플리케이션**: 컴퓨팅 작업을 실행하는 데 필요한 애플리케이션 서비스를 나타냅니다. 현재 Flink, big-data-suite, colocation, airflow, pytorch 및 spark-operator 애플리케이션이 기본적으로 지원됩니다. 필요에 따라 하나 또는 여러 개의 애플리케이션을 선택할 수 있습니다. 사용자 지정 애플리케이션을 배포하려면 TKE 콘솔로 이동하여 직접 배포할 수 있습니다.
5.  **다음**을 클릭하여 **버킷 구성** 페이지로 이동합니다.
이 페이지에서 컴퓨팅 클러스터에 대해 다른 버킷을 구성할 수 있습니다. 기본적으로 GooseFS는 컴퓨팅 가속을 위해 컴퓨팅 클러스터의 로컬 노드에서 버킷 및 캐싱 데이터를 관리하는 데 사용할 수 있습니다. 다음 매개변수를 구성해야 합니다.
 - 리전: 기본적으로 컴퓨팅 클러스터의 리전이며 편집할 수 없습니다. 리전에 컴퓨팅 작업에 사용할 수 있는 버킷이 없는 경우 **버킷 생성**을 클릭하여 버킷을 생성할 수 있습니다.
 - 버킷: 지정된 리전에서 여러 버킷을 선택할 수 있습니다. 버킷의 지정된 파일 디렉터리만 마운트할 수도 있습니다.
>! 전체 버킷을 마운트하는 경우 두 번째 입력 상자를 무시할 수 있습니다. 디렉터리를 지정해야 하는 경우 `prefix/*` 형식으로 디렉터리 이름을 입력합니다.
>
 - GooseFS 활성화: GooseFS는 컴퓨팅 작업을 가속화합니다. 기본적으로 활성화되어 있으며 수정할 수 없습니다. 추가 비용은 발생하지 않습니다.
6.  **다음**을 클릭하여 **GooseFS 애플리케이션 구성** 페이지로 이동합니다.
데이터 레이크 환경에서 모든 컴퓨팅 작업은 GooseFS를 통해 COS에 액세스해야 합니다. 따라서 지정된 버킷의 secretId 및 secretKey에 액세스할 수 있는 권한을 GooseFS에 부여해야 합니다.
7.  **다음**을 클릭하고 정보를 확인합니다.
8.  구성 항목을 수정하려면 **수정**을 클릭합니다. 모든 것이 올바른지 확인한 후 **환경 생성**을 클릭합니다. 그 다음 **환경 목록으로 돌아가서 새로고침**하면 새로 생성된 환경을 볼 수 있습니다.
**환경을 삭제**하려면 환경 목록에서 **삭제**를 클릭하고 팝업 창에서 삭제를 확인합니다.
9. 목록에서 환경 이름을 클릭하여 **기본 정보** 페이지로 이동합니다.
환경, 컴퓨팅 클러스터 및 버킷 정보를 설명하는 세 가지 보기를 사용할 수 있습니다.
 - 환경 정보: 환경의 이름, 리전, 연결된 컴퓨팅 클러스터, 스토리지 서비스, 생성 시간을 표시합니다.
 - 컴퓨팅 클러스터 정보: 컴퓨팅 클러스터의 이름, 노드 수, CPU, 메모리, GPU 사용량을 표시합니다. 세부 정보 보기를 클릭하여 TKE 콘솔에 들어가 컴퓨팅 클러스터 세부 정보를 볼 수 있습니다.
 - 버킷 정보: 컴퓨팅 클러스터와 연결된 버킷의 이름, 파일 URL, GooseFS 상태를 표시합니다. 세부 정보 보기를 클릭하여 스토리지 서비스의 세부 정보를 볼 수 있습니다.

이제 데이터 레이크 환경 생성을 완료했습니다.
