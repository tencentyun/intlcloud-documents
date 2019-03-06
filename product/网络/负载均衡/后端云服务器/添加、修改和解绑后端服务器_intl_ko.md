CLB는 요청을 정상적으로 운행 중인 백 엔드 CVM 인스턴스에 라우팅합니다. 인스턴스에 대한 요청이 높아지면 사용자는 로드밸런서에 더 많은 인스턴스를 추가하여 처리해야 합니다.

RS를 언바인딩하면 CLB 인스턴스와 CVM 인스턴스의 관련 관계도 해제합니다. 그 요청에 대한 포워딩을 즉시 중단하지만 CVM의 수명 주기에는 영향을 미치지 않기 때문에 준비가 잘 되었을 때 그것을 다시 RS 클러스터에 추가할 수 있습니다.

CLB 인스턴스가 어느 자동 조정 그룹이 연결되어 있을 경우, 해당 그룹의 인스턴스는 CLB 백 엔드 인스턴스에 자동 추가되며, 자동 조정 그룹에서 제거한 CVM 인스턴스는 CLB RS에서 자동 삭제됩니다.

## CLB 백 엔드 인스턴스 추가
### 콘솔을 사용하여 CLB 백 엔드 인스턴스 추가

1) [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인한 뒤 해당하는 CLB 인스턴스 ID를 클릭하여 CLB 세부 정보 페이지에 진입합니다.

2) CVM 바인딩 탭 중 [CVM 바인딩] 버튼을 클릭합니다.

3) 팝업창에 ‘동일 지역, 동일 네트워크 환경, 격리되지 않음, 만료되지 않음, 대역폭(피크값)이 0이 아님` 선택 항목 CVM 목록이 나타납니다. 연결해야 할 CVM을 선택하고 [확인] 버튼을 클릭합니다.

그러면 CVM이 CLB과의 연결 작업을 완료할 수 있습니다.

### API로 CLB 백 엔드 인스턴스 추가

[RegisterInstancesWithLoadBalancer API](https://cloud.tencent.com/doc/api/244/1265)를 참조하십시오.

## CLB RS 가중치 수정
RS 가중치는 CVM이 포워딩된 요청 상대 수량을 결정합니다. CLB RS 가중치와 과련한 더 많은 정보는 [CLB 라운드 로빈 방식](/doc/product/214/6153)을 참조할 수 있습니다.

### 콘솔을 사용하여 CLB RS 가중치 수정

1) [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인한 뒤 해당하는 CLB 인스턴스 ID를 클릭하여 CLB 세부 정보 페이지에 진입합니다.

2) CVM 바인딩 탭 중 해당 CVM 가중치란의 [수정] 버튼을 클릭하면 백 엔드 CVM 가중치를 수정할 수 있습니다.

### API로 CLB RS 가중치 수정
[ModifyLoadBalancerBackends API](https://cloud.tencent.com/doc/api/244/1264)를 참조하십시오.

## CLB RS 언바인딩

### 콘솔을 사용하여 CLB RS 언바인딩

1) [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인한 뒤 해당하는 CLB 인스턴스 ID를 클릭하여 CLB 세부 정보 페이지에 진입합니다.

2) CVM 바인딩 탭 중 해당 CVM [언바인딩] 버튼을 클릭하면 백 엔드 CVM과 CLB의 바인딩 관계를 해제할 수 있습니다.

