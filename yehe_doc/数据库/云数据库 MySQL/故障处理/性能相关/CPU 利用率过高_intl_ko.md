## 문제 설명
TencentDB for MySQL에 응답이 느리거나, 연결할 수 없거나, 시간 초과 현상이 발생하였습니다. TencentDB for MySQL의 CPU 사용률이 80%를 초과하면 서비스 응답이 느려지거나 시간이 초과되거나 데이터베이스가 연결되지 않을 수 있습니다.

TencentDB for MySQL 인스턴스의 CPU 사용률은 [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb) 또는 [DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain/event?product=mysql)의 인스턴스 모니터링 페이지에서 확인할 수 있습니다.

>?CPU 사용률이 너무 높아지면 정상적인 업무 운영을 위해 [데이터베이스 인스턴스 사양 변경](https://intl.cloud.tencent.com/document/product/236/19707)의 안내에 따라 CPU 사양을 먼저 높일 것을 권장합니다. 후속적으로 이 문서를 참고하여 문제 해결 및 최적화를 진행할 수 있습니다.

## 장애 리스크
MySQL CPU 이용률이 너무 높은 상태로 장시간 유지되면 데이터베이스의 전체 성능이 크게 저하될 수 있으며, 심한 경우 인스턴스가 정지될 수도 있습니다.

HA 시스템이 이러한 문제를 감지하면 비즈니스의 고가용성을 유지하기 위해 원본-복제 전환을 트리거합니다. 전환하는 동안 일반적으로 60초 미만 동안 인스턴스를 사용할 수 없습니다. 피크 시간에 전환이 발생하면 비즈니스 안정성과 연속성에 심각한 영향을 미칩니다.

CPU 리소스 부족으로 비즈니스가 영향을 받지 않도록 하려면 CPU 사용률이 높은 인스턴스에 대해 애플리케이션을 최적화하거나 CPU 리소스를 업그레이드하는 것이 좋습니다. 원본-복제 전환 시 단 몇 초 동안만 연결이 끊어집니다. 따라서 지속적인 연결을 위해서는 애플리케이션에 재연결 메커니즘이 있어야 합니다.

## 가능한 원인
MySQL의 CPU 리소스는 주로 시스템 스레드와 사용자 스레드에서 사용됩니다. 따라서 CVM이 TencentDB for MySQL 인스턴스에서 독점적으로 사용되는 경우 두 가지 유형의 스레드에 집중하는 것만으로도 대부분의 문제를 해결할 수 있습니다.

### 사용자 스레드
사용자 스레드가 혼잡한 경우 대부분 ‘슬로우 쿼리’, ‘과도한 계산’ 및 ‘높은 QPS’(초당 쿼리 수)로 인해 발생합니다.

- **슬로우 쿼리**
order by, group by, 임시 테이블, join 등을 포함하는 쿼리는 매우 비효율적이어서 단일 SQL 문을 계산하는 데 CPU 시간이 훨씬 더 오래 걸립니다.
- **과도한 계산**
많은 양의 데이터 때문에 과도한 계산이 발생합니다.
- **높은 QPS(Queries Per Second)**
QPS가 높으면 CPU 시간이 길어집니다. 예를 들어, 4코어 서버가 20k - 30k의 높은 QPS를 유지하는 경우 단일 SQL 문의 CPU 시간이 짧더라도 총 CPU 시간이 매우 길어질 수 있습니다.

### 시스템 스레드
프로덕션 환경에서는 시스템 스레드 문제 발생은 그리 많지 않습니다. 일반적으로 여러 시스템 스레드의 CPU 사용률은 CVM에 사용 가능한 CPU 코어가 4개 이상 있는 한 동시에 너무 높거나 100%에 가까운 경우가 거의 없습니다. 그러나 아래 이미지와 같이 CPU 사용률에 영향을 줄 수 있는 몇 가지 bug가 있습니다.
![](https://main.qcloudimg.com/raw/e7c078a31b983fec2990801bfabde282.png)

## 해결 방법
대부분의 CPU 문제는 사용량이 많은 사용자 스레드로 인해 발생합니다. 다음 섹션에서는 사용자 스레드로 인해 발생하는 높은 CPU 사용률에 대한 솔루션에 중점을 둡니다.
- 슬로우 쿼리: 슬로우 쿼리를 식별하고 최적화하려면 DBbrain을 권장합니다. 자세한 내용은 [슬로우 쿼리](#mcx)를 참고하십시오.
- 과도한 계산: 많은 양의 데이터로 인해 발생하는 높은 CPU 사용률 문제를 해결하려면 [과도한 계산](#jsld)을 참고하십시오.
- 높은 QPS: 너무 많은 액세스 요청으로 인한 높은 CPU 사용률 문제를 해결하려면 [높은 QPS](#gqps)을 참고하십시오.

## 문제 해결 단계
### [슬로우 쿼리](id:mcx)
DBbrain을 사용하여 높은 CPU 사용률을 유발하는 SQL 문을 식별하고 최적화합니다.
- **예외 진단(권장)**: 이 기능은 7 * 24시간 예외를 감지 및 진단하고 실시간으로 최적화 제안을 제공합니다. 자세한 내용은 [Method 1 (recommended). Use the exception diagnosis feature to troubleshoot database exceptions](https://intl.cloud.tencent.com/document/product/1035/36053)를 참고하십시오.
- **슬로우 SQL 분석**: 이 기능은 현재 인스턴스의 느린 SQL 문을 분석하고 최적화 제안을 제공합니다. 자세한 내용은 [Method 2. Use the "slow SQL analysis" feature to troubleshoot SQL statements that lead to high CPU utilization](https://intl.cloud.tencent.com/document/product/1035/36053)을 참고하십시오.
- **감사 로그 분석**: 이 기능은 SQL 문에 대한 심층 분석을 수행하고 TencentDB 감사 데이터(전체 SQL)를 기반으로 최적화 제안을 제공합니다. 자세한 내용은 [Method 3. Use the "audit log analysis" feature to troubleshoot SQL statements that cause high CPU utilization](https://intl.cloud.tencent.com/document/product/1035/36053)을 참고하십시오.

MySQL에서는 슬로우 쿼리 시간(long_query_time)이 기본적으로 10s로 설정됩니다. 성능 문제가 발생한 후 슬로우 쿼리가 발견되지 않으면 매개변수 값을 1s로 조정한 후 비즈니스 사이클에서 슬로우 쿼리가 있는지 관찰하고 있는 경우 그에 따라 슬로우 쿼리를 최적화하는 것이 좋습니다. 매개변수를 조정한 후에도 여전히 슬로우 쿼리가 발견되지 않았지만 CPU 사용률이 높은 경우 데이터베이스의 전반적인 성능을 향상시키기 위해 CPU 구성을 업그레이드하는 것이 좋습니다.

### [과도한 계산](id:jsld)
MySQL이 방대한 양의 데이터를 처리할 때 인덱스와 쿼리 실행 계획이 잘 작동하더라도 CPU 사용률이 높을 수 있습니다. 또한 이러한 문제는 MySQL의 one-thread-per-connection 기능으로 인해 낮은 동시성에서도 여전히 발생할 수 있습니다.

일반적으로 두 가지 일반적인 솔루션이 있습니다.
- 읽기/쓰기 분리를 활성화합니다. 비즈니스 액세스 부하가 낮은 읽기 전용 복제본 노드에서 이 유형의 쿼리를 실행합니다.
- 큰 SQL 쿼리를 더 작은 쿼리로 분할하도록 프로그램을 최적화합니다.

### [높은 QPS](id:gqps)
- CPU 사양을 업그레이드하여 전체 데이터베이스 성능을 개선합니다.
- 읽기 전용 인스턴스를 사용하여 원본 인스턴스의 로드를 분담합니다.
- 쿼리 문을 최적화하여 효율성을 높입니다.


