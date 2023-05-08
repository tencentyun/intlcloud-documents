본문은 TencentDB for MySQL 커널의 버전 업데이트에 대해 설명합니다.
>?
>- TencentDB for MySQL 인스턴스의 마이너 커널 버전 업그레이드 방법에 대한 자세한 내용은 [커널 마이너 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/36816)를 참고하십시오.
>- 마이너 버전 업그레이드 시 일부 마이너 버전은 점검 중이라 선택이 불가할 수 있습니다. 콘솔에서 사용할 수 있는 마이너 버전이 우선됩니다.

<dx-tabs>
::: MySQL 8.0 커널 버전 릴리스 정보
<table>
<thead><tr><th>마이너 버전</th><th>설명</th></tr></thead>
<tbody>

<tr>	
<td>20220831</td>
<td><ul><li>새로운 기능</li><ul>
<li>MySQL 버전의 동적인 설정을 지원합니다.</li>
<li>투명한 열 암호화를 지원합니다. 테이블을 생성할 때 varchar 필드에 대한 encryption 속성을 지정할 수 있으며 스토리지 시스템이 열을 암호화합니다. 이 기능은 2023년에 상용화될 예정입니다.</li>
<li>도구 사용 중 내부 데이터 일관성을 위해 비교 SQL에 대한 구독으로 인해 발생하는 타사 데이터 구독 도구의 예외를 수정했습니다. <dx-alert infotype="explain" title="참고">데이터베이스 인스턴스가 마이그레이션, 업그레이드 또는 장애 후 복구된 후 시스템은 데이터 일관성을 확인하기 위해 데이터 일관성을 비교합니다. 비교 SQL이 `statement` 모드인 경우 `statement` 모드의 SQL에 대한 일부 타사 구독 툴의 응답으로 예외가 발생하기 쉽습니다. 인스턴스가 커널로 업그레이드되면 타사 데이터 구독 툴은 내부 데이터 일관성을 위해 비교 SQL을 구독할 수 없습니다.</dx-alert></li>
<li>NO_WAIT 추가 지원 | DDL 작업을 위한 WAIT [n]. 이렇게 하면 MDL 잠금을 얻을 수 없어 기다려야 하거나 MDL 잠금을 위해 지정된 시간을 기다린 경우 이러한 작업을 즉시 롤백할 수 있습니다.</li>
<li>쓰기보다 읽기가 많은 시나리오에 적합한 Fast Query Cache 기능을 지원합니다. 읽기보다 쓰기가 더 많거나, 데이터가 매우 자주 업데이트되거나, 쿼리 결과 집합이 매우 큰 경우 이 기능을 사용하지 않는 것이 좋습니다.</li>
<li>향상된 mts 교착 상태 감지를 지원합니다.</li>
<li><a href="https://www.tencentcloud.com/document/product/236/52512">병렬 쿼리</a>를 지원합니다. 이 기능을 사용하도록 설정하면 대용량 쿼리를 자동으로 식별할 수 있습니다. 병렬 쿼리 기능은 여러 컴퓨팅 코어를 활용하여 대규모 쿼리의 응답 시간을 크게 단축합니다.</li>
</ul>
<li>성능 최적화</li><ul>
<li>트랜잭션 시스템의 오버헤드를 최적화하여 스냅샷을 찍습니다. Copy Free Snapshot 방법을 채택하고 글로벌 활성 트랜잭션 hash에서 트랜잭션 지연을 삭제하고 스냅샷 촬영 방법을 최적화하여 스냅샷 이벤트의 논리적 타임스탬프를 결정합니다. sysbench에서 테스트한 바와 같이 극한의 성능은 read-write 시나리오에서 11% 증가했습니다.</li>
<li>prepared statement에 대한 권한 확인이 최적화되었습니다. 권한 버전 번호를 나타내기 위해 전역적으로 변수를 사용하고, prepared statement는 prepare 후 버전 번호를 기록하며, 시스템은 실행 중에 버전 번호가 변경되었는지 확인합니다. 권한 변경이 없으면 시스템은 권한 확인을 건너뜁니다. 그렇지 않으면 권한을 확인하고 버전 번호를 다시 기록합니다.</li>
<li>스레드 풀에서 시간 획득의 정확도를 최적화했습니다.</li>
<li>최적화된 기록 offset을 가져옵니다. 레코드 offset은 각 index에 대해 캐시됩니다. 조건이 충족되면 캐시된 offset이 직접 사용되어 rec_get_offsets() 함수를 호출하는 컴퓨팅 오버헤드를 줄입니다.</li>
<li>최적화된 Parallel DDL. <br>1. 인덱스 필드가 작은 경우 샘플링 빈도를 낮추기 위해 샘플링된 메모리 크기가 줄어듭니다. <br>2. 정렬에는 K-way 병합 알고리즘을 사용하여 병합 및 정렬의 라운드 수를 효과적으로 줄여 IO 수를 낮춥니다. <br>3. 레코드를 읽을 때 매번 각 레코드에 대한 offsets 생성을 방지하기 위해 고정 길이 offset이 캐시됩니다.</li>
<li>insert 성능을 향상시키기 위해 undo log 정보 기록 로직을 최적화했습니다.</li>
<li>반동기화가 활성화된 후 성능이 향상되었습니다.</li>
<li>감사 성능을 최적화하여 시스템 오버헤드를 줄였습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>가끔 Thread_memory 값이 비정상적으로 표시되던 문제를 수정했습니다.</li>
<li>배치 문 감사 중 timestamp가 정확하지 않은 문제를 수정했습니다.</li>
<li>두 번째 레벨에서 열 수정과 관련된 문제를 수정했습니다.</li>
<li>CREATE TABLE t1 AS SELECT ST_POINTFROMGEOHASH("0123", 4326); 문으로 인해 원본-복제본 연결이 끊어지는 문제가 수정되었습니다.</li>
<li>테이블 레벨에서 동시 요청 중에 복제본(slave)이 재시도하지 못하는 문제를 수정했습니다.</li>
<li>show slave hosts가 실행될 때 보고되는 Malformed packet 오류를 수정했습니다.</li>
<li>휴지통 문제를 수정했습니다.</li>
<li>jemalloc 메커니즘이 ARM 장치 모델에서 쉽게 OOM을 트리거하는 문제를 수정했습니다.</li>
<li>truncate pfs account table로 인해 통계 수집이 실패하는 문제를 수정했습니다.</li>
<li>휴지통에 외래 키 제약 조건이 있을 때 서브 테이블을 먼저 복구한 다음 상위 테이블을 복구하는 동안 발생하는 예외를 수정했습니다.</li>
<li>sql_mode 로그 문제를 수정했습니다.</li>
<li>CREATE DEFINER가 실행될 때 프로시저가 비정상이 되는 간헐적인 문제를 수정했습니다.</li>
<li>Copy Free Snapshot 문제를 수정했습니다.</li>
<li>스레드 풀의 성능 변동을 수정했습니다.</li>
<li>hash join+union의 결과가 비어 있을 수 있는 문제를 수정했습니다.</li>
<li>메모리 문제를 수정했습니다.</li>
</ul>
</td>
</tr>	

<tr>	
<td>20220401</td>
<td><ul><li>bug 수정</li><ul>
<li>FTS 인덱스를 생성할 때 Parallel DDL의 stage 변수 오류로 인한 stage null 포인터 crash 문제를 수정했습니다.</li>
<li>전체 텍스트 인덱스를 추가할 때 발생할 수 있는 crash를 수정했습니다.</li>
</ul></td>
</tr>	

<tr>	
<td>20220331</td>
<td><ul><li>bug 수정</li><ul>
<li>스레드 풀(Thread Pool)에서 와일드 포인터의 역참조로 인한 crash 문제를 수정했습니다.</li>
</ul></td>
</tr>

<tr>	
<td>20220330</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>기본적으로 writeset 병렬 복제를 활성화했습니다.</li>
<li>IO, 메모리 사용 비율 및 SQL 시간 초과 정책을 사용자 단위로 제어할 수 있는 확장된 리소스 그룹을 지원합니다.</li>
<li>UNDO 시간 범위 내에서 언제든지 데이터를 쿼리할 수 있는 플래시백 쿼리 기능을 지원합니다.</li>
<li>이 statement에 의해 작동되는 데이터 행을 반환할 수 있는 delete/insert/replace/update의 returning 구문을 지원합니다.</li>
<li>row 모드 gtid 복제 기능 확장을 지원합니다.</li>
<li>트랜잭션 잠금 최적화를 지원합니다.</li>
<li>휴지통 향상, 휴지통에서 truncate table과 테이블 자동 정리를 지원합니다.</li>
<li>parallel ddl 기능을 지원하여 3단계 병렬 처리를 통해 인덱스를 생성해야 하는 DDL 작업의 속도를 높였습니다.</li>
<li>빠른 인덱스 열 수정을 지원합니다.</li>
<li>자동 통계 수집 및 교차 시스템 통계 수집을 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>binlog_order_commits 비활성화 시 트랜잭션이 제출될 때 gtid에 대한 잠금 충돌이 최적화되었습니다.</li>
<li>InnoDB 실행 단계를 rseg의 단일 스레드 생성에서 멀티 스레드 생성으로 변경하여 MySQL 실행 시간을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>교착 상태 또는 잠금 대기 후 연결이 끊어지면 트랜잭션이 종료되지 않는 문제를 수정했습니다</li>
<li>innodb_row_lock_current_waits 값이 비정상적인 문제를 수정했습니다.</li>
<li>use database없이 감사 플러그인의 sql type 오류를 수정했습니다.</li>
<li>큰 테이블의 비동기 삭제 중에 innodb_async_table_size보다 작은 테이블도 rename되는 문제를 수정했습니다.</li>
<li> 감사 플러그인에 잘못된 이스케이프 문자가 포함된 문제를 수정했습니다.</li>
<li>빠른 열 수정 후 롤백 문제를 수정했습니다.</li>
<li>trx_sys close가 xa를 포함할 때 발생할 수 있는 crash를 수정했습니다.</li>
<li>merge derived table 시 발생하는 crash를 수정했습니다.</li>
<li>writeset이 활성화된 후 binlog_format을 수정하는 문제를 수정했습니다.</li>
<li>동일한 행에서 A->B->A->C 업데이트할 때 hash scan으로 인해 발생하는 오류(오류 코드: 1032)를 수정했습니다.</li>
<li>Prepared Statement 모드에서 정렬 인덱스가 유효하지 않을 수 있는 문제를 수정했습니다.</li>
<li>구체화된 결과를 소비하는 연산자는 구체화된 연산자의 반환 값 경로에 병합되어 실행 계획 이해 및 표시에 오류가 발생할 수 있는 문제를 수정했습니다.</li>
<li>큰 테이블의 비동기 삭제에 대한 극단적인 경우의 예외를 수정했습니다.</li>
<li>sql filter 설정 시 비정상적인 오류 메시지를 수정했습니다.</li>
<li>저장 프로시저 구문 분석 중에 보고된 구문 오류를 수정했습니다.</li>
<li>과거 히스토그램을 적용할 수 없는 문제를 수정했습니다.</li>
<li>SHOW SLAVE HOSTS(show replicas)의 Role 열 표시로 인한 호환성 문제를 수정했습니다.</li>
<li>열 수가 올바르지 않을 때 Item_in_subselect::single_value_transformer의 crash를 수정했습니다.</li>
<li>서브 테이블의 virtual column과 외래 키 열이 포함된 경우 캐스케이드 업데이트 중 메모리 누수로 인한 충돌이 수정되었습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20211202</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>빠른 열 수정을 지원합니다.</li>
<li>히스토그램 버전 관리를 지원합니다.</li>
<li>물리적 테이블의 무작위 샘플을 얻기 위한 SQL2003 TABLESAMPLE(단일 테이블) 샘플링 제어 구문을 지원합니다.</li>
<li>예약되지 않은 키워드 추가: TABLESAMPLE BERNOULLI.</li>
<li>주어진 입력 필드에 대한 히스토그램을 작성하기 위해 HISTOGRAM() 함수를 추가했습니다.</li>
<li>compressed 히스토그램을 지원합니다.</li>
<li>SQL 스로틀링을 지원합니다.</li>
<li>MySQL 클러스터 역할 구성 기능을 지원하며 기본 역할은 CDB_ROLE_UNKNOWN입니다.</li>
<li>역할을 표시하기 위해 show replicas 명령의 표시 결과에 새로운 Role 열이 추가되었습니다.</li>
<li>proxy를 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>insert on duplicate key update로 인한 핫스팟 업데이트 문제를 최적화했습니다.</li>
<li>event 같은 여러 개의 동일한 binlog event를 집계하여 hash scan의 애플리케이션을 가속화했습니다.</li>
<li>plan cache가 활성화되었을 때 스레드 풀 모드의 포인트 쿼리에서 prepare 문에 의한 메모리 사용량을 크게 줄였습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>핫스팟 업데이트 최적화가 활성화된 후 불안정한 성능 오류를 수정했습니다.</li>
<li>'select count(*)' 병렬 스캔이 극단적인 경우 전체 테이블을 스캔이 발생하는 문제가 수정되었습니다.</li>
<li>다양한 경우에 제로 통계 읽기로 인한 실행 계획 변경으로 인해 발생하는 성능 문제를 수정했습니다.</li>
<li>query가 오랫동안 query end 상태인 bug를 수정했습니다.</li>
<li>긴 기록에서 통계가 심각하게 과소평가되는 bug를 수정했습니다.</li>
<li>Temptable 엔진을 사용하고 선택한 열의 집계 함수 수가 255를 초과할 때 오류가 보고되는 bug를 수정했습니다.</li>
<li>json_table 함수에서 열 이름의 대소문자 구분 문제를 수정했습니다.</li>
<li>return true 시 표현식이 일찍 반환되어 윈도우 함수에서 정확성 문제를 일으키는 bug를 수정했습니다.</li>
<li>user variables가 포함된 경우 derived condition pushdown에 의한 푸시다운으로 인해 발생하는 정확성 문제를 수정했습니다.</li>
<li>Rule에 추가된 namespace가 없을 때 SQL filter가 crash하기 쉬운 문제를 수정했습니다.</li>
<li>높은 동시성 및 높은 충돌에서 스레드 풀(Thread Pool)이 활성화되었을 때 QPS 지터를 수정했습니다.</li>
<li>극단적인 경우(호스트 파일 시스템이 손상된 경우) 원본-복제 bp 풀 동기화에서 파일 핸들이 누출되는 문제를 수정했습니다.</li>
<li>index mapping 문제를 수정했습니다.</li>
<li>통계 캐시 동기화 문제를 수정했습니다.</li>
<li>update 문 또는 저장 프로시저를 실행하는 동안 정보가 지워지지 않을 때 발생하는 crash를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210830</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>사전 로딩된 행 수 제한을 지원했습니다.</li>
<li>계획 캐시 확인 최적화를 지원합니다.</li>
<li>확장된 ANALYZE 구문(UPDATE HISTOGRAM c USING DATA 'json') 및 히스토그램에 직접 쓰기를 지원합니다.
</li>
</ul>

<li>성능 최적화</li><ul>
<li>평가 오류 및 I/O 오버헤드를 줄이기 위해 인덱스 다이빙을 히스토그램으로 대체했습니다(이 기능은 기본적으로 활성화되어 있지 않음).</li>
</ul>

<li>bug 수정</li><ul>
<li>online-DDL 중에 통계 정보가 0이 될 수 있는 문제를 수정했습니다.</li>
<li>복제본 인스턴스에서 generated column이 업데이트되지 않는 문제를 수정했습니다.</li>
<li>binlog 압축 시 인스턴스 hang 문제를 수정했습니다.</li>
<li>새로 생성된 binlog 파일의 previous_gtids event에서 event 누락 문제를 수정했습니다.</li>
<li>시스템 변수가 수정되었을 때 발생할 수 있는 교착 상태를 수정했습니다.</li>
<li>show processlist에서 복제 인스턴스의 sql 스레드 info가 잘못 표시되는 문제를 수정했습니다.</li>
<li>MySQL 8.0.23에서 제공하는 hash join 관련 bugfix를 구현했습니다.</li>
<li>MySQL에서 제공하는 writeset 관련 bugfix를 구현했습니다.</li>
<li>MySQL 8.0.24에서 제공하는 쿼리 최적화 프로그램 관련 bugfix를 구현했습니다.</li>
<li>FAST DDL에서 flush list 최적화 및 릴리스 페이지의 동시성 bug를 수정했습니다.</li>
<li>테이블 수가 많은 인스턴스에서 데이터 사전 업데이트 중 메모리 사용량을 최적화했습니다.</li>
<li>instant add column 후 새 기본 키 생성으로 인한 crash를 수정했습니다.</li>
<li>전체 텍스트 인덱스 쿼리에서 메모리 증가로 인한 OOM을 수정했습니다.</li>
<li>show processlist에서 반환된 결과 집합의 TIME 필드에 -1이 포함된 문제를 수정했습니다.</li>
<li>히스토그램 호환성으로 인해 테이블이 열리지 않는 문제를 수정했습니다.</li>
<li>Singleton 히스토그램이 구성될 때 부동 소수점 누적 오류를 수정했습니다.</li>
<li>row 형식 로그의 테이블 이름에 한자를 많이 사용하여 복제가 중단되는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210330</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>지원되는 원본-복제 bp 풀 동기화: 고가용성(HA) 원본-복제 전환이 발생한 후 일반적으로 복제본을 warmup하는 데, 즉 핫스팟 데이터를 buffer pool에 로딩하는 데 오랜 시간이 걸립니다. 복제본의 워밍업을 가속화하기 위해 TXSQL은 이제 원본과 복제본 간의 bp 풀 동기화를 지원합니다.</li>
<li>Sort Merge Join 기능을 지원합니다.</li>
<li>FAST DDL 작업을 지원합니다.</li>
<li>character_set_client_handshake 매개변수 값 쿼리를 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>인덱스를 생성하는 동안 성능 변동 문제를 해결하여 시스템 안정성을 향상시키기 위해 flush list에서 추적된 더티 페이지를 스캔하고 플러시하는 메커니즘을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>offline_mode 및 cdb_working_mode의 매개변수 수정으로 인해 발생하는 교착 상태를 수정했습니다.</li>
<li>글로벌 객체 trx_sys의 max_trx_id를 지속적으로 저장하는 동안 동시성 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20201230</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>MySQL <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-19.html" target="_blank">8.0.19</a>, <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-20.html" target="_blank">8.0.20</a>, <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-21.html" target="_blank">8.0.21</a>, <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-22.html" target="_blank">8.0.22</a>의 공식 업데이트를 지원합니다.</li>
<li>thread_handling 매개변수를 사용하여 스레드 풀링 모드 또는 연결 풀링 모드의 동적 설정을 지원했습니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>쓰기 성능을 개선하기 위해BINLOG LOCK_done 충돌을 최적화했습니다.</li>
<li>Lock Free Hash를 사용해 trx_sys mutex 충돌을 최적화하고 성능을 개선했습니다.</li>
<li>redo log 플러시를 최적화했습니다.</li>
<li>buffer pool 초기화 시간을 최적화했습니다.</li>
<li>큰 테이블에서 drop table 작업 중 어댑티브 해시 인덱스(AHI) 지우기를 최적화했습니다.</li>
<li>감사 성능을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>innodb 임시 테이블 정리 시 성능 변동이 수정되었습니다.</li>
<li>인스턴스에 코어가 많을 때 read only 성능 저하를 수정했습니다.</li>
<li>hash scan으로 인한 오류(오류 코드: 1032)를 수정했습니다.</li>
<li>핫스팟 업데이트로 인한 동시성 보안 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200630</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>큰 테이블의 비동기 드롭 지원: 큰 테이블 삭제로 인한 비즈니스 성능 변동을 피하기 위해 파일을 비동기식으로 천천히 지울 수 있습니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>리소스 충돌을 줄이기 위해 유휴 작업의 자동 kill을 지원합니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>투명한 데이터 암호화(TDE)를 지원합니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>relay_log_pos & master_log_pos 사이의 체크포인트가 일치하지 않아 전환이 실패하는 문제를 수정했습니다.</li>
<li>디스크에 데이터를 비동기식으로 저장하여 발생하는 데이터 파일 오류를 수정했습니다.</li>
<li>fsync가 EIO를 반환하고 재시도가 반복되는 경우의 하드 오류를 수정했습니다.</li>
<li>전체 텍스트 인덱스의 멀티바이트 문자 세트에서 구 검색(phrase search)으로 인한 충돌을 수정했습니다.</li>
</ul>
</td>
</tr>
</tbody></table>
:::
::: MySQL 5.7 커널 버전 릴리스 정보
<table>
<thead><tr><th>마이너 버전</th><th>설명</th></tr></thead>
<tbody>

<tr>	
<td>20220716</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>InnoDB에 대한 자동 증분 열 지속성을 지원합니다.</li>
<li>정확한 메모리 통계를 지원합니다.</li>
<li>Query 레벨 메모리 모니터링을 지원합니다.</li>
<li>휴지통을 지원합니다.</li>
<li>병렬 DDL 문을 지원합니다.</li>
<li>플래시백 쿼리를 지원합니다.</li>
<li>내부 xa 트랜잭션에 대한 비동기 롤백을 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>큰 테이블의 최적화된 비동기 드롭. <br>큰 테이블의 원래 정의는 50G이며 이제 innodb_async_table_size로 제어하여 더 유연하게 만들 수 있습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>인덱스 생성을 위해 alter table을 실행할 때 ERROR 1878 (HY000): Temporary file write failure가 보고되는 문제를 수정했습니다.</li>
<li>PFS 메모리 모니터링 데이터에서 buf/buf/pool을 볼 수 없는 문제를 수정했습니다.</li>
<li>권한 확인으로 인해 일부 시나리오에서 returning 문으로 인해 예외가 발생할 수 있는 문제를 수정했습니다.</li>
<li>parser가 문의 세미콜론을 올바르게 처리하지 않아 오류가 보고되는 문제를 수정했습니다.</li>
<li>감사 명세서의 작은따옴표가 이스케이프되지 않는 문제를 수정했습니다.</li>
<li>ARM 플랫폼에서 갑자기 메모리 사용량이 증가하는 문제를 수정했습니다.</li>
<li>writeset이 활성화된 후 binlog_format을 수정하여 발생하는 원본-복제본 불일치 문제를 수정했습니다.</li>
<li>많은 수의 스레드를 동시에 종료하여 발생하는 높은 CPU 사용량 문제를 수정했습니다.</li>
<li>drop table partiton force와 관련된 bug를 수정했습니다.</li>
<li>binlog dump가 멈추고 인스턴스 재시작이 느려지는 문제를 수정했습니다.</li>
<li>create table like temporary table이 binlog의 문자 세트를 상속하지 않았기 때문에 원본-복제본 동기화가 실패하는 문제를 수정했습니다.</li>
<li>show detail processlist에 잘못된 문자가 표시되는 문제를 수정했습니다.</li>
<li>경우에 따라 스레드 풀이 닫힐 때 thread_group 잠금이 해제되지 않는 문제를 수정했습니다.</li>
<li>병렬 table 레벨에서 부모 테이블을 업데이트하면 인스턴스가 비정상적으로 실행되는 문제가 수정되었습니다.</li>
<li>복제본(slave)에서 가상 열이 잘못 계산되는 문제를 수정했습니다.</li>
<li>gtid_subset이 행을 실행한 후 null_value를 false로 설정하지 않는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20211230</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>MySQL <a href="https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-19.html" target="_blank">5.7.19</a>에서 <a href="https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-36.html" target="_blank">5.7.36</a>으로 공식 업데이트를 지원합니다.</li>
<li>HA 전환 후 성능 복구 속도를 높이기 위해 원본-복제 buffer pool 동기화를 지원합니다(네이티브 모드보다 약 90초 더 빠름).</li>
<li>백업 중 서비스 가용성을 향상시키기 위해 경량 메타데이터 잠금을 제공하는 backup lock 기능을 추가했습니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>read_write 시나리오에서 UTF_8 함수의 성능을 최적화하기 위해 utf8/utf8mb4 my_charpos 인라인과 관련된 함수를 만들었습니다.
<li>jemalloc 버전을 5.2.1로 업그레이드했습니다.</li>
<li>binlog rotate 시 파일 번호 가져오기를 최적화했습니다.</li>
<li>반동기화 복제본 io(slave io)을 최적화했습니다.</li>
<li>hash scan 집계를 최적화했습니다.</li>
<li>대규모 트랜잭션에 대한 crash recover 시작을 가속화했습니다.</li>
</ul>

<tr>	
<td>20211102</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>도구 사용 중 내부 데이터 일관성을 위해 비교 SQL에 대한 구독으로 인해 발생하는 타사 데이터 구독 도구의 예외를 수정했습니다. <dx-alert infotype="explain" title="참고">데이터베이스 인스턴스가 마이그레이션, 업그레이드 또는 장애 후 복구된 후 시스템은 데이터 일관성을 확인하기 위해 데이터 일관성을 비교합니다. 비교 SQL이 `statement` 모드인 경우 `statement` 모드의 SQL에 대한 일부 타사 구독 툴의 응답으로 예외가 발생하기 쉽습니다. 인스턴스가 커널로 업그레이드되면 타사 데이터 구독 툴은 내부 데이터 일관성을 위해 비교 SQL을 구독할 수 없습니다.</dx-alert></li>
</ul>
</td>
</tr>

<tr>	
<td>20211031</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>writeset 복제를 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>백업 성공률을 높이기 위해 checkpoint 메커니즘을 최적화했습니다.</li>
<li>hash scan 인덱스 선택을 최적화했습니다.</li>
<li>insert on duplicate key update를 지원하도록 핫스팟 업데이트 성능을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>핫스팟 업데이트가 활성화된 후 불안정한 성능 오류를 수정했습니다.</li>
<li>instant ddl 이후 update 작업을 롤백하여 발생하는 crash를 수정했습니다.</li>
<li>열 압축이 활성화된 후 create table select 문이 압축 속성을 상속하지 않는 문제를 수정했습니다.</li>
<li>skip-grant-table 옵션이 활성화된 후 show variables like 'tencent_root%’ 문으로 인해 발생하는 인스턴스 crash를 수정했습니다.</li>
<li>read only 모드에서 Query Rewriter 플러그인의 crash를 수정했습니다.</li>
<li>파티션 테이블의 hash scan으로 인해 발생한 오류(오류 코드: 1032)를 수정했습니다.</li>
<li>mts 모드에서 첫 번째 대규모 트랜잭션의 sbm이 0인 문제를 수정했습니다.</li>
<li>slave_preserve_commit_order=ON 및 slave_transaction_retries=0으로 인한 stop slave 충돌을 수정했습니다.</li>
<li>몇 가지 XA 트랜잭션 bug를 수정했습니다.</li>
<li>default 값이 있는 json 필드가 생성된 후 show create 중에 SQL 스플라이싱이 잘못되는 문제를 수정했습니다.</li>
<li>트랜잭션이 차단된 후 연결이 끊긴 트랜잭션을 롤백할 수 없는 문제를 수정했습니다.</li>
<li>innodb persistent 모드에서 긴 기록 아래에서 통계가 0이 될 수 있는 문제를 수정했습니다.</li>
<li>ANALYZE TABLE이 쿼리 힙을 유발할 수 있는 문제를 수정하기 위해 8.0을 포팅했습니다.</li>
<li>변경 후 Server 레이어에 innodb 통계를 동기화할 수 없는 문제를 수정했습니다.</li>
<li>통계 샘플링이 너무 오랫동안 쓰기를 차단하고 크래쉬를 일으킬 수 있는 문제를 수정했습니다(Bug#31889883).</li>
<li>innodb 통계 업데이트 프로세스 중에 0행을 읽을 가능성을 수정했습니다(BUG#105224).</li>
<li>MVCC에서 가능한 O(N^2) 동작을 수정했습니다(Bug#28825617).</li>
<li>연결이 해제되었을 때 임시 테이블을 닫고 binlog rotate를 트리거하여 발생하는 crash를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210630</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>현재 복제본(slave)이 재생한 binlog 타임스탬프를 하기 위해 SHOW SLAVE DETAIL [FOR CHANNEL channel] 명령이 추가되었습니다.</li>
<li>transaction_read_only/transaction_isolation 매개변수를 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>여러 개의 동일한 binlog event를 집계하여 복제본(slave)에 대한 hash scan의 애플리케이션을 가속화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>중복 기본 키가 존재하고 열을 찾을 수 없으며 UPDATE 문으로 인해 임시 테이블에서 열이 너무 긴 문제를 수정했습니다.</li>
<li>DDL 프로세스 중에 통계가 0이 될 수 있는 문제를 수정했습니다.</li>
<li>연결 상태 통계에서 부정확한 undo log size를 수정했습니다.</li>
<li>metadata_locks 테이블 쿼리로 인해 발생하는 인스턴스 crash를 수정했습니다.</li>
<li>of를 예약되지 않은 키워드로 수정했습니다.</li>
<li>동적으로 수정된 버전 번호가 새 연결에서 올바르게 표시되지 않는 문제를 수정했습니다.</li>
<li>page_cache cleanning 액세스의 와일드 포인터를 수정했습니다.</li>
<li>alter table 실행 시 ‘Incorrect key file for table’ 오류가 보고될 수 있는 문제를 수정했습니다.</li>
<li>파티션 테이블의 과도한 메모리 사용을 수정했습니다.</li>
<li>show processlist에서 반환된 결과 집합의 TIME 필드에 -1이 포함된 문제를 수정했습니다.</li>
<li>복제본(slave) 노드에서 XA 트랜잭션 복제의 잠금 대기를 수정했습니다.</li>
<li>equal range 쿼리에서 파티션 테이블의 잘못된 잠금을 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210331</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>statment에 의해 수정된 데이터 행을 검색하기 위해 delete/insert/replace 문에서 returning을 지원합니다. delete의 경우 반환된 데이터 행은 사전 이미지이고 insert/replace의 경우 사후 이미지입니다.</li>
<li>열 압축 기능 지원: 행 압축 및 데이터 페이지 압축은 이미 지원되지만 테이블의 작은 필드는 자주 읽고 쓰는 반면 큰 필드는 그렇지 않은 경우 두 압축 방법 모두 많은 컴퓨팅 리소스를 낭비합니다. 반대로 열 압축은 자주 액세스하지 않는 큰 필드를 압축하고 필드의 전체 행을 저장하는 공간을 줄여 읽기 및 쓰기 액세스 효율성을 향상시킬 수 있습니다.</li>
<li>character_set_client_handshake 매개변수 값 쿼리를 지원합니다.</li>
<li>슬라이딩 윈도우 기법을 기반으로 하는 posix_fadvise 함수를 사용하여 로그 파일이 차지하는 page cache의 수동 지우기를 지원하여 운영 체제의 메모리 압력을 낮추고 인스턴스 안정성을 개선했습니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>CREATE INDEX의 병렬성 최적화: 인덱스를 생성하는 과정에서 임시 테이블에 병합 정렬이 필요하므로 시간이 많이 걸립니다. 이 문제를 해결하기 위해 이제 병렬 임시 테이블 병합 정렬 알고리즘이 지원되어 시간이 50% 이상 단축되었습니다.</li>
<li>인덱스를 생성하는 동안 성능 변동 문제를 해결하여 시스템 안정성을 향상시키기 위해 flush list에서 추적된 더티 페이지를 스캔하고 플러시하는 메커니즘을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>메모리 누수 문제를 수정했습니다.</li>
<li>json 사용의 안정성을 개선하기 위해 MySQL 8.0에서 제공되는 json 버그 수정을 구현했습니다.</li>
<li>hash scan으로 인한 오류(오류 코드: 1032)를 수정했습니다.</li>
<li>핫스팟 업데이트로 인한 동시성 보안 문제를 수정했습니다.</li>
<li>MySQL에서 제공하는 gcol bug 수정을 일괄적으로 구현했습니다.</li>
<li>경우에 따라 datetime 데이터와 String 데이터를 비교하지 못하는 문제를 수정했습니다.</li>
<li>원본-복제 bp 풀 동기화가 활성화된 경우 파일 핸들을 해제할 수 없는 bug를 수정했습니다.</li>
<li>offline_mode 매개변수를 설정하고 동시에 연결을 생성하여 발생하는 교착 상태 bug를 수정했습니다.</li>
<li>동시 범위 쿼리에 잘못 설정된 m_end_range 매개변수로 인해 발생하는 crash를 수정했습니다.</li>
<li>groupby 절에 json 열이 나타나는 경우 temporay table에서 update 문을 실행하는 데 시간이 오래 걸리는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20201231</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>SELECT FOR UPDATE/SHARE 문에서 NOWAIT 및 SKIP LOCKED 사용이 지원됩니다.</li>
<li>thread_handling 매개변수를 사용하여 스레드 풀링 모드 또는 연결 풀링 모드의 동적 설정을 지원했습니다.</li>
<li>원본-복제 buffer pool 동기화를 지원합니다.</li>
<li>사용자 연결 상태 모니터링을 지원합니다. 모니터링 항목에는 동기/비동기 IO, 메모리, 로그 크기, CPU 시간, 잠금 기간 등이 포함됩니다.
</li>
</ul>

<li>성능 최적화</li><ul>
<li>높은 동시성 성능을 개선하기 위해 트랜잭션 서브 시스템을 최적화했습니다.</li>
<li>대규모 트랜잭션의 crash recover 시작 시간을 최적화했습니다.</li>
<li>redo log 플러시를 최적화했습니다.</li>
<li>buffer pool 초기화 시간을 최적화했습니다.</li>
<li>utf8/utf8mb4 문자열 효율성을 최적화했습니다.</li>
<li>감사 성능을 최적화했습니다.</li>
<li>gtid_purged 값이 비어 있는 것에 대한 제한을 철회했습니다.</li>
<li>백업 잠금 최적화: LOCK TABLES FOR BACKUP, LOCK BINLOG FOR BACKUP 및 UNLOCK BINLOG가 지원됩니다. FLUSH TABLES WITH READ LOCK은 데이터베이스 백업을 위해 사용되지만 전체 데이터베이스가 서비스를 제공하지 못하도록 차단합니다. 반대로 위의 세 문은 데이터베이스가 서비스를 제공할 수 있도록 하면서 물리적/논리적 백업 중에 데이터 일관성을 보장하기 위해 경량 백업 잠금을 사용합니다.</li>
<li>큰 테이블에서 drop table 작업을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>performance_schema 쿼리 시 hang 문제를 수정했습니다.</li>
<li>digest_add_token 기능의 overflow를 수정했습니다.</li>
<li>truncate table 문을 사용하여 ibuf에 액세스할 때 발생하는 crash를 수정했습니다.</li>
<li>left join 문의 const가 예상보다 일찍 계산될 때 잘못된 쿼리를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200930</td>
<td>
<ul><li>성능 최적화</li><ul>
<li>백업 잠금을 최적화했습니다. FLUSH TABLES WITH READ LOCK은 데이터베이스 백업을 위해 사용되지만 전체 데이터베이스가 서비스를 제공하지 못하도록 차단합니다. 따라서 이 버전에서는 경량 백업 잠금이 제공됩니다.</li>
<li>큰 테이블에서 drop table 작업을 최적화했습니다. innodb_fast_ahi_cleanup_for_drop_table 매개변수는 큰 테이블을 drop할 때 어댑티브 해시 인덱스를 정리하는 데 걸리는 시간을 크게 줄이는 데 도움이 됩니다.
</li>
</ul>

<li>bug 수정</li><ul>
<li>truncate table 문을 사용하여 ibuf에 액세스할 때 발생하는 crash를 수정했습니다.</li>
<li>빠른 열 추가 기능이 활성화된 경우 콜드 백업 실패를 수정했습니다.</li>
<li>innodb 메모리 테이블 객체의 빈번한 릴리스로 발생하는 성능 저하를 수정했습니다.</li>
<li>left join 문의 const가 예상보다 일찍 계산될 때 잘못된 쿼리를 수정했습니다.</li>
<li>sql throttling 및 query rewrite 간의 Rule 클래스 이름 충돌로 인해 발생하는 core 문제를 수정했습니다.</li>
<li>여러 session에서 insert on duplicate key update 문으로 인해 발생하는 동시 업데이트 문제를 수정했습니다.</li>
<li>auto_increment_increment 열에 데이터를 동시에 삽입하여 발생하는 duplicate key error를 수정했습니다.</li>
<li>innodb 메모리 객체를 제거하여 발생하는 충돌을 수정했습니다.</li>
<li>핫스팟 업데이트로 인한 동시성 보안 문제를 수정했습니다.</li>
<li>jemalloc을 v5.2.1로 업그레이드한 후 스레드 풀을 활성화할 때 coredump 문제를 수정했습니다.</li>
<li>fwrite 오류 없는 처리로 인해 불완전한 감사 로그가 수정되었습니다.</li>
<li>mysqld_safe가 root로 시작될 때 로그를 인쇄하지 못하는 문제를 수정했습니다.</li>
<li>alter table exchange partition으로 인한 ddl log 파일의 크기 증가를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200701</td>
<td>
<ul><li>bug 수정</li><ul>
<li>INNOBASE_SHARE index mapping 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200630</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>SELECT FOR UPDATE/SHARE 문에서 NOWAIT 및 SKIP LOCKED 사용을 지원합니다.</li>
<li>대규모 트랜잭션으로 인한 원본-복제 지연 및 백업 실패와 같은 문제를 해결할 수 있는 대규모 트랜잭션 최적화를 지원합니다.</li>
<li>최적화된 감사 성능: 비동기 감사가 지원됩니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>digest_add_token 기능의 오버플로를 수정했습니다.</li>
<li>insert blob으로 인한 인스턴스 crash를 수정했습니다.</li>
<li>event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 원본-복제본 복제 중단을 수정했습니다.</li>
<li>performance_schema 쿼리 시 hang 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200331</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>공식 MySQL 5.7.22 버전의 JSON 시리즈 기능을 추가했습니다.</li>
<li>전자상거래 플래시 세일 시나리오를 위해 실시간 세션에 설명된 대로 <a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">Hotspot update</a> 기능을 지원합니다.</li>
<li>실시간 세션에 설명된 대로 <a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">SQL throttling</a> 기능을 지원합니다.</li>
<li>사용자 지정 KMS 키로 암호화를 지원합니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>전체 텍스트 인덱스의 멀티바이트 문자 세트에서 구 검색(phrase search)으로 인한 충돌을 수정했습니다.</li>
<li>높은 동시성 시나리오에서 CATS(Contention-Aware Transaction Scheduling) 잠금 스케쥴링 모듈의 crash를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190830</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>손상된 데이터를 건너뛰고 binlog가 손상되었을 때 구문 분석을 계속하도록 지원했습니다. 소스 인스턴스와 binlog가 모두 손상된 경우 이 기능은 가능한 한 많이 사용하기 위해 복제본 데이터베이스에서 데이터를 복원하는 데 도움이 됩니다.</li>
<li>non-GTID에서 GTID 모드로 데이터 동기화를 지원했습니다.</li>
<li>show full processlist 문을 실행하여 ‘사용자 스레드 메모리 사용량’ 쿼리를 지원했습니다.</li>
<li>테이블에 대한 <a href="https://intl.cloud.tencent.com/document/product/236/35988" target="_blank">빠른 칼럼 추가</a>를 지원합니다. 이 기능은 데이터를 복제하거나 디스크 용량 I/O를 사용하지 않으며 사용량이 많은 시간에 실시간으로 변경 사항을 구현할 수 있습니다.</li>
<li>지속적인 자동 증분 값을 지원합니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>Grant 문의 열 이름에 예약어가 포함된 경우 복제가 중단되는 문제를 수정했습니다.</li>
<li>파티션 테이블에서 역방향 스캔을 수행할 때 SQL 실행 효율성이 떨어지는 문제를 수정했습니다.</li>
<li>가상 열 인덱스 및 기본 키 사용 시 데이터 불일치로 인해 쿼리 결과에 예외가 발생하는 문제를 수정했습니다.</li>
<li>InnoDB 기본 키 범위 쿼리로 인해 데이터가 누락되는 문제를 수정했습니다.</li>
<li>공간 인덱스가 있는 테이블에 대해 DDL 문을 실행할 때 시스템 crash 문제를 수정했습니다.</li>
<li>binlog 크기가 너무 크고 하트비트 정보의 파일 길이가 한도를 초과한 경우 원본-복제 연결 끊김이 발생하는 문제를 수정했습니다.</li>
<li>event 삭제 시 다른 event가 예정대로 실행되지 않는 문제를 수정했습니다.</li>
<li>집계 쿼리 결과가 올바르지 않은 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190615</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>투명한 데이터 암호화(TDE)를 지원합니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190430</td>
<td>
<ul><li>bug 수정</li><ul>
<li>서브 쿼리에서 긴 텍스트 기능을 사용할 때 null 포인터 참조가 발생하는 문제를 수정했습니다.</li>
<li>Hash Scan으로 인해 원본-복제 연결이 끊어지는 문제를 수정했습니다.</li>
<li>원본 binlog 전환으로 인해 복제(slave) I/O 스레드가 중단되는 문제를 수정했습니다.</li>
<li>NAME_CONST 사용으로 인한 crash를 수정했습니다.</li>
<li>문자 세트로 인한 illegal mix of collation 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190203</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>큰 테이블의 비동기 드롭 지원: 큰 테이블 삭제로 인한 비즈니스 성능 변동을 피하기 위해 파일을 비동기식으로 천천히 지울 수 있습니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>CATS 잠금 스케쥴링을 지원합니다.</li>
<li>GTID가 활성화된 경우 트랜잭션에서 임시 테이블 및 CTS 구문 생성 및 삭제를 지원했습니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>암시적 기본 키를 지원합니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>cdb_kill_user_extra 매개변수(기본값: root@%)를 구성하여 다른 사용자의 세션을 kill할 수 있는 super 권한이 없는 사용자를 지원합니다.</li>
<li>엔터프라이즈급 암호화 함수를 지원합니다. 해당 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
</ul>

<li>bug 수정</li><ul>
<li>binlog 캐시 파일 공간이 부족할 때 복제가 중단되는 문제를 수정했습니다.</li>
<li>fsync가 EIO를 반환하고 재시도가 반복되는 경우의 하드 오류를 수정했습니다.</li>
<li>복제가 중단되고 GTID 홀(Hole)로 인해 복구할 수 없는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180918</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>리소스 충돌을 줄이기 위해 유휴 트랜잭션 자동 kill을 지원합니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>저장 엔진을 MEMORY에서 InnoDB로 자동 변경 지원: 전역 변수 cdb_convert_memory_to_innodb가 ON이면 테이블이 생성되거나 수정될 때 엔진이 MEMORY에서 InnoDB로 변경됩니다.</li>
<li>보이지 않는 인덱스를 지원합니다.</li>
<li>jlibc 메모리 관리 모듈을 대체하여 메모리 사용량을 줄이고 할당 효율성을 높일 수 있는 jemalloc으로 메모리 관리를 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>rotate HOLDLOCK 기간을 줄이고 시스템 성능을 개선하도록 binlog 스위치를 최적화했습니다.</li>
<li>Crash Recovery 속도를 향상시켰습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>원본-복제 전환으로 인해 event가 무효화되는 문제를 수정했습니다.</li>
<li>REPLAY LOG RECORD로 인한 Crash를 수정했습니다.</li>
<li>Loose index scans로 인해 쿼리 결과가 올바르지 않은 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180530</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>SQL 감사를 지원합니다.</li>
<li>테이블 수준의 동시 복제를 지원합니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
</ul>

<li>성능 최적화</li><ul>
<li>복제본(slave) 인스턴스 잠금을 최적화하여 복제본(slave) 인스턴스의 성능 동기화를 개선합니다.</li>
<li>select ... limit 문의 푸시다운을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>relay_log_pos & master_log_pos 사이의 체크포인트가 일치하지 않아 전환이 실패하는 문제를 수정했습니다.</li>
<li>Crash on UPDATE ON DUPLICATE KEY로 인한 Crash를 수정했습니다.</li>
<li>JSON 열을 가져올 때 ‘Invalid escape character in string.’ 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20171130</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>현재 인스턴스에서 MDL 부여 및 대기 상태를 쿼리하기 위해 information_schema.metadata_locks 뷰를 지원합니다.</li>
<li> DDL 작업 대기 시간 초과를 허용하기 위해 ALTER TABLE NO_WAIT | TIMEOUT 구문을 지원합니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>스레드 풀을 지원합니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.
</ul>

<li>bug 수정</li><ul>
<li>bytes_data를 기반으로 계산하여 innodb_buffer_pool_pages_data 매개변수 오버플로우(overflow) 오류를 수정했습니다.</li>
<li>비동기 모드에서 속도 제한 플러그인을 사용할 수 없게 되는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

</tbody></table>
:::
::: MySQL 5.6 커널 버전 릴리스 정보
<table>
<thead><tr><th>마이너 버전</th><th>설명</th></tr></thead>
<tbody>

<tr>	
<td>20220303</td>
<td>
<ul><li>Bug 수정</li><ul>
<li>빅 테이블의 비동기 삭제 시 mem_strdup에 의해 할당된 메모리가 row_mysql_truncate_t::file_name에 사용될 때 발생하는 비정상적인 릴리스가 수정되었습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20220302</td>
<td>
<ul><li>Bug 수정</li><ul>
<li>sql_update.cc의 메모리 누수 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20220301</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>동적 매개변수 innodb_spin_wait_pause_multiplier를 사용하여 스핀 주기(0–100)를 동적으로 구성할 수 있습니다. <br>이 매개변수는 임시 조정에 사용되며 콘솔을 통한 변경 수정을 지원하지 않습니다.</li>
<li>교착 상태 루프 정보 인쇄를 지원합니다. <br>innodb_print_dead_lock_loop_info 매개변수를 통해 이 기능을 활성화한 후 교착 상태가 발생하면 show engine innodb status를 실행하여 교착 상태 루프 정보를 볼 수 있습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>복제본(slave) 재시작 후 memory 테이블에서 익명의 GTID 트랜잭션이 생성되는 문제를 수정했습니다.</li>
<li>root@localhost 권한 누락으로 인해 업그레이드가 실패하는 문제를 수정했습니다.</li>
<li>innodb_row_lock_current_waits 등 모니터링 변수의 값이 비정상적이던 문제를 수정했습니다.</li>
<li>감사 플러그인의 sql type 매핑 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20211030</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>대형 트랜잭션 복제 최적화를 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>hash scan의 애플리케이션 속도를 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>많은 수의 테이블 쿼리로 인해 발생하는 OOM을 수정했습니다.</li>
<li>innodb_thread_concurrecy를 0으로 설정하여 발생하는 무한 루프 오류를 수정했습니다.</li>
<li>긴 기록의 통계가 0이던 문제를 수정했습니다.</li>
<li>sbm 점프 오류를 수정했습니다.</li>
<li>LOCK_binlog_end_pos hang 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210630</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>대형 트랜잭션 복제 최적화를 지원합니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>index merge가 활성화되었을 때 잘못된 복사를 수정했습니다.</li>
<li>row 모드에서 cdb_more_gtid_feature_supported가 활성화되었을 때 create table select 실행 중단으로 인해 복제가 중단되는 문제를 수정했습니다.</li>
<li>show create table에서 max(id)가 AUTO_INCREMENT보다 큰 Bug를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20201231</td>
<td>
<ul><li>bug 수정</li><ul>
<li>hash scan으로 인한 오류(오류 코드: 1032)를 수정했습니다.</li>
<li>replace into가 row 기반 복제에서 auto increment 열을 업데이트하지 않는 문제를 수정했습니다.</li>
<li>SQL 문 구문 분석을 위해 요청된 메모리를 해제하지 않아 발생하는 메모리 누수를 수정했습니다.</li>
<li>create table as select를 실행할 때 sql mode 검사를 건너뛰는 문제를 수정했습니다.</li>
<li>기본값 Insert 시 sql mode 검사를 건너뛰는 문제를 수정했습니다.</li>
<li>바운드 매개변수로 update를 실행할 때 sql mode 검사를 건너뛰는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200915</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>실시간 세션에 설명된 대로 <a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">SQL throttling</a> 기능을 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>buffer pool의 초기화 가속을 최적화했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>원본과 복제본 모두에서 rename table의 hang 문제를 수정했습니다.</li>
<li>event_scheduler가 disable로 설정되고 cdb_skip_event_scheduler가 on에서 off로 변경될 때 crash가 수정되었습니다.</li>
<li>srv_max_n_threads에서 tencentroot의 최대 연결 수가 계산되지 않을 때 sync_wait_array 어설션 실패를 수정했습니다.</li>
<li>TencentDB for MySQL v5.6과 다른 클라우드 벤더의 MySQL v5.6 사이의 시스템 테이블 구조 불일치로 인해 발생하는 원본-복제 병렬 복제 crash를 수정했습니다.</li>
<li>INSERT ON DUPLICATE KEY UPDATE THE WRONG ROW 오류를 수정했습니다.</li>
<li>index_mapping 오류를 수정했습니다.</li>
<li>mtr bug를 수정했습니다.</li>
<li>event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 원본-복제본 복제 중단을 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190930</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>show full processlist 문을 실행하여 ‘사용자 스레드 메모리 사용량’ 쿼리를 지원합니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>레플리카의 replication filter로 인해 발생한 gtid hole을 수정했습니다.</li>
<li>Binlog 크기가 너무 크고 하트비트 정보의 파일 길이가 한도를 초과한 경우 원본-복제 연결 끊김이 발생하는 문제를 수정했습니다.</li>
<li>문자 세트로 인한 illegal mix of collation 오류를 수정했습니다.</li>
<li>Hash Scan으로 인해 원본-복제 연결이 끊어지는 문제를 수정했습니다.</li>
<li>NAME_CONST 사용으로 인한 crash를 수정했습니다.</li>
<li>원본 binlog 전환으로 인해 복제(slave) I/O 스레드가 중단되는 문제를 수정했습니다.</li>
<li>innodb_log_checusum으로 인해 호환되지 않는 백업 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190530</td>
<td>
<ul><li>bug 수정</li><ul>
<li>RC 모드에서 더티 데이터를 읽을 수 있는 문제를 수정했습니다.</li>
<li>임시 테이블 삭제로 인해 복제본 인스턴스 재생이 실패할 수 있는 문제를 수정했습니다.</li>
<li>높은 동시성에서 교착 상태의 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190203</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>큰 테이블의 비동기 드롭 지원: 큰 테이블 삭제로 인한 비즈니스 성능 변동을 피하기 위해 파일을 비동기식으로 천천히 지울 수 있습니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>cdb_kill_user_extra 매개변수(기본값: root@%)를 구성하여 다른 사용자의 세션을 kill할 수 있는 super 권한이 없는 사용자를 지원합니다.</li>
<li>GTID가 활성화된 경우 트랜잭션에서 임시 테이블 및 CTS 구문 생성 및 삭제를 지원했습니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
</ul>

<li>성능 최적화</li><ul>
<li>파티션 테이블의 복제 및 재생을 최적화하여 효율성을 높였습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>임시 공간 부족으로 인해 원본과 복제본 간의 데이터 불일치 오류를 수정했습니다.</li>
<li>중단된 핫스팟 기록 업데이트 오류를 수정했습니다.</li>
<li>동시 복제 중에 Seconds_Behind_Master 값에 예외가 있는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180915</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>저장 엔진을 MEMORY에서 InnoDB로 자동 변경 지원: 전역 변수 cdb_convert_memory_to_innodb가 ON이면 테이블이 생성되거나 수정될 때 엔진이 MEMORY에서 InnoDB로 변경됩니다.</li>
<li>리소스 충돌을 줄이기 위해 유휴 트랜잭션 자동 kill을 지원합니다.이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
</ul>

<li>bug 수정</li><ul>
<li>REPLAY LOG RECORD로 인한 crash를 수정했습니다.</li>
<li>decimal 정확성 문제로 인해 원본과 복제본 간의 시간 데이터 불일치 오류를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180130</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>스레드 풀을 지원합니다. 이 기능을 신청하려면 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">티켓 제출</a>하십시오.</li>
<li>복제본(slave) 노드에 대해 동적으로 수정되는 복제 필터링 규칙을 지원합니다.</li>
</ul>

<li>성능 최적화</li><ul>
<li>drop table로 인한 성능 변동이 감소했습니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>인증 암호 문자열로 인해 데이터베이스 crash 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180122</td>
<td>
<ul><li>새로운 기능</li><ul>
<li>SQL 감사를 지원합니다.</li>
</ul>

<li>bug 수정</li><ul>
<li>정수 오버플로 오류를 수정했습니다.</li>
<li>전체 텍스트 인덱스를 사용하는 쿼리로 인해 발생하는 오류를 수정했습니다.</li>
<li>복제 중에 복제본(slave)이 crash하는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20170830</td>
<td>
<ul><li>bug 수정</li><ul>
<li>비동기 모드에서 binlog 속도 제한이 무효화되는 문제를 수정했습니다.</li>
<li>buffer_pool 상태에 예외가 있는 문제를 수정했습니다.</li>
<li>SEQUENCE와 암시적 기본 키가 충돌하는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20170228</td>
<td>
<ul><li>bug 수정</li><ul>
<li>drop table의 문자 인코딩 bug를 수정했습니다.</li>
<li>데이터베이스 또는 테이블의 소수점과 같은 특수 기호가 replicate-wild-do-table 문으로 제대로 필터링되지 않는 문제를 수정했습니다.</li>
<li>복제본에 rotate 이벤트가 발생한 후 SQL 스레드가 너무 일찍 종료되는 문제를 수정했습니다.</li>
</ul>
</td>
</tr>

<tr>	
<td>20161130</td>
<td>
<ul><li>성능 최적화</li><ul>
<li>lock_log 잠금을 분할하여 잠금 로그에 사용되는 시간을 줄이고 동시성 성능을 향상시킵니다.</li>
<li>응답 시간을 개선하기 위해 소스의 ACK 스레드를 분리했습니다.</li>
<li>팬텀 읽기를 방지하기 위해 ACK를 기다리는 동안 사용자 스레드가 kill되는 것을 금지했습니다.</li>
<li>sync_binlog != 1일 때 불필요한 lock_sync 잠금을 수정했습니다.</li>
</ul>
</td>
</tr>

</tbody></table>
:::
</dx-tabs>
