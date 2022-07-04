## TXRocks 개요
TXRocks는 매우 인기 있는 고성능 영구 KV(key-value) 스토리지인 RocksDB를 기반으로 Tencent의 TXSQL 팀에서 개발한 트랜잭션 스토리지 엔진입니다.

## 왜 TXRocks인가
TXRocks 트랜잭션 스토리지 엔진은 RocksDB의 LSM Tree 스토리지 구조를 활용하여 InnoDB의 half-full 페이지 및 조각으로 인해 발생하는 낭비를 줄일 뿐만 아니라 컴팩트 스토리지 형식을 사용합니다. 따라서 InnoDB에 필적하는 성능을 가지지만 저장 공간은 절반 이상 줄일 수 있습니다. 데이터 볼륨이 크고 트랜잭션 읽기/쓰기 성능에 대한 요구 사항이 높은 비즈니스에 더 적합합니다.

## RocksDB의 LSM Tree 아키텍처
RocksDB는 LSM Tree 스토리지 구조를 사용합니다. 여기서 데이터는 메모리의 MemTable 세트와 디스크의 다중 레벨 SST 파일로 구성됩니다.
쓰기 요청의 경우 새 버전의 레코드가 먼저 Active MemTable에 작성된 다음 데이터 내구성을 위해 WAL이 작성됩니다. 요청에 대해 MemTable 및 WAL 파일이 작성된 후 응답이 반환될 수 있습니다.
Active MemTable에 기록된 데이터의 양이 특정 임계값에 도달하면 MemTable은 동결된 Immutable MemTable로 전환됩니다. 백엔드 스레드는 Immutable MemTable을 디스크로 플러시하여 SST 파일을 생성합니다. SST 파일은 플러시 순서로 L0 - L6 레벨로 정렬됩니다. 각 레벨에서 서로 다른 SST 파일의 레코드는 순차적이며 겹치지 않습니다. 그러나 Immutable MemTable이 점유하는 메모리 공간을 즉시 릴리스하기 위해 이러한 레코드는 L0 레벨에서 겹칠 수 있습니다. 

레코드를 읽으면 Active MemTable, Immutable MemTable, L0의 SST 파일, L1 – 6의 SST 파일에서 차례로 검색됩니다. 컴포넌트에서 레코드가 발견되면 최신 버전의 레코드가 발견되어 즉시 반환됩니다.

범위 스캔이 수행되면 MemTable을 포함하는 데이터의 각 레벨에서 이터레이터가 생성됩니다. 이터레이터는 다음 레코드를 찾기 위해 병합 정렬을 수행합니다. 읽기 과정에서 볼 수 있듯이 LSM Tree의 레벨이 너무 많으면 읽기 성능, 특히 범위 스캔 성능이 크게 떨어집니다. 따라서 더 나은 LSM Tree 모양을 유지하기 위해 백엔드는 지속적으로 compaction 작업을 수행하여 낮은 레벨의 데이터를 높은 레벨로 병합하여 레벨 수를 줄입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/cc38118399e25373a55631ca94f15ec4.png)

## TXRocks 아키텍처
![](https://qcloudimg.tencent-cloud.cn/raw/b7bd4fb0cc37a7d60c0c29945095c167.png)

## TXRocks의 강점
#### 저장 공간 절약
InnoDB에서 사용하는 B+tree 구조에 비해 LSM Tree는 상당한 저장 공간을 절약할 수 있습니다.
InnoDB의 B+Tree 분할은 종종 half-full 페이지, 유휴 페이지 및 공간 낭비를 초래합니다. 따라서 InnoDB는 유효 페이지 활용도가 낮습니다.

TXRocks SST 파일의 크기는 일반적으로 수십 또는 수백 MB 이상의 값으로 설정됩니다. 따라서 TXRocks는 4K 정렬로 인한 낭비가 훨씬 적습니다. SST 파일은 Block으로 나누어져 있지만 해당 Block을 정렬할 필요는 없습니다.

또한 TXRocks SST 파일은 접두사 압축을 사용하므로 동일한 접두사가 있는 데이터 레코드에 대해 하나의 레코드만 생성됩니다. 다른 레벨의 SST 파일은 다른 압축 알고리즘을 채택하여 저장 공간 오버헤드를 더욱 줄일 수 있습니다. 트랜잭션 overhead의 경우 InnoDB 레코드에는 trx id 및 roll_ptr 필드가 포함되어야 합니다. 대조적으로, 다른 트랜잭션 오버헤드는 가장 낮은 레벨의 TXRock(대부분의 데이터 포함)에 있는 SST 파일에 대해 저장할 필요가 없습니다. 예를 들어, 레코드의 버전 번호는 충분한 시간이 지나면 지울 수 있습니다.

#### 쓰기 증폭 감소
InnoDB는 데이터의 한 행만 변경되더라도 전체 페이지가 디스크로 플러시될 수 있는 In-Place 변경 모드를 사용하여 높은 쓰기 증폭과 더 많은 랜덤 쓰기를 유발합니다.

TXRocks는 쓰기 증폭이 낮은 Append-Only 변경 모드를 사용합니다. 따라서 쓰기 주기가 제한된 SSD와 같은 장치에 더 친숙합니다.

## 적용 시나리오
TXRocks는 스토리지 비용에 민감하고, 쓰기보다 읽기가 훨씬 많고, 데이터 볼륨이 크며, 높은 트랜잭션 읽기/쓰기 성능을 요구하는 기업에 매우 적합합니다.

## TXRock 사용 방법
자세한 내용은 [Instructions](https://intl.cloud.tencent.com/document/product/236/47014)를 참고하십시오.

## 최적화 및 후속 개발 
TXSQL 팀은 비즈니스 요구 사항을 기반으로 TXRocks를 최적화하고 있습니다. 그 예로, sum 쿼리 성능을 30배 이상 향상하였습니다. 또한 더 높은 성능과 비용 효율성을 위해 AEP를 L2 캐시로 사용하기 위해 새로운 하드웨어와의 통합을 적극적으로 모색하고 있습니다.

TencentDB for MySQL의 스토리지 엔진으로서 TXRocks는 사용 중 발생하는 문제와 관련하여 지속적으로 최적화되고 개선될 것입니다. TXSQL 팀은 또한 새로운 하드웨어를 기반으로 기술을 탐색할 것이며 InnoDB에 대한 중요 보완책으로 더 많은 주요 서비스에서 TXRock을 출시할 것입니다.

