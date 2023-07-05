## 작업 시나리오

Tencent Cloud TKE는 기본적으로 모든 클러스터에 기본 모니터링 기능을 제공합니다. 아래 단계를 통해 TKE 모니터링 데이터를 조회할 수 있습니다.
- [클러스터 지표 조회](#check1)
- [노드 지표 조회](#check2)
- [노드에서 Pod의 지표 조회](#check3)
- [워크로드 지표 조회](#check4)
- [워크로드 내 Pod 지표 조회](#check5)
- [Pod에 있는 Container의 지표 조회](#check6)

## 전제 조건
TKE 콘솔에 로그인하고 [[Cluster Management](https://console.cloud.tencent.com/tke2/cluster?rid=1)] 페이지로 이동합니다.

## 작업 단계

<span id="check1"></span>
### 클러스터 지표 조회
모니터링 데이터를 조회할 클러스터의 행에서 <img src="https://main.qcloudimg.com/raw/fef90a2f69f50758b30e4c4b5e0bc7de.png" style="margin-bottom: -2px;;"></img>을(를) 클릭합니다. 아래 이미지와 같이 해당 클러스터의 모니터링 정보가 표시됩니다.
![](https://main.qcloudimg.com/raw/444d1c462cf681ec7456229b25373c3a.png)

<span id="check2"></span>
### 노드 지표 조회
아래 단계를 통해 노드 및 Master&Etcd 노드에 대한 모니터링 정보를 조회할 수 있습니다.
1. 조회할 클러스터의 ID/이름을 선택하여 클러스터 관리 페이지로 이동합니다.
2. **Node Management**를 펼쳐 일반 노드와 Master&Etcd 노드에 대한 모니터링 정보를 확인합니다.
 - **Node**>**Monitoring**을 선택하여 **Node Monitoring** 페이지로 이동하고 모니터링 정보를 확인합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/c1c1fca1e108f8479b50a895c2d2d0b5.png)
 - **Master&Etcd**>**Monitoring**을 선택하면 **Master&Etcd Monitoring** 페이지로 이동하여 모니터링 정보를 확인할 수 있습니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/b178510aaf43b2907d64835d7384a5b1.png)

<span id="check3"></span>
### 노드에서 Pod의 지표 조회
아래 두 가지 방법 중 하나를 사용하여 노드의 Pod 지표를 확인할 수 있습니다.
1. 확인할 클러스터의 ID/이름을 선택하여 클러스터 관리 페이지로 이동합니다.
2. **Node Management**>**Node**를 선택하여 노드 목록 페이지로 이동합니다.
3. 필요에 따라 노드에서 Pod의 지표를 조회하는 방법을 선택합니다.
 - 노드 목록에서 Pod 지표 확인하기.
    1. **Monitoring**을 클릭하여 **Node Monitoring** 페이지로 이동합니다.
    2. **Pod**를 클릭하고 확인할 노드로 **Node**를 선택합니다. 이렇게 하면 해당 노드의 Pod에 대해 모니터링되는 지표의 플롯을 확인할 수 있습니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/e58301ce2675d2de018a867c31fcfb69.png)
 - 노드 세부 정보 페이지에서 Pod 지표 확인하기.
    1. 확인할 노드의 ID/이름을 선택하여 노드 관리 페이지로 이동합니다.
    2. **Pod Management** 탭을 선택하고 **Monitoring**을 클릭하여 해당 노드의 Pod에 대해 모니터링되는 지표의 플롯을 확인합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/269631374cbe8ff955de4d691c53772c.png)

<span id="check4"></span>
### 워크로드 지표 조회
1. 확인할 클러스터의 ID/이름을 선택하여 클러스터 관리 페이지로 이동합니다.
2. **Workload**>**Any Workload Type**을 선택합니다. 예를 들어 **Deployment**를 선택하여 Deployment 관리 페이지로 이동합니다.
3. **Monitoring**을 클릭하여 워크로드 모니터링 정보를 확인합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/392b8235bb98367b50bc4b20e6ad3118.png)

<span id="target"></span><span id="check5"></span>
### 워크로드 내 Pod 지표 조회
<span id="first"></span>
1. 확인할 클러스터의 ID/이름을 선택하여 클러스터 관리 페이지로 이동합니다.
2. **Workload**>**Any Workload Type**을 선택합니다. 예를 들어 **Deployment**를 선택하여 Deployment 관리 페이지로 이동합니다.
3. 확인할 워크로드 이름을 선택하여 워크로드 관리 페이지로 이동합니다.<span id="third"></span>
4. **Pod Management** 탭을 선택하고 **Monitoring**을 클릭하여 해당 워크로드의 Pod에 대해 모니터링되는 지표 플롯을 확인합니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/bda91f0b0fb55cf87cf7258cc471ae1f.png)

<span id="check6"></span>
### Pod에 있는 Container의 지표 조회
1. 워크로드 세부 정보 페이지로 이동하려면 [워크로드 내 Pod 지표 조회](#target)의 [1단계](#first) - [3단계](#third)를 참고하십시오.
2. **Pod Management** 탭을 선택하고 **Monitoring**을 클릭하여 **Pod Monitoring** 페이지로 이동합니다.
3. **Container**를 클릭하고 조회할 Pod로 **Pod**를 선택합니다. 이렇게 하면 해당 Pod의 Container에 대해 모니터링되는 지표의 플롯을 볼 수 있습니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/28b567cd6eda684fbd0076d89bdadd76.png)


