## 작업 시나리오
WordPress 서비스를 빠르게 만드는 방법에 대해 알아보려면 [단일 포드 WordPress](https://intl.cloud.tencent.com/document/product/457/7205)를 참고하십시오. 이러한 방식으로 생성된 WordPress 서비스에는 다음과 같은 기능이 있습니다.
- 데이터는 동일한 컨테이너에서 실행되는 MySQL 데이터베이스에 기록됩니다.
- 서비스를 빠르게 실행할 수 있습니다.
- 특정 이유로 컨테이너가 중지되면 데이터베이스 및 스토리지 유형 파일이 손실됩니다.

MySQL 데이터베이스를 사용하면 데이터를 영구적으로 저장할 수 있습니다. 데이터베이스는 포드/컨테이너가 다시 시작될 때 계속 실행됩니다. 본 문서에서는 [TencentDB](https://intl.cloud.tencent.com/product/cdb)를 사용하여 MySQL 데이터베이스를 구성하는 방법과 TencentDB를 사용하는 WordPress 서비스를 만드는 방법을 설명합니다.

## 전제 조건
- [Tencent Cloud 계정 등록](https://intl.cloud.tencent.com/register)을 완료합니다.
- 클러스터를 생성 완료해야 합니다. 클러스터 생성 방법에 대한 자세한 내용은 [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637)를 참고하십시오.
>?문서에 사용된 데이터베이스는 [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147)입니다.


## 작업 단계

### WordPress 서비스 생성
#### TencentDB 인스턴스 생성
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하고 아래 이미지와 같이 데이터베이스 인스턴스 목록에서 [Create]를 클릭합니다.
![](https://main.qcloudimg.com/raw/78b43441e5d296e83e2db9246aaddff7.png)
2. 구매할 구성을 선택합니다. 자세한 내용은 [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147)을 참고하십시오.
>!데이터베이스는 클러스터와 동일한 지역에 있어야 합니다. 그렇지 않으면 데이터베이스에 연결할 수 없습니다.

3. 데이터베이스를 생성한 후 [MySQL instance list](https://console.cloud.tencent.com/cdb)에서 볼 수 있습니다.
4. 데이터베이스를 초기화합니다. 자세한 내용은 [MySQL 인스턴스 초기화](https://intl.cloud.tencent.com/document/product/236/3128)를 참고하십시오.

#### Tencent DB를 사용하는 WordPress 서비스 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. ‘Cluster Management’ 페이지에서 서비스가 생성될 클러스터의 ID를 클릭하여 아래 이미지와 같이 클러스터의 ‘Deployment’ 페이지로 이동한 후 [Create]를 클릭합니다.
![](https://main.qcloudimg.com/raw/239bfe0c3488c19139c5359b27d24044.png)
3. ‘Create Workload’ 페이지에서 아래 이미지와 같이 워크로드의 기본 정보를 지정합니다.
![](https://main.qcloudimg.com/raw/3ff74d307b48b793ac121345e7f19154.png)
 - **Workload Name**: 생성할 워크로드의 이름입니다. 여기서는 wordpress를 예시로 사용합니다.
 - **Description**: 관련 워크로드 정보를 지정합니다.
 -  **Tag**: key = value 키 값 쌍을 지정합니다. 기본값은 k8s-app = **wordpress**입니다.
 -  **Namespace**: 요구 사항에 따라 네임스페이스를 선택합니다.
 -  **Type**: 요구 사항에 따라 유형을 선택합니다.
 - **Volume**: 요구 사항에 따라 워크로드가 탑재되는 볼륨을 설정합니다. 자세한 내용은 [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)를 참고하십시오.
4. 아래 그림의 지침에 따라 ‘Containers in the pod’를 설정합니다.
![](https://main.qcloudimg.com/raw/7e2fccaf2c0168743dc03480cab2a6f3.png)
주요 매개변수는 다음과 같습니다. 다른 매개변수에 대한 기본 설정을 유지합니다.
  - **Name**: 사용자 정의 컨테이너 이름을 입력합니다. 이 예시에서는 test가 사용됩니다.
  - **Image**: `wordpress`를 입력하십시오.
  - **Image Tag**: latest를 입력하십시오.
  - **Image Pull Policy**: 세 가지 정책을 사용할 수 있습니다. 필요에 따라 정책을 선택합니다. 이 예시에서는 기본 정책이 사용됩니다.
이미지 가져오기 정책을 지정하지 않으면 이미지 태그가 비어 있거나 latest일 때 Always 정책이 사용됩니다. 그렇지 않으면 IfNotPresent 정책이 사용됩니다.
      - **Always**: 이미지는 항상 원격 위치에서 가져옵니다.
      - **IfNotPresent**: 기본적으로 로컬 이미지를 사용합니다. 이미지를 사용할 수 없는 경우 원격 위치에서 가져옵니다.
      - **Never**: 로컬 이미지만 사용합니다. 이미지를 사용할 수 없으면 예외가 발생합니다.
 - **Environment variable**: 다음 설정 정보를 순서대로 입력합니다.
WORDPRESS_DB_HOST = TencentDB for MySQL의 내부 IP 주소
WORDPRESS_DB_PASSWORD = 초기화 시 입력한 비밀번호
5. 아래 이미지와 같이 서비스의 Pod 수를 설정합니다.
![](https://main.qcloudimg.com/raw/06e71d9208795f57159bdaba8eae45b4.png)
 - **Manual adjustment**: 포드 수를 설정합니다. 이 예시에서 포드 수는 1로 설정되어 있습니다. ‘+’ 또는 ‘-’를 클릭하여 포드 수를 변경할 수 있습니다.
 - **Auto Adjustment**: 설정 조건 중 하나라도 충족되면 pod 수가 자동으로 조정됩니다. 자세한 내용은 [Automatic Scaling Basic Operations](https://intl.cloud.tencent.com/document/product/457/32424)를 참고하십시오.
6. 아래 그림의 지침에 따라 워크로드에 대한 액세스 설정(Service)을 구성합니다.
![](https://main.qcloudimg.com/raw/9d0d2970a6df63f6eb83bbc73deb7178.png)
 - **Service**: ‘Enable’을 선택합니다.
 - **Service Access**: ‘Via Internet’를 선택합니다.
 - **Load Balancer**: 필요에 따라 로드 밸런서를 생성하거나 선택합니다.
  - **Port Mapping**: TCP를 선택하고 컨테이너 포트와 서비스 포트를 모두 80으로 설정합니다.
 >!서비스가 속한 클러스터의 보안 그룹은 노드 네트워크와 컨테이너 네트워크를 인터넷에 개방해야 합니다. 또한 인터넷에 포트 30000-32768을 개방해야 합니다. 그렇지 않으면 TKE를 사용하지 못할 수 있습니다. 자세한 내용은 [TKE 보안 그룹 설정](https://intl.cloud.tencent.com/document/product/457/9084)을 참고하십시오.

7. [Create workload]을 클릭합니다.


### WordPress 서비스에 액세스
다음 두 가지 방법 중 하나를 사용하여 WordPress 서비스에 액세스할 수 있습니다.

#### CLB IP 주소를 사용하여 WordPress 서비스에 액세스
1. 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 클릭하여 ‘Cluster Management’ 페이지로 이동합니다.
2. WordPress 서비스가 속한 클러스터의 ID를 클릭하고 [Service]>[Service]를 선택합니다.
3. 서비스 관리 페이지에서 아래 이미지와 같이 WordPress 서비스의 CLB IP 주소를 복사합니다.
![](https://main.qcloudimg.com/raw/f5f9964eacb4752e528ce32d467662a8.png)
4. 브라우저 주소 상자에 CLB IP 주소를 붙여넣고 **Enter** 키를 눌러 서비스에 액세스합니다.

#### 서비스 이름을 사용하여 WordPress 서비스에 액세스
클러스터의 다른 서비스 또는 컨테이너는 서비스 이름을 사용하여 WordPress 서비스에 액세스할 수 있습니다.

### WordPress 서비스 인증
서비스 생성 후 서비스에 접속하면 아래 이미지와 같이 WordPress 서버 설정 페이지가 나타납니다.
![](https://main.qcloudimg.com/raw/903f45d57c58541433b555d487bd2980.png)

### 더 많은 WordPress 설정
컨테이너 생성에 실패한 경우 [Event FAQ](https://intl.cloud.tencent.com/document/product/457/8187)를 참고하십시오.
