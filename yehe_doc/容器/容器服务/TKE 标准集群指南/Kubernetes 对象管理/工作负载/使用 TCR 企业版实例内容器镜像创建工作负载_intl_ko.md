## 작업 시나리오
Tencent Container Registry(TCR) 엔터프라이즈 버전은 엄격한 데이터 보안 및 규정 준수 요구 사항, 여러 리전에 분산된 비즈니스, 대규모 클러스터가 있는 엔터프라이즈급 컨테이너 고객를 위해 엔터프라이즈급 독점 보안 이미지 호스팅 서비스를 제공합니다. TCR 개인 버전과 비교했을 때, TCR 엔터프라이즈 버전은 컨테이너 이미지 보안 스캔, 리전 간 자동 동기화, Helm Chart 호스팅, 네트워크 액세스 제어 및 기타 기능을 지원합니다. 자세한 내용은 [TCR](https://intl.cloud.tencent.com/document/product/1051)을 참고하십시오.

본 문서는 TCR에서 호스팅되는 프라이빗 이미지를 사용하여 Tencent Kubernetes Engine(TKE)에서 애플리케이션을 배포하는 방법을 설명합니다.

## 전제 조건
TCR에서 호스팅되는 프라이빗 이미지를 사용하여 TKE에서 애플리케이션을 배포하기 전에 다음 작업을 완료했는지 확인하십시오.
- [TCR Console](https://console.cloud.tencent.com/tcr)에서 TCR 엔터프라이즈 버전 인스턴스 생성을 완료해야 합니다. TCR 엔터프라이즈 버전 인스턴스를 생성하지 않은 경우 [Creating an Enterprise Edition Instance](https://intl.cloud.tencent.com/document/product/1051/35486)를 참고하여 생성하시기 바랍니다.
- 서브 계정을 사용하는 경우 해당 인스턴스에 대한 서브 계정 작업 권한을 부여해야 합니다. 자세한 내용은 [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248)을 참고하십시오.


## 작업 단계

### 컨테이너 이미지 준비
#### 네임스페이스 생성
새 TCR 엔터프라이즈 버전 인스턴스에는 기본 네임스페이스가 없으며 푸시된 이미지를 통해 네임스페이스를 자동으로 생성할 수 없습니다. 따라서 필요에 따라 네임스페이스를 생성합니다. 자세한 내용은 [Managing Namespace](https://intl.cloud.tencent.com/document/product/1051/35487)를 참고하십시오.
프로젝트 또는 팀 이름을 기반으로 네임스페이스 이름을 지정하는 것이 좋습니다. 이 문서에서는 `docker`를 예시로 사용합니다. 네임스페이스가 생성되면 다음 페이지가 나타납니다.
![](https://main.qcloudimg.com/raw/38d0f3739e45a94c39265b32fe0437aa.png)

#### 이미지 저장소 생성(선택 사항)
컨테이너 이미지는 특정 이미지 저장소에서 호스팅됩니다. 필요에 따라 이미지 저장소를 만듭니다. 자세한 내용은 [Creating an Image Repository](https://intl.cloud.tencent.com/document/product/1051/35488)를 참고하십시오. 이미지 저장소 이름을 배포할 컨테이너 이미지의 이름으로 설정합니다. 이 문서에서는 `getting-started`를 예시로 사용합니다. 이미지 저장소가 생성되면 다음 페이지가 나타납니다.
>?docker cli 또는 jenkins와 같은 다른 이미지 도구를 사용하여 이미지를 TCR 엔터프라이즈 버전 인스턴스로 푸시합니다. 이미지 저장소가 없으면 이미지 저장소가 자동으로 생성됩니다. 미리 만들 필요가 없습니다.

![](https://main.qcloudimg.com/raw/c07fbfbc133bde822f13f7a5005ea6d8.png)

#### 컨테이너 이미지 푸시
docker cli 또는 jenkins와 같은 다른 이미지를 사용하여 이미지를 특정 이미지 리포지토리로 푸시할 수 있습니다. 여기에서 docker cli는 이미지를 푸시하는 데 사용됩니다. 컨테이너 이미지를 푸시하려면 Docker가 설치된 CVM 또는 물리적 서버를 사용하고 클라이언트가 인스턴스에 액세스할 수 있는지 확인해야 합니다. 자세한 내용은 [Network Access Control Overview](https://intl.cloud.tencent.com/document/product/1051/35490)를 참고하십시오.
1. [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253)을 참고하여 액세스 자격 증명을 얻고 Docker Login 합니다.
2. 로그인에 성공하면 로컬 서버에 컨테이너 이미지를 생성하거나 테스트를 위해 Docker Hub에서 공개 이미지를 가져옵니다.
이 문서에서는 공식 DockerHub 웹 사이트의 최신 Nginx 이미지를 예시로 사용합니다. 명령 라인 도구에서 다음 명령을 순차적으로 실행하여 이 이미지를 푸시합니다. demo-tcr, docker 및 getting-started를 사용자가 생성한 실제 인스턴스, 네임스페이스 및 이미지 리포지토리 이름으로 바꾸십시오.
```
docker tag getting-started:latest demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
```
docker push demo-tcr.tencentcloudcr.com/docker/getting-started:latest
```
이미지가 푸시된 후 TCR 콘솔의 ‘[Image Repository](https://console.cloud.tencent.com/tcr/repository)’ 페이지로 이동하고 레지스트리 이름을 선택하여 세부 정보를 볼 수 있습니다.
<span id="deployTKE"></span>

### TKE 클러스터 액세스 TCR 인스턴스 설정
TCR 엔터프라이즈 버전 인스턴스는 네트워크 액세스 제어를 지원하고 기본적으로 모든 외부 액세스를 거부합니다. TKE 클러스터의 외부망 또는 내부망을 선택하여 특정 인스턴스에 액세스하고 TKE 클러스터의 네트워크 구성을 기반으로 컨테이너 이미지를 가져올 수 있습니다. TKE 클러스터와 TCR 인스턴스가 동일한 리전에 배포되는 경우 TKE 클러스터가 내부망을 통해 컨테이너 이미지를 풀링하여 풀링을 가속화하고 외부망 트래픽 비용을 줄이는 것이 좋습니다.
#### 빠른 액세스 구성을 위해 TCR 애드온 사용(권장)
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. ‘Cluster Management’ 페이지에서 대상 클러스터의 ID를 클릭하여 클러스터 세부 정보 페이지로 이동합니다. 
3. 클러스터 세부 정보 페이지의 왼쪽 사이드바에서 [Add-on Management]를 클릭하여 ‘Add-on Management’ 페이지로 이동하고 [Create]를 클릭합니다.
4. ‘Create an add-on’ 페이지에서 아래와 같이 ‘TCR’을 선택합니다.
    >? 현재 TCR 애드온은 K8S 버전은 1.14, 1.16의 클러스터만 지원합니다. 다른 클러스터 버전을 사용하는 경우 액세스 방법을 수동으로 구성하거나 클러스터 버전을 업그레이드하십시오.
	
   ![](https://main.qcloudimg.com/raw/217494ffd43b7d2e6d2621df67d5d80a.png)
  - 애드온 및 설정 설명을 보려면 [View Detail]을 클릭합니다.
  - [Parameter Configuration]을 클릭하여 애드온을 설정합니다.
5. ‘TCR Add-on Parameter Setting’ 페이지에서 아래와 같이 [View Detail]에 설명된 애드온 설정 방법을 기반으로 관련 매개변수를 설정합니다.
![](https://main.qcloudimg.com/raw/729b3e3b4170de3c6d344adb1ccaf7cf.png)
    - **Associate with Instance**: TKE 클러스터와 동일한 리전에서 TCR 인스턴스를 선택합니다.
    - **Password-free Pulling**: 기본 설정을 유지합니다.
    - **Private Network Access Configuration**: 내부망 액세스 링크에 ‘Linkage normal’이 표시되지 않으면 TCR 인스턴스와 TKE 클러스터가 위치한 VPC의 내부망 링크를 설정해야 합니다. 자세한 내용은 [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492)을 참고하십시오.
6. [OK]를 클릭하여 애드온 선택 페이지로 돌아갑니다.
7. 애드온 선택 페이지에서 [Done]을 클릭하여 클러스터에 대한 TCR 애드온을 설치합니다.
8. 애드온이 설치된 후 클러스터는 아래와 같이 개인 네트워크를 통해 암호 없이 연결된 인스턴스에서 이미지를 가져올 수 있습니다.
![](https://main.qcloudimg.com/raw/28820e0f8742656ea540f86e6336c156.png)

#### 내부망 액세스 및 액세스 자격 증명 수동 설정
#### 1. 내부망 액세스 설정
1. TCR 인스턴스와 TKE 클러스터가 위치한 VPC의 내부망 연결을 구성하고 자동 파싱을 활성화합니다. 자세한 내용은 [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492)을 참고하십시오.
2. 현재 TCR 인스턴스가 위치한 지역에서 자동 구문 분석이 지원되지 않는 경우 TKE 클러스터에서 TCR 인스턴스에 대한 도메인 이름 구문 분석을 구성할 수 있습니다. 실제 요구 사항에 따라 다음 솔루션 중에서 선택할 수 있습니다.
 - **Configuring the node host when creating the cluster**
 TKE 클러스터 생성 프로세스 중 ‘CVM Configuration’ 단계에서 [Advanced Setting]을 선택하고 ‘Node Launch Configuration’에 다음 내용을 입력합니다.
```
echo '172.21.17.69 demo.tencentcloudcr.com' >> /etc/hosts
```
 - **Configuring the node host for an existing cluster**
클러스터 노드에 로그인하고 다음 명령을 실행합니다.
```
echo '172.21.17.69 demo.tencentcloudcr.com' >> /etc/hosts
```
`172.21.17.69` 및 `demo.tencentcloudcr.com`을 사용하는 내부망 확인 IP 주소 및 TCR 인스턴스 도메인 이름으로 바꿉니다.

<span id="issued"></span>
#### 2. 액세스 자격 증명 설정
네임스페이스를 생성할 때 아래 단계에 따라 액세스 자격 증명을 제공합니다.
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. ‘Cluster Management’ 페이지에서 대상 클러스터의 ID를 클릭하여 클러스터 세부 정보 페이지로 이동합니다.
3. 왼쪽 사이드바에서 [Namespace]를 클릭하여 ‘Namespace’ 페이지로 이동하고 [Create]를 클릭합니다.
4. ‘CreateNamespace’ 페이지에서 ‘Auto-issue TKE image repository access credential’을 선택하고 아래와 같이 클러스터가 액세스할 TCR 인스턴스를 선택합니다.
	![](https://main.qcloudimg.com/raw/46557c14ff5e9f833e911a9ad08e0d6d.png)
5. [Create Namespace]를 클릭합니다.
	네임스페이스가 생성되면 인스턴스의 액세스 자격 증명이 네임스페이스에 자동으로 전달됩니다. 액세스 자격 증명(예: `1000090225xx-tcr-m3ut3qxx-dockercfg`)을 보려면 [Configuration Management]>[Secret]을 선택합니다. `1000090225xx`는 네임스페이스 생성에 사용된 서브 계정의 UIN을 나타내며 `tcr-m3ut3qxx`는 선택한 인스턴스의 ID를 나타냅니다.

기존 네임스페이스에 액세스 자격 증명을 전달하려면 다음 단계를 수행하십시오.
<span id="loginInfo"></span>
1. 인스턴스에 로그인하는 데 사용되는 사용자 이름과 비밀번호를 얻습니다. 자세한 내용은 [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253)을 참고하십시오.
2. 클러스터 세부 정보 페이지의 왼쪽 사이드바에서 [Configuration Management]>[Secret]을 선택하여 ‘Secret’ 페이지로 이동합니다.
3. ‘Secret’ 페이지에서 [Create]를 클릭하면 아래와 같이 ‘CreateSecret’ 페이지로 이동합니다. 액세스 자격 증명을 전달하려면 다음 정보를 참고하십시오.
	![](https://main.qcloudimg.com/raw/73e3f94b14b0c37940c27f85f58e5e87.png)
	주요 매개변수 정보는 다음과 같습니다.
	 - **Secret Type**: [Dockercfg]를 선택합니다.
	 - **Effective Scope**: 액세스 자격 증명이 전달되는 네임스페이스를 선택합니다.
	 - **Repository Domain Name**: TCR 인스턴스의 액세스 도메인 이름을 입력합니다.
	 - **Username and Password**: [1단계](#loginInfo)에서 얻은 사용자 이름과 비밀번호를 입력합니다.
4. [Create Secret]을 클릭하여 액세스 자격 증명을 제공합니다.

### TCR 인스턴스의 컨테이너 이미지를 사용하여 워크로드 생성
1. 클러스터 세부 정보 페이지의 왼쪽 사이드바에서 [Workload]>[Deployment]를 선택합니다.
2. ‘Deployment’ 페이지에서 [Create]를 클릭합니다.
3. ‘CreateWorkload’ 페이지에서 다음 매개변수를 설정하여 워크로드를 생성합니다.
주요 매개변수는 다음과 같이 설명됩니다.
 - **Namespace**: 액세스 자격 증명이 전달되는 네임스페이스를 선택합니다.
 - **Containers in the Pod**:
    - **Image**: [Select Image]를 클릭하고 팝업 창에서 ‘TCR Enterprise’를 선택하고 필요에 따라 리전, 인스턴스 및 이미지 저장소를 선택합니다. 아래 그림을 참고하십시오.
![](https://main.qcloudimg.com/raw/deb308676d70aa35a6f3fba1046281d9.png)
 - **Image Access Credential**:
	 - 클러스터에 TCR 애드온이 설치되어 있으면 설정할 필요가 없습니다.
	 - 클러스터에 TCR 애드온이 설치되어 있지 않으면 [Add Image Access Credential]를 클릭하고 [Configuring the access credential](#issued) 단계에서 전달된 액세스 자격 증명을 선택합니다. 아래 그림을 참고하십시오.
![](https://main.qcloudimg.com/raw/e8ef83350f71a79b014bfcfc2382fd46.png)
4. 다른 매개변수를 설정한 후 [Create Workload]를 클릭하고 워크로드 배포 진행률을 확인합니다.
워크로드가 배포되면 아래 그림과 같이 워크로드에 대한 ‘Number of Running/Desired Pod’가 ‘Deployment’ 페이지에서 ‘1/1’이 됩니다.
![](https://main.qcloudimg.com/raw/b1d02a4df392d56e191daff8ae61db0f.png)
