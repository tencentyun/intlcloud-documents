## 작업 시나리오
본 문서는 컨테이너 클러스터에서 Nginx 서비스를 빠르게 생성하는 방법을 설명합니다.

## 전제 조건
- [Tencent Cloud 계정 등록](https://intl.cloud.tencent.com/register)을 완료합니다.
-  클러스터를 생성합니다. 자세한 내용은 [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637)를 참고하십시오.

## 작업 단계

### Nginx 서비스 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. ‘Cluster Management’ 페이지에서 서비스를 생성할 클러스터의 ID를 클릭하여 클러스터의 워크로드 ‘Deployment’ 페이지로 이동하고 [Create]를 클릭합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/036baf23123e7291d5fcfb82a2572e53.png)
3. ‘Create Workload’ 페이지에서 지침에 따라 작업 부하의 기본 정보를 지정합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/a1391e5768e6fd5cfe0e6b3c65417a50.png)
  - **Workload Name**: 생성할 워크로드의 이름을 입력합니다. 여기서는 nginx를 예로 사용합니다.
  -  **Description**: 관련 워크로드 정보를 입력합니다.
  -  **Tag**: key = value 이것은 키 값 쌍이며 이 예시의 태그는 기본적으로 k8s-app = **nginx**로 설정됩니다.
  -  **Namespace**: 요구 사항에 따라 네임스페이스를 선택합니다.
  -  **Type**: 요구 사항에 따라 유형을 선택합니다.
  -   **Volume**: 요구 사항에 따라 탑재된 워크로드 볼륨을 설정합니다. 자세한 내용은 [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)를 참고하십시오.
4. 지침에 따라 ‘Containers in the pod’를 설정합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/2ec2c7c803ee61a2d218f17df785636e.png)
주요 매개변수 정보는 다음과 같습니다.
  - **Name**: 포드에 있는 컨테이너의 이름을 입력합니다. 여기서는 test를 예시로 사용합니다.
  - **Image**: [Select an image]를 클릭하고 팝업 창에서 [DockerHub Image]> **nginx**를 선택한 후 [OK]를 클릭합니다.
  - **Image Tag**: 기본값인 `latest`를 사용합니다.
  - **Image Pull Policy**: 필요에 따라 사용 가능한 세 가지 정책 중 하나를 선택합니다. 이 예시에서는 기본 정책이 적용됩니다.
    이미지 가져오기 정책을 설정하지 않고 이미지 태그가 비어 있거나 `latest` 상태로 남아 있으면 Always 정책이 사용됩니다. 그렇지 않으면 IfNotPresent 정책이 사용됩니다.
    - **Always**: 이미지를 항상 원격으로 가져옵니다.
    - **IfNotPresent**: 기본적으로 로컬 이미지가 사용됩니다. 사용 가능한 로컬 이미지가 없으면 이미지를 원격으로 가져옵니다.
    - **Never**: 로컬 이미지가 사용됩니다. 사용 가능한 로컬 이미지가 없으면 예외가 보고됩니다.
5. ‘Number of Pod’ 섹션에서 지침에 따라 서비스에 대한 파드 수를 설정합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/51c4971952bbd697ca458a415fd1ce21.png)
 - **Manual adjustment**: 포드 수를 설정합니다. 이 예에서 포드 수는 1로 설정되어 있습니다. ‘+’ 또는 ‘-’를 클릭하여 포드 수를 변경할 수 있습니다.
 - **Auto Adjustment**: 설정 조건 중 하나라도 충족되면 pod 수가 자동으로 조정됩니다. 자세한 내용은 [Service Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424)을 참고하십시오.
6.   다음 지침에 따라 워크로드 액세스를 설정합니다. 아래 이미지를 참고하십시오.   
![](https://main.qcloudimg.com/raw/aedd2d73ab7e5f79218d8194c9b1c249.png)
 - **Service**: ‘Enable’을 선택합니다.
 - **Service Access**: ‘Via Internet’을 선택합니다.
 - **Load Balancer**: 요구 사항에 따라 선택합니다.
 - **Port Mapping**: TCP 프로토콜을 선택하고 컨테이너 포트와 서비스 포트를 모두 80으로 설정합니다.
 >!서비스 클러스터의 보안 그룹은 노드 네트워크와 컨테이너 네트워크를 인터넷에 개방해야 합니다. 또한 인터넷에 포트 30000 - 32768을 개방해야 합니다. 그렇지 않으면 TKE를 사용할 수 없는 문제가 발생할 수 있습니다. 자세한 내용은 [TKE 보안 그룹 설정](https://intl.cloud.tencent.com/document/product/457/9084)을 참고하십시오.
7. [Create workload]을 클릭하여 Nginx 서비스 생성을 완료합니다.


### Nginx 서비스에 액세스

Nginx 서비스는 다음 두 가지 방법으로 액세스할 수 있습니다.

#### **Cloud Load Balancer(CLB) IP**를 사용하여 Nginx 서비스에 액세스

1. 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 클릭하여 ‘Cluster Management’ 페이지로 이동합니다.
2. Nginx 서비스의 클러스터 ID를 클릭하고 [Service]>[Service]를 선택합니다.
3. 서비스 관리 페이지에서 Nginx 서비스의 CLB IP를 복사합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/bab54241805b352ae007ece3d130bb4a.png)
4. 브라우저의 주소 표시줄에 CLB IP를 입력하고 ‘**Enter**’ 키를 눌러 서비스에 액세스합니다.

#### 서비스 이름을 사용하여 Nginx 서비스에 액세스

클러스터의 다른 서비스 또는 컨테이너는 서비스 이름으로 직접 액세스할 수 있습니다.

### Nginx 서비스 확인
서비스가 성공적으로 생성되면 서비스에 액세스할 때 Nginx 서버 시작 페이지로 직접 들어갑니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/156e6d3b804e6b214ef7600fee4fa9c1.png)

### 더 많은 Nginx 설정
컨테이너 생성에 실패한 경우 [Event FAQ](https://intl.cloud.tencent.com/document/product/457/8187)를 참고하십시오.
