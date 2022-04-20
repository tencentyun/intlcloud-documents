## 작업 시나리오
WordPress는 PHP로 개발된 블로그 플랫폼입니다. 콘텐츠 관리 시스템으로 사용하거나 PHP 및 MySQL 데이터베이스를 지원하는 서비스에서 웹사이트를 만드는 데 사용할 수 있습니다.

본 문서에서는 Docker Hub의 공식 `wordpress` 이미지를 사용하여 공개적으로 액세스 가능한 WordPress 웹 사이트를 만드는 방법을 설명합니다.


## 전제 조건
>!
>- `wordpress` 이미지에는 WordPress의 모든 운영 환경이 포함되어 있어 서비스를 직접 풀링해서 생성할 수 있습니다.
>- 단일 Pod가 있는 WordPress는 테스트 목적으로만 사용되므로 영구 데이터 저장을 보장할 수 없습니다. 자체 구축한 MySQL 또는 TencentDB를 사용하여 데이터를 저장하는 것이 좋습니다. 자세한 내용은 [TencentDB를 사용하는 WordPress 서비스](/doc/product/457/7447)를 참고하십시오. 
>
- [Tencent Cloud 계정 등록](https://intl.cloud.tencent.com/register)을 완료합니다.
- 클러스터를 생성했습니다. 클러스터 생성 방법에 대한 자세한 내용은 [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637)를 참고하십시오.

## 작업 단계
### WordPress 서비스 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 **[Cluster](https://console.cloud.tencent.com/tke2/cluster)**를 선택합니다.
2. ‘Cluster Management’ 페이지에서 서비스를 생성할 클러스터의 ID를 클릭하여 아래 그림과 같이 클러스터의 ‘Deployment’ 페이지로 이동한 후 **Create**를 클릭합니다.
![](https://main.qcloudimg.com/raw/1e32ac2e0e8d99315305f1b55034d691.png)
3. ‘Create Workload’ 페이지에서 아래 그림과 같이 워크로드의 기본 정보를 지정합니다.
![](https://main.qcloudimg.com/raw/a1c6b34a108a7a24d3f22e7048dec3ef.png)
 - **Workload Name**: 생성할 워크로드의 이름을 입력합니다. 이 예시에서는 wordpress를 사용합니다.
 - **Description**: 관련 워크로드 정보를 지정합니다.
 - **Tag**: key = value 키 값 쌍을 지정합니다. 기본값은 k8s-app = **wordpress**입니다.
 - **Namespace**: 요구 사항에 따라 네임스페이스를 선택합니다.
 - **Type**: 요구 사항에 따라 유형을 선택합니다.
 - **Volume**: 요구 사항에 따라 워크로드가 탑재되는 볼륨을 설정합니다. 자세한 내용은 [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)를 참고하십시오.
4. 아래 지침에 따라 **Containers in the Pod**를 설정합니다.
주요 매개변수는 다음과 같이 설명됩니다. 다른 매개변수의 기본값을 유지할 수 있습니다.
 - **Name**: 사용자 정의 컨테이너 이름을 입력합니다. 이 예시에서는 test가 사용됩니다.
 - **Image**: `wordpress`를 입력합니다.
 - **Image Tag**: latest를 입력합니다.
 - **Image Pull Policy**: 세 가지 정책을 사용할 수 있습니다. 필요에 따라 정책을 선택합니다. 본 예시에서는 기본 정책이 사용됩니다.
   이미지 가져오기 정책을 설정하지 않고 이미지 태그가 비어 있거나 `latest`으로 설정된 경우 Always 정책이 사용됩니다. 그렇지 않으면 IfNotPresent 정책이 사용됩니다.
    - **Always**: 항상 원격 끝에서 이미지를 가져옵니다.
    - **IfNotPresent**: 기본적으로 로컬 이미지가 사용됩니다. 사용 가능한 로컬 이미지가 없으면 이미지를 원격으로 가져옵니다.
    - **Never**: 로컬 이미지만 사용합니다. 사용 가능한 로컬 이미지가 없으면 예외가 발생합니다.
6. 지시에 따라 서비스의 Pod 수를 설정합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/649c9a62a29a77d09451e6d0dc487d58.png)
 - **Manual adjustment**: 포드 수를 설정합니다. 이 예시에서 포드 수는 1로 설정되어 있습니다. ‘+’ 또는 ‘-’를 클릭하여 포드 수를 변경할 수 있습니다.
 - **Auto Adjustment**: 설정 조건 중 하나라도 충족되면 pod 수가 자동으로 조정됩니다. 자세한 내용은 [Automatic Scaling Basic Operation](https://intl.cloud.tencent.com/document/product/457/32424) 기본 작업을 참고하십시오.
8. 아래 지침에 따라 워크로드에 대한 **Access Setting (Service)**를 구성합니다.
 - **Service**: 활성화를 선택합니다.
 - **Service Access**: ‘LoadBalancer(public network)’를 선택합니다.
 - **Load Balancer**: 요구 사항에 따라 선택합니다.
 - **Port Mapping**: TCP를 선택하고 컨테이너 포트와 서비스 포트를 모두 80으로 설정합니다.
>!서비스가 속한 클러스터의 보안 그룹은 노드 네트워크와 컨테이너 네트워크를 인터넷에 개방해야 합니다. 또한 인터넷에 포트 30000 - 32768을 개방해야 합니다. 그렇지 않으면 TKE를 사용하지 못할 수 있습니다. 자세한 내용은 [TKE 보안 그룹 설정](https://intl.cloud.tencent.com/document/product/457/9084)을 참고하십시오.
9. **Create Workload**을 클릭하여 WordPress 서비스를 생성합니다.


###  WordPress 서비스에 액세스

다음 두 가지 방법 중 하나를 사용하여 WordPress 서비스에 액세스할 수 있습니다.

#### CLB IP 주소를 사용하여 액세스
1. 왼쪽 사이드바에서 **[Cluster](https://console.cloud.tencent.com/tke2/cluster)**를 클릭하여 ‘Cluster Management’ 페이지로 이동합니다.
2. WordPress 서비스가 속한 클러스터의 ID를 클릭하고 **Service and Route** > **Service**를 선택합니다.
3. 서비스 관리 페이지에서 아래 그림과 같이 WordPress 서비스의 CLB IP 주소를 복사합니다.
![](https://main.qcloudimg.com/raw/8a8ea1dc181ab31660313ed0883bc980.png)
4. 브라우저에 CLB IP 주소를 붙여넣고 ‘**Enter**’ 키를 눌러 서비스에 액세스합니다.

#### 서비스 이름을 사용하여 WordPress 서비스에 액세스
클러스터의 다른 서비스 또는 컨테이너는 서비스 이름을 사용하여 WordPress 서비스에 액세스할 수 있습니다.

### WordPress 서비스 확인
서비스 생성 후 서비스에 접속하면 아래 그림과 같이 WordPress 서버 설정 페이지가 나타납니다.
![](https://main.qcloudimg.com/raw/4ccbffc42a7f9381e2595175ea32be65.png)

### 더 많은 WordPress 설정
컨테이너 생성에 실패한 경우 [Event FAQ](https://intl.cloud.tencent.com/document/product/457/8187)를 참고하십시오.

