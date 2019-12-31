## 작업 시나리오
사용자가 인스턴스 서비스를 중지해야 하거나 종료 상태를 진행해야 수정 가능한 구성일 경우 인스턴스를 종료할 수 있습니다. 인스턴스 종료는 로컬 컴퓨터의 종료 작업과 같습니다.

## 주의사항

- 시스템 커맨드를 사용하여 종료하거나(예: Windows 시스템의 종료 및 Linux 시스템의 shutdown 커맨드), Tencent Cloud 콘솔을 사용하여 종료할 수 있습니다. 종료 시 콘솔을 열어 종료 프로세스를 조회하여 문제가 발견되지 않았는지 검사를 추천합니다.
- 인스턴스 서비스가 종료될 경우 서비스를 제공할 수 없습니다. 따라서 종료하기 전 CVM이 서비스 요청을 중지했는지 확인하십시오.
- 인스턴스가 정상적으로 종료될 경우 상태가 종료 중으로 변경되며 종료가 완료된 후에는 종료로 변경됩니다. 종료 시간이 너무 길 경우 문제가 발생할 수 있습니다. 자세한 내용은 [종료 관련](https://intl.cloud.tencent.com/document/product/213/2917)을 참조하여 강제 종료를 피하십시오.
- 인스턴스가 종료된 후 모든 스토리지가 인스턴스 상태와 연결을 유지하며, 모든 디스크 데이터도 보존됩니다. 메모리의 데이터는 손실됩니다.
- 인스턴스의 종료는 인스턴스의 물리적 기능을 변경하지 않습니다. 인스턴스 공용 네트워크 IP와 개인 네트워크 IP는 변경되지 않으며, [EIPv6](https://intl.cloud.tencent.com/document/product/213/5733)는 바인딩 관계를 유지합니다. 하지만 서비스 중단 [클래식링크](https://cloud.tencent.com/document/product/215/20083)와 같은 IP를 액세스할 경우 오류 응답을 얻습니다. 관계는 변경되지 않고 유지됩니다. 
- 만약 종료 인스턴스가 [CLB 인스턴스의 백엔드 서버 클러스터](https://cloud.tencent.com/document/product/214/6095)에 속할 경우 종료 후 지속적인 서비스를 제공하지 않습니다.
상태 확인 정책이 구성되어 있는 경우 종료 인스턴스가 자동으로 차단되고 요청이 전달되지 않습니다. 상태 확인 정책의 구성되어 있지 않은 경우 클라이언트는 502 오류 리턴을 수신할 수 있습니다. 자세한 정보는 [상태 확인](https://intl.cloud.tencent.com/document/product/214/3394)을 참조하십시오.
- 만약 종료 인스턴스가 [Auto Scaling 그룹](https://intl.cloud.tencent.com/document/product/377/3590)에 있는 경우 Auto Scaling 서비스는 종료된 인스턴스의 운행 상황이 좋지 않다고 표시합니다. 이 경우 Auto Scaling 그룹에서 삭제된후 교체 인스턴스가 시작됩니다. 자세한 내용은 [Auto Scaling](https://cloud.tencent.com/document/product/377)를 참조하십시오.

## 작업 절차
### 콘솔을 통해 인스턴스를 종료할 경우
 1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
 2. 실제 필요에 따라 다른 작업 방식을 선택하십시오.
  - 단일 인스턴스 종료: 종료해야 하는 인스턴스를 선택한 뒤, 오른쪽 작업 표시줄에서 [더보기] > [인스턴스 상태] > [종료]를 클릭하십시오.
  - 다중 인스턴스 종료: 종료해야 하는 모든 인스턴스를 선택한 뒤, 리스트의 상단에서 [종료]를 클릭해 인스턴스를 일괄로 종료하십시오.
    종료할 수 없는 인스턴스는 원인을 표시합니다.

### API를 통해 인스턴스를 종료할 경우
[StopInstances](https://cloud.tencent.com/document/product/213/15743) 인터페페이스를 참조하십시오.

## 후속 작업
인스턴스가 종료 상태인 경우에만 다음 인스턴스 속성을 수정할 수 있습니다.
- **인스턴스 구성(CPU, 메모리)**: 인스턴스 유형을 변경할 경우 [인스턴스 구성 조정](https://intl.cloud.tencent.com/document/product/213/2178)을 참조하십시오.
- **마운트 된 CBS의 크기**: CBS의 크기를 조정할 경우 [CBS 확장](https://intl.cloud.tencent.com/document/product/362/5747)을 참조하십시오.
- **비밀번호 수정**: [로그인 및 비밀번호](https://intl.cloud.tencent.com/document/product/213/6093)를 참조하십시오.
- **로딩 키**: [SSH 키](https://intl.cloud.tencent.com/document/product/213/6092)를 참조하십시오.
