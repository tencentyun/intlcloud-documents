### DynamoDB 클러스터 소개
DynamoDB는 문서와 키 값 스토리지 모형을 지원하고 테이블 차원을 기반으로 하며 높은 확장성을 갖춘 NoSQL 데이터베이스 서비스입니다. 기존의 NoSQL 모듈 프레임에 기반으로 Tencent Cloud 데이터베이스팀은 DynamoDB 프로토콜과 원활히 호환되며, 인스턴스 수준의 백업 및 롤백을 지원하고 자동 재해 복구 메커니즘을 탑재한 안정적인 고성능 데이터베이스 서비스를 출시했습니다. DynamoDB 개발자의 경우, 코드를 많이 바꿀 필요 없이 DynamoDB 프로토콜을 통해 데이터베이스에 액세스할 수 있습니다.


### DynamoDB 클러스터 생성
MongoDB [구매 페이지](https://buy.cloud.tencent.com/mongodb?clusterType=1)에 들어간 후, [샤딩 클러스터]를 클릭하고, 프로토콜 유형에서 "DynamoDB 프로토콜"을 선택합니다.
기본 레이어도 스토리지 용량의 매끄러운 확장을 위해 여러 물리적 서버에 데이터를 분리하여 배포합니다. 따라서, 사용자는 수요에 맞게 샤딩 수, 샤딩의 노드 수 및 노드 사양을 선택해야 합니다. 모든 샤딩은 다중 노드의 복제본 세트입니다. 샤드 내의 다중 노드는 자동으로 재해 복구하여 서비스의 뛰어난 가용성을 보장합니다.
[![](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)

### 콘솔 관리
콘솔에서 노드의 구성, 사양 및 사용한 용량 등 DynamoDB 클러스터 인스턴스의 세부 정보를 볼 수 있습니다. 또한 콘솔에서 인스턴스의 갱신 관리 및 용량 확장 등의 작업을 진행할 수 있습니다.
[![](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)

### 용량 확장 작업
현재 DynamoDB 클러스터의 확장 방식은 모든 노드에 일괄적인 확장만 지원합니다. 노드를 추가하여 확장할 수 없습니다. 인스턴스 리스트 페이지에서 "용량 확장" 버튼을 클릭하고 확장할 용량 사양을 선택한 후, [업그레이드]를 클릭합니다.
[![](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)


### 백업과 롤백
현재는 인스턴스 수준의 백업과 롤백을 지원합니다. 인스턴스 세부 정보 페이지에서 [백업] 버튼을 클릭하여 비고 정보를 입력한 후, [제출]을 클릭하여 인스턴스를 백업합니다.
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
롤백 작업 과정에서 롤백할 날짜를 입력해야 합니다. 현재는 5일 내의 임의적인 시점으로 롤백할 수 있습니다. 단, 이것은 2개 백업 간의 시점을 선택하여 롤백하는 것입니다. 조건이 충족하지 않는다면 수동 백업을 실행해야 합니다.
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

### 인스턴스 모니터링
인스턴스는 인스턴스, 샤딩, 및 노드의 3차원으로 모니터링 메트릭을 제공하여 전체 클러스터 데이터를 모니터링합니다. 그리고 작업 요청, 용량 사용, 부하 등 다양한 메트릭의 모니터링 데이터도 제공합니다.
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)

