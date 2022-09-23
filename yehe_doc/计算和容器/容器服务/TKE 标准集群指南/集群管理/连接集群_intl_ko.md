## 작업 시나리오
Kubernetes 명령 라인 도구인 kubectl을 사용하여 로컬 클라이언트에서 TKE 클러스터에 연결할 수 있습니다. 본 문서에서는 클러스터 연결 방법을 설명합니다.

## 전제 조건
curl 소프트웨어를 설치하십시오.
운영 체제 유형에 따라 kubectl 획득 방법을 선택하십시오.
> 필요에 따라 명령 라인에서 ‘v1.8.13’을 비즈니스에 필요한 kubectl 버전으로 바꿉니다.

- **Mac OS X**
다음 명령을 실행하여 kubectl을 가져옵니다.
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/darwin/amd64/kubectl
```
- **Linux**
다음 명령을 실행하여 kubectl을 가져옵니다.
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/linux/amd64/kubectl
```
- **Windows**
다음 명령을 실행하여 Kubectl을 가져옵니다.
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/windows/amd64/kubectl.exe
```

## 작업 단계

<span id="installKubectl"></span>

### Kubectl 설치

1. [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/)을 참고하여 kubectl을 설치합니다.
> 
>- kubectl을 이미 설치했다면 이 단계를 건너뛰십시오.
>- 이 단계에서는 Linux 운영 체제를 예로 사용합니다.

2. 다음 명령어를 실행하여 kubectl 사용 권한을 부여합니다.
```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
3. 다음 명령어를 실행하여 설치 결과를 확인합니다.
```shell
kubectl version
```
반환된 버전 정보가 다음과 유사하면 설치가 완료된 것입니다.
```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```

###  Kubeconfig 설정

1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster?rid=4)]를 클릭하여 클러스터 관리 페이지로 이동합니다.
2. 대상 **클러스터의 ID 또는 이름**을 클릭하여 클러스터의 세부 정보 페이지로 이동합니다.
3. 왼쪽 사이드바에서 [Basic Information]를 클릭합니다. 다음 그림과 같이 ‘Basic Information’ 페이지의 ‘Cluster APIServer Information’ 섹션에서 클러스터의 접속 주소, 공용 네트워크/사설 네트워크 접속 상태, kubeconfig 접속 자격 증명 등의 정보를 볼 수 있다.
 - **Accessed URL**: 클러스터의 APIServer 주소를 나타냅니다. 이 주소는 액세스를 위해 브라우저에 복사하여 붙여넣을 수 없습니다.
 - **Access entry**: 필요에 따라 주소 항목을 설정합니다.
	- **Public Network Access**: 이 옵션은 기본적으로 비활성화되어 있습니다. 공용 네트워크 액세스를 활성화하면 **클러스터의 apiserver가 공용 네트워크에 노출됩니다**. 또한 소스 권한을 설정해야 합니다. 기본적으로 모든 소스의 액세스 시도는 거부됩니다. 단일 IP 주소 또는 CIDR 블록에서 액세스를 허용할 수 있습니다. `0.0.0.0/0`을 설정하여 모든 소스에 대해 클러스터를 열지 않는 것이 좋습니다.
	- **Private Network Access**: 이 옵션은 기본적으로 비활성화되어 있습니다. 활성화하려면 서브넷을 설정해야 합니다. 사설 네트워크 액세스가 성공적으로 활성화되면 설정된 서브넷에서 IP 주소가 할당됩니다.
 - **Kubeconfig**: 복사 및 다운로드할 수 있는 클러스터의 액세스 자격 증명을 나타냅니다.
4. 필요에 따라 클러스터 자격 증명을 설정합니다.
   설정하기 전에 클러스터에 대한 액세스 자격 증명이 현재 클라이언트에 설정되었는지 확인합니다.
	- **No**인 경우 `~/.kube/config` 파일이 비어 있어 획득한 kubeconfig 액세스 자격 증명을 파일에 복사할 수 있습니다. `~/.kube/config` 파일이 클라이언트에 없으면 새로 만듭니다.
	- **Yes**인 경우 획득한 kubeconfig를 지정된 위치에 다운로드하고 다음 명령을 순서대로 실행하여 여러 클러스터의 config 파일을 병합할 수 있습니다.
```
KUBECONFIG=~/.kube/config:~/Downloads/cls-3jju4zdc-config kubectl config view --merge --flatten > ~/.kube/config
```
```
export KUBECONFIG=~/.kube/config
```
	위 명령어에서 `~/Downloads/cls-3jju4zdc-config`는 현재 클러스터의 kubeconfig 파일 경로를 나타냅니다. 이 경로를 다운로드한 파일의 실제 로컬 경로로 바꿉니다.


### Kubernetes 클러스터에 액세스
1.  kubeconfig를 설정한 후 다음 명령을 순서대로 실행하여 context를 보고 클러스터에 액세스할 컨텍스트를 전환합니다.
```
kubectl config get-contexts
```
```
kubectl config use-context cls-3jju4zdc-context-default
```
2.  다음 명령어를 실행하여 클러스터에 액세스할 수 있는지 확인합니다.
```
kubectl get node
```
클러스터에 연결할 수 없는 경우 공용 네트워크 액세스 또는 사설 네트워크 액세스가 활성화되어 있는지 확인하고 액세스 클라이언트가 지정된 네트워크 환경에 있는지 확인합니다.

## 관련 설명

### kubectl 명령 라인 소개

Kubectl은 Kubernetes 클러스터에서 작업을 수행하기 위한 명령 라인 도구입니다. 이 문서에서는 kubectl 구문, 일반적인 명령 작업 및 몇 가지 예를 다룹니다. 각 명령(모든 기본 명령 및 하위 명령 포함)에 대한 자세한 내용은 [kubectl reference document](https://kubernetes.io/docs/reference/generated/kubectl/kubectl/)를 참고하거나 `kubectl help` 명령을 실행하여 도움말 정보를 확인하십시오. kubectl 설치에 대한 자세한 내용은 [Kubectl 설치](#installKubectl)를 참고하십시오.
