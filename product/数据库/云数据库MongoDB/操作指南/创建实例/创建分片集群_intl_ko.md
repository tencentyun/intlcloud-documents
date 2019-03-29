### 샤딩 클러스터 소개
현재 TencentDB for MongoDB는 샤딩 기능을 지원합니다. 샤딩 클러스터는 데이터를 샤딩 키에 따라 여러 물리적 서버에 저장합니다. 매끄러운 확장으로 TB/PB 수준의 데이터 스토리지 시나리오에 적합합니다. 또한, 샤딩 클러스터는 인스턴스 수준의 백업과 롤백을 지원하여 데이터의 높은 신뢰성을 보장합니다. 각 샤딩은 다중 노드로 자동 재해 복구를 구현하여 서비스의 뛰어난 가용성을 확보합니다. TencentDB for MongoDB 샤딩 기능으로 편리하고 효율적으로 대용량 분산형 스토리지 메커니즘을 구축합니다.


### 샤딩 클러스터 생성
MongoDB [구매 페이지](https://buy.cloud.tencent.com/mongodb?clusterType=1)에 로그인하여 "샤딩 클러스터"를 클릭하고 수요에 따라 샤딩 수, 샤딩 노드 수 및 노드 사양을 선택합니다. 모든 샤딩은 다중 노드의 복제본 세트입니다. 샤드 내의 다중 노드는 자동으로 재해 복구하여 서비스의 뛰어난 가용성을 보장합니다.
[![](https://mc.qcloudimg.com/static/img/6fb80892b40e93cbcc19cb43d2d70b80/goumaiye.png)](https://mc.qcloudimg.com/static/img/6fb80892b40e93cbcc19cb43d2d70b80/goumaiye.png)

### 샤딩 클러스터 콘솔
콘솔에서 샤드의 구성, 샤드 노드의 사양 및 사용한 용량 등 샤딩 클러스터 인스턴스의 세부 정보를 볼 수 있습니다. 또한 콘솔에서 인스턴스의 갱신 관리 및 용량 확장 등의 작업을 진행할 수 있습니다.
[![](https://mc.qcloudimg.com/static/img/6cabd8fbb7652a85648fe454b243d365/k2.png)](https://mc.qcloudimg.com/static/img/6cabd8fbb7652a85648fe454b243d365/k2.png)

### 샤딩 클러스터 용량 확장
현재 TencentDB for MongoDB 샤딩 클러스터의 확장 방식은 모든 노드에 일괄적인 용량 확장만 지원합니다. 노드를 추가하여 확장할 수 없습니다. 인스턴스 리스트 페이지에서 "확장" 버튼을 클릭하고 확장할 용량 사양을 선택한 후, [업그레이드]를 클릭합니다.
[![](https://mc.qcloudimg.com/static/img/e723c37c10c076c03e2836dbdeec7b80/%7BADB18884-AB90-4475-B309-83F334A26A1E%7D.png)](https://mc.qcloudimg.com/static/img/e723c37c10c076c03e2836dbdeec7b80/%7BADB18884-AB90-4475-B309-83F334A26A1E%7D.png)


### 백업과 롤백
샤딩 클러스터 인스턴스의 백업 롤백은 복제본 세트와 일치합니다. 현재는 인스턴스 수준의 백업과 롤백을 지원합니다. 인스턴스 세부 정보 페이지에서 [백업] 버튼을 클릭하여 비고 정보를 입력한 후, [제출]을 클릭하여 인스턴스를 백업합니다.
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
롤백 작업 과정에서 롤백할 날짜를 입력해야 합니다. 현재는 5일 내의 임의적인 시점으로 롤백할 수 있습니다. 단, 이것은 2개 백업(성공하고 oplog 쓰기 충진 상태가 아님) 간의 시점을 선택하여 롤백하는 것입니다. 조건이 충족하지 않는다면 수동 백업을 실행해야 합니다.
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

### 클러스터 인스턴스 모니터링
TencentDB for MongoDB 샤딩 클러스터 인스턴스는 인스턴스, 샤딩, 및 노드의 3차원으로 모니터링 메트릭을 제공하여 전체 클러스터 데이터를 모니터링합니다. 그리고 작업 요청, 용량 사용, 부하 등 다양한 메트릭의 모니터링 데이터도 제공합니다.
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)
