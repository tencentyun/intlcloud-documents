## 작업 시나리오

다음과 같은 방법으로 클러스터에 노드를 추가할 수 있습니다.
- [노드 생성](#createNode)
- [기존 노드 추가](#addExistingNode)

## 전제 조건

[TKE Console](https://console.cloud.tencent.com/tke2)에 로그인했습니다.

## 작업 단계

[](id:createNode)
### 노드 생성

1. 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 클릭하여 ‘Cluster Management’ 페이지로 이동합니다.
2. CVM 인스턴스를 생성할 클러스터의 ID를 클릭하여 클러스터의 세부 정보 페이지로 이동합니다.
3. 왼쪽 사이드바에서 [Node Management]>[Node]를 선택하여 노드 목록 페이지로 이동하고 [Create Node]를 클릭합니다.
4. ‘Create Node’ 페이지에서 아래 그림과 같이 필요에 따라 관련 매개변수를 설정합니다.
![](https://main.qcloudimg.com/raw/952eb1e912940ebc080949f0a1dae13e.png)
주요 매개변수 정보는 다음과 같습니다.
  - **Billing Mode**: [pay-as-you-go] 및 [monthly subscription]가 지원됩니다. 자세한 내용은 [과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.
  - **Availability Zone**: 이 매개변수는 가용존에서 사용 가능한 서브넷 목록을 필터링하는 데 사용됩니다.
  - **Cluster Network**: 생성된 노드에 IP를 할당하는 서브넷을 선택합니다. 단일 노드 생성은 단일 서브넷만 지원합니다.
  - **Model Configuration**: [Select a model]을 클릭합니다. ‘Model Configuration’ 페이지에서 다음 설명에 따라 필요에 따라 값을 선택합니다.
    - **Model**: CPU 코어 수, 메모리 크기, 인스턴스 유형을 지정하여 모델을 선택할 수 있습니다. 자세한 내용은 [인스턴스 스펙](https://intl.cloud.tencent.com/document/product/213/11518)을 참고하십시오.
    - **System disk**: 스토리지를 제어하고 CVM(Cloud Virtual Machines) 실행을 스케쥴링합니다. 선택한 모델에 사용할 수 있는 시스템 디스크 유형을 보고 필요에 따라 시스템 디스크를 선택할 수 있습니다. 자세한 내용은 [Cloud Disk Type](https://intl.cloud.tencent.com/document/product/362/31636)을 참고하십시오.
    - **Data Disk**: 모든 사용자 데이터를 저장합니다.
  - **Instance Name**: 콘솔에 표시되는 CVM 인스턴스 이름으로 호스트 이름의 이름 지정 모드에 따라 결정됩니다. 다음 두 가지 이름 설정 방법이 제공됩니다.
        - **Auto-generated**: 호스트 이름이 자동으로 지정됩니다. 여러 인스턴스에 대한 순차 번호 지정 또는 사용자 정의 형식을 지원합니다. 최대 60자까지 허용됩니다. 인스턴스 이름은 기본적으로 `tke_클러스터id_worker` 형식으로 자동 생성됩니다.
        - **Custom Name**: 호스트 이름을 수동으로 설정합니다. 인스턴스 이름은 재설정하지 않은 호스트 이름과 동일합니다.
 - **Login Method**: 필요에 따라 다음 로그인 방법 중 하나를 선택할 수 있습니다.
    -  **SSH Key Pair**: 키 쌍은 알고리즘을 사용하여 생성된 매개변수 쌍입니다. 키 쌍을 사용하여 CVM 인스턴스에 로그인하는 것이 일반 암호를 사용하는 것보다 더 안전합니다. 자세한 내용은 [SSH 키](https://intl.cloud.tencent.com/document/product/213/6092)를 참고하십시오.
      - **SSH Key**: 이 매개변수는 [SSH Key Pair]이 선택된 경우에만 표시됩니다. 드롭다운 목록에서 기존 키를 선택합니다. 키를 만드는 방법은 [SSH 키 관리](https://intl.cloud.tencent.com/document/product/213/16691)를 참고하십시오.
    - **Random Password**: 시스템이 자동으로 생성된 비밀번호를 [Message Center](https://console.cloud.tencent.com/message)로 보냅니다. 
    - **Custom Password**: 프롬프트에 따라 비밀번호를 설정합니다.
 - **Security Group**: 기본값은 클러스터 생성 시 지정한 보안 그룹입니다. 보안 그룹을 교체하거나 필요에 따라 보안 그룹을 추가할 수 있습니다.
 - **Amount**: 생성할 인스턴스 수입니다. 필요에 따라 이 값을 지정할 수 있습니다.
5. (선택 사항) 다음 그림과 같이 ‘Create Node’ 페이지에서 [More Setting]을 클릭하여 추가 정보를 보거나 설정합니다.
![](https://main.qcloudimg.com/raw/54bbd92b00eea36efaf6de36c850b7eb.png)
  - **CAM Role**: 이번에 생성된 모든 노드를 동일한 CAM 역할에 바인딩하고 해당 역할에 바인딩된 권한 정책을 노드에 부여할 수 있습니다. 자세한 내용은 [인스턴스 역할 관리](https://intl.cloud.tencent.com/document/product/213/38290)를 참고하십시오.
  - **Container Directory**: 컨테이너 및 이미지 저장 디렉터리를 설정하려면 이 옵션을 선택합니다. `/var/lib/docker`와 같은 데이터 디스크에 저장하는 것이 좋습니다.
  - **Security Services**: 무료 DDoS 보호, WAF(Web Application Firewall) 및 클라우드 워크로드 보호가 기본적으로 활성화됩니다. 자세한 내용은 [Cloud Workload Protection](https://intl.cloud.tencent.com/product/cwp)을 참고하십시오.
  - **Cloud Monitor(CM)**: 기본적으로 무료 모니터링, 분석 및 경보가 활성화되며 CVM 모니터링 메트릭을 얻기 위해 구성 요소가 설치됩니다. 자세한 내용은 [Cloud Monitor](https://intl.cloud.tencent.com/product/cm)를 참고하십시오.
  - **Cordon initial nodes**: ‘Cordon this node’를 선택한 후 이 노드에 새 Pod를 스케쥴링할 수 없습니다. 노드를 수동으로 해제하거나 필요에 따라 사용자 정의 데이터에서 [uncordon command](https://intl.cloud.tencent.com/document/product/457/30654)를 실행할 수 있습니다.
  - **Label**: [New Label]을 클릭하여 노드를 필터링하거나 관리하는 데 사용되는 Label을 사용자 정의합니다.
  - **Custom data**: 노드를 구성할 사용자 정의 데이터를 지정합니다. 즉, 노드가 시작될 때 구성된 스크립트를 실행합니다. 스크립트의 재진입 및 재시도 로직을 확인해야 합니다. 스크립트 및 해당 로그 파일은 노드 경로 `/usr/local/qcloud/tke/userscript`에서 볼 수 있습니다.

[](id:addExistingNode)
### 기존 노드 추가

>!
>- 현재는 동일한 VPC에만 CVM 인스턴스를 추가할 수 있습니다.
>- 클러스터에 공용 게이트웨이 CVM을 추가하지 마십시오. 이 유형의 CVM을 다시 설치하여 클러스터에 추가하고 노드를 사용할 수 없게 되면 DNS 예외가 발생합니다.

1. 왼쪽 사이드바에서 [[Cluster](https://console.cloud.tencent.com/tke2/cluster)]를 클릭하여 ‘Cluster Management’ 페이지로 이동합니다.
2. 기존 노드를 추가할 클러스터의 ID를 클릭하여 해당 클러스터의 상세 페이지로 이동합니다.
3. [Node Management]>[Node]를 선택하고 아래 그림과 같이 [Add Existing Node]를 클릭합니다.
![](https://main.qcloudimg.com/raw/7407fd0e78baa86ae7ea089f108c54c9.png)
4. ‘Select Node’ 페이지에서 추가할 노드를 선택하고 [Next]를 클릭합니다.
5. ‘CVM Configuration’ 페이지에서 클러스터에 추가할 CVM 인스턴스를 구성합니다.
주요 매개변수 정보는 다음과 같습니다.
 - 마운트 데이터 디스크: 마운트 포맷 관련 설정입니다. 장치 이름과 마운트 지점을 입력하고 시스템을 포맷할지 여부를 선택합니다.
    - 미선택: 데이터 디스크 장착을 설정하지 않습니다. 수동으로 마운트하거나 스크립트를 사용하여 마운트할 수 있습니다.
    - 선택: 장치 이름, 포맷 시스템(포맷 안 함 선택 가능), 마운트 지점을 설정해야 합니다.
     /dev/vdb 장치를 ext4로 포맷하고 /var/lib/docker 디렉토리에 마운트하려면 다음과 같이 설정할 수 있습니다.
     장치 이름: /dev/vdb로 설정, 형식 시스템: ext4를 선택, 마운트 포인트: /var/lib/docker로 설정
<dx-alert infotype="notice" title="">
- 중요한 데이터는 미리 백업하시기 바랍니다. 디스크를 포맷했다면 시스템을 포맷할 필요 없이 마운트 지점만 입력하면 됩니다.
- 마운트 형식 설정은 선택한 노드에 적용됩니다. 입력한 장치 이름(예: /dev/vdb)이 예상에 맞는지 확인하십시오(CBS에서 핫 스와핑 및 기타 작업을 수행한 경우 장치 이름이 변경될 수 있음).
- 파티션을 생성했거나 /LVM을 사용하는 경우 장치 이름에 파티션 이름 /LVM 이름을 입력하고 마운트를 포맷하기 위한 해당 매개변수를 설정하십시오.
- 장치 이름을 잘못 입력하면 오류가 발생하고 노드 초기화가 종료됩니다.
- 입력한 마운트 포인트가 존재하지 않는 경우 해당 디렉터리가 생성되며 오류는 발생하지 않습니다.
</dx-alert>
 - 컨테이너 디렉터리: 컨테이너 및 이미지 저장 디렉터리를 설정합니다. 데이터 디스크에 저장하는 것이 좋습니다.
 - 운영 체제: 클러스터 세부 정보 페이지에서 OS 설정을 수정할 수 있습니다. 수정 후 새로 추가되거나 다시 설치된 노드는 새 운영 체제를 사용합니다.
 - 로그인 방법:
     - 사용자 정의 암호: 프롬프트에 따라 암호를 설정합니다.
    - SSH 키 쌍: 키 쌍은 알고리즘에 의해 생성된 매개변수 쌍입니다. 키 쌍을 사용하여 CVM에 로그인하는 것이 일반 암호를 사용하는 것보다 더 안전합니다. 자세한 내용은 [SSH 키](https://intl.cloud.tencent.com/document/product/213/6092)를 참고하십시오.
    - 비밀번호 자동 생성: 비밀번호가 자동으로 생성되어 메시지 센터를 통해 귀하에게 전송됩니다.
 - 보안 그룹: 필요에 따라 CVM 인스턴스에 대한 네트워크 액세스 제어를 설정합니다. [Add Security Group]을 클릭하여 인터넷에 대한 다른 포트를 열 수 있습니다.
6. [Finish]를 클릭합니다.





