본문은 콘솔 또는 명령 라인을 통해 TencentDB for MySQL의 병렬 쿼리 기능을 활성화 또는 비활성화하는 방법을 설명합니다.

## 전제 조건
데이터베이스 버전: 커널 버전 20220831 이상의 MySQL 8.0.

## 매개변수 설명
>?CPU 코어 수가 4보다 크거나 같으면 원본 인스턴스 및 읽기 전용 인스턴스 모두에 대해 병렬 쿼리 기능을 활성화할 수 있습니다.

콘솔 또는 명령 라인을 통해 txsql_max_parallel_worker_threads 및 txsql_parallel_degree 매개변수를 0 이외의 값으로 설정하여 현재 인스턴스에 대한 병렬 쿼리 기능을 활성화할 수 있습니다. 매개변수 및 권장 설정은 다음과 같습니다.
**매개변수 정보**

| 매개변수 | 변수 유형 | 범위 | 기본값 | 값 범위 | 설명 |
|---------|---------|---------|---------|---------|---------|
| txsql_max_parallel_worker_threads | Integer | Global | {MIN(DBInitCpu,0)} | 0-{MAX(DBInitCpu-2,2)} | 병렬 쿼리에 사용할 수 있는 인스턴스 노드의 총 스레드 수입니다. 0으로 설정하면 사용 가능한 병렬 스레드가 없으며 병렬 쿼리 기능을 비활성화함을 나타냅니다. |
| txsql_parallel_degree | Integer | Global/session | 4 | 0 - 64 | 단일 문의 병렬 쿼리 중에 사용할 수 있는 최대 스레드 수(기본 병렬 처리)입니다. 0은 병렬 쿼리 기능을 비활성화함을 나타냅니다. |

**권장 설정**
- 병렬 처리 수준 제한: txsql_parallel_degree는 단일 문장의 병렬 쿼리를 위한 최대 스레드 수, 즉 기본 병렬성을 나타냅니다. 이 값을 인스턴스의 CPU 코어 수량의 절반으로 제한하는 것이 좋습니다. 안정성을 보장하기 위해 CPU 코어가 4개 미만인 소규모 클러스터에서는 병렬 쿼리 기능이 비활성화되며 콘솔 또는 명령 라인을 통해 병렬 쿼리 매개변수를 조정할 수 없습니다.
- SQL 문의 병렬 쿼리 시 기본적으로 txsql_parallel_degree에 의해 설정된 병렬 처리 수준이 사용되며, 이는 HINT 문을 통해 조정할 수 있습니다. 자세한 내용은 [hint 문 제어](https://www.tencentcloud.com/document/product/236/53410)를 참고하십시오.
- txsql_max_parallel_worker_threads는 병렬 쿼리에 사용할 수 있는 인스턴스의 스레드 수를 나타내고, txsql_max_parallel_worker_threads / txsql_parallel_degree는 병렬 쿼리에서 허용되는 최대 SQL 문 수를 나타냅니다.
- txsql_max_parallel_worker_threads 및 txsql_parallel_degree는 병렬 쿼리 기능의 상태를 제어합니다. 둘 중 하나가 0이면 기능이 비활성화됩니다.

TencentDB for MySQL은 비즈니스 적응 및 안정성을 위해 병렬 쿼리의 실행 조건을 설정할 수 있는 다양한 매개변수를 제공합니다. 조건이 설정되면 데이터베이스는 병렬문 실행을 위한 실행 비용, 테이블 행 수 및 메모리 사용량과 같은 조건에 대해 각 SQL문을 실행할 수 있는지 여부를 확인합니다. 매개변수는 다음과 같이 설명됩니다.

| 매개변수 | 변수 유형 | 범위 | 기본값 | 값 범위 | 설명 |
|---------|---------|---------|---------|---------|---------|
| innodb_txsql_parallel_partitions_per_worker | Integer | Global/Session |13 |0-256 |분할된 데이터의 병렬 스캔에서 스레드당 스캔할 평균 파티션 수입니다. |
| txsql_optimizer_context_max_mem_size | Integer | Global/Session |{MIN(DBInitMemory*52429,8388608)} |0-{DBInitMemory*52429} |병렬 쿼리 플랜 환경에서 단일 문이 신청할 수 있는 최대 메모리 크기입니다. |
| txsql_parallel_cost_threshold | Integer | Global/Session |50000 |0-9223372036854476000 |병렬 실행 비용의 임계값입니다. 실행 비용이 이 임계값보다 높은 명령문만 병렬로 실행됩니다. |
| txsql_parallel_exchange_buffer_size | Integer | Global/Session |1048576 |65536-268435456 |데이터 교환 버퍼 크기입니다. |
| txsql_parallel_table_record_threshold | Integer | Global/Session |5000 |0-9223372036854476000 |병렬 테이블 행 수량의 임계값입니다. 이 임계값보다 많은 행 수량이 있는 테이블만 병렬 테이블로 선택됩니다. |

>!
>- 병렬 쿼리 매개변수는 인스턴스를 다시 시작할 필요 없이 설정된 직후에 적용됩니다.
>- 매개변수의 범위가 session인 경우 해당 문에 대해서만 적용됩니다.

### 콘솔에서 병렬 쿼리 활성화 또는 비활성화
MySQL 콘솔의 매개변수 설정 페이지에서 매개변수를 설정하여 기능을 활성화하거나 비활성화할 수 있습니다.
- 병렬 쿼리를 활성화하려면 txsql_max_parallel_worker_threads 및 txsql_parallel_degree를 0 이외의 값으로 설정합니다.
- 병렬 쿼리를 비활성화하려면 txsql_max_parallel_worker_threads 및 txsql_parallel_degree를 0으로 설정합니다.

매개변수 설정 페이지에서 실행 조건을 설정할 수도 있습니다. 자세한 방법은 [인스턴스 매개변수 설정](https://intl.cloud.tencent.com/document/product/236/35793)을 참고하십시오.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/BgaK167_18.png)

### hint 문을 통해 SQL 문의 병렬 실행 모드 지정
TencentDB for MySQL을 사용하면 hint 문을 통해 SQL 문의 병렬 실행 모드를 지정할 수 있습니다. 자세한 방법은 [hint 문 제어](https://www.tencentcloud.com/document/product/236/53410)를 참고하십시오.

## 관련 문서
- [병렬 쿼리 보기](https://www.tencentcloud.com/document/product/236/53411)
- [hint 문 제어](https://www.tencentcloud.com/document/product/236/53410)

