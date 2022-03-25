## 작업 시나리오
사용자가 인스턴스 서비스를 중지해야 하거나 종료 상태를 진행해야 수정 가능한 설정일 경우 인스턴스를 종료할 수 있습니다. 인스턴스 종료는 로컬 컴퓨터의 종료 작업과 같습니다.

## 주의 사항

- 시스템 명령어를 사용하여 종료하거나(예: Windows 시스템의 종료 및 Linux 시스템의 shutdown 명령어), Tencent Cloud 콘솔을 사용하여 종료할 수 있습니다. 종료 시 콘솔을 열어 종료 프로세스를 조회하여 문제가 발견되지 않았는지 검사하는 것을 권장합니다.
- 인스턴스 서비스가 종료될 경우 서비스를 제공할 수 없습니다. 따라서 종료하기 전 CVM이 서비스 요청을 중지했는지 확인하십시오.
- 인스턴스가 정상적으로 종료될 경우 상태가 종료 중으로 변경되며 종료가 완료된 후에는 종료로 변경됩니다. 종료 시간이 너무 길 경우 문제가 발생할 수 있습니다. 자세한 내용은 [종료 관련](https://intl.cloud.tencent.com/document/product/213/2917)을 참고하여 강제 종료를 피하십시오.
- 인스턴스가 종료된 후 모든 스토리지가 인스턴스 상태와 연결을 유지하며, 모든 디스크 데이터도 보존됩니다. 메모리의 데이터는 손실됩니다.
- 인스턴스 종료는 인스턴스의 물리적 특성, 인스턴스 공용 IP 및 개인 IP를 변경하지 않습니다. [EIP](https://intl.cloud.tencent.com/document/product/213/5733) 바인딩 관계가 유지되지만, 서비스 중단으로 인해 이러한 IP에 액세스할 때 잘못된 응답이 발생합니다. [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) 관계는 유지됩니다.
- 만약 종료 인스턴스가 [CLB 인스턴스의 백엔드 서버 클러스터](https://intl.cloud.tencent.com/document/product/214/32388)에 속할 경우 종료 후 지속적인 서비스를 제공하지 않습니다.
상태 확인 정책이 설정되어 있는 경우 종료 인스턴스가 자동으로 차단되고 요청이 전달되지 않습니다. 상태 확인 정책이 설정되어 있지 않은 경우 클라이언트는 502 오류 리턴을 수신할 수 있습니다. 자세한 정보는 [상태 확인](https://intl.cloud.tencent.com/document/product/214/38451)을 참고하십시오.
- 만약 종료 인스턴스가 [Auto Scaling 그룹](https://intl.cloud.tencent.com/document/product/377/3590)에 있는 경우 Auto Scaling 서비스는 종료된 인스턴스의 운행 상황이 좋지 않다고 표시합니다. 이 경우 Auto Scaling 그룹에서 삭제된 후 교체 인스턴스가 시작됩니다. 자세한 내용은 [Auto Scaling](https://intl.cloud.tencent.com/zh/document/product/377)을 참고하십시오.

## 작업 단계
<dx-tabs>
::: 콘솔을 통한 인스턴스 종료

#### 인스턴스 개별 종료
 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
 2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
  - **리스트 뷰**: 아래 그림과 같이 종료할 인스턴스를 선택하고 오른쪽 작업 열에서 **더보기** > **인스턴스 상태** > **종료**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e46cac67a3040e2a5ba851c24d386f0e.png)
  - **탭 뷰**: 아래 그림과 같이 종료할 인스턴스 페이지 오른쪽 상단에서 **더보기** > **인스턴스 상태** > **종료**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e15c3a175ce068f4d3070b232026bc54.png)




#### 인스턴스 일괄 종료
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 아래 이미지와 같이 종료할 모든 인스턴스를 선택하고 리스트의 상단에서 **종료**를 클릭해 인스턴스를 일괄 종료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b467b958fcb01c5183fbcfe8bded913c.png)
<dx-alert infotype="explain" title="">
종료할 수 없는 인스턴스는 원인을 표시합니다.
</dx-alert>


:::
::: \sAPI\s를 통한 인스턴스 종료
[StopInstances](https://intl.cloud.tencent.com/document/product/213/33235) 인터페이스를 참고하십시오.
:::
</dx-tabs>

## 후속 작업
인스턴스가 종료 상태인 경우에만 다음 인스턴스 속성을 수정할 수 있습니다.
- **인스턴스 설정(CPU, 메모리)**: 인스턴스 유형을 변경할 경우 [인스턴스 설정 변경](https://intl.cloud.tencent.com/document/product/213/2178)을 참고하십시오.
- **비밀번호 수정**: [로그인 비밀번호](https://intl.cloud.tencent.com/document/product/213/6093)를 참고하십시오.
- **키 로딩**: [SSH 키](https://intl.cloud.tencent.com/document/product/213/6092)를 참고하십시오.
