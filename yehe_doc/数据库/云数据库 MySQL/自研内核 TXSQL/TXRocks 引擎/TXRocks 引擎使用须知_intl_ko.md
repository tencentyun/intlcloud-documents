TXRocks는 RocksDB를 기반으로 Tencent의 TXSQL 팀에서 개발한 트랜잭션 스토리지 엔진입니다. 더 많은 저장 공간을 절약하고 쓰기 증폭이 더 낮습니다.

## 제품 소개
TXRocks 트랜잭션 스토리지 엔진은 RocksDB의 LSM Tree 스토리지 구조를 활용하여 InnoDB의 half-full 페이지 및 조각으로 인해 발생하는 낭비를 줄일 뿐만 아니라 컴팩트 스토리지 형식을 사용합니다. 따라서 InnoDB에 필적하는 성능을 가지지만 절반 또는 그보다 작은 저장 공간만 있으면 됩니다. 데이터 볼륨이 크고 트랜잭션 읽기/쓰기 성능에 대한 요구 사항이 높은 비즈니스에 더 적합합니다.

## 전제 조건
데이터베이스 버전은 2노드 아키텍처, MySQL 5.7 또는 8.0이어야 합니다.

## TencentDB for MySQL 인스턴스 구매(RocksDB 엔진 포함)
TencentDB for MySQL [구매 페이지](https://buy.Intl.cloud.tencent.com/cdb)에서 인스턴스를 구매할 때 RocksDB를 엔진으로 선택할 수 있습니다. 기타 매개변수에 대한 자세한 내용은 [MySQL 인스턴스 생성](https://intl.cloud.tencent.com/document/product/236/37785)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/4b309a61ecac3520e27160da7143c224.png)

>?RocksDB는 효율적인 쓰기와 높은 압축을 갖춘 key-value 스토리지 엔진입니다. 현재 MySQL 5.7 및 8.0만 RocksDB 엔진을 사용할 수 있습니다.

## RocksDB 테이블 생성
인스턴스 생성 시 RocksDB가 기본 엔진으로 선택되면 테이블 생성에 사용되는 기본 엔진이 됩니다. 다음 명령을 실행하여 기본 엔진을 볼 수 있습니다.
```
show variables like '%default_storage_engine%';
```
![](https://qcloudimg.tencent-cloud.cn/raw/3bb1550d5995cece7cec2712ad62c5d0.png)
기본 엔진이 RocksDB인 경우 테이블 생성 명령에서 스토리지 엔진을 지정할 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f4cb2efa27e236fb26a78971a8725cbd.png)
테이블이 생성된 후 해당 데이터는 RocksDB에 저장되며 InnoDB와 동일한 방식으로 사용할 수 있습니다.

## 엔진 기능 제한
TXRocks에는 아래와 같이 엔진 기능에 대한 특정 제한이 있습니다.
<table>
<thead><tr><th>카테고리</th><th>기능</th><th>TXRocks 제한</th></tr></thead>
<tbody>
<tr>
<td>DDL</td><td>Online DDL</td><td>미지원, 예를 들어 ALTER TABLE ... ALOGRITHM=INSTANT는 미지원, Partition 관리 작업에는 COPY 알고리즘만 지원</td></tr>
<tr>
<td rowspan="5">SQL</td>
<td>외래 키</td><td>미지원(Foreign Key)</td></tr>
<td>파티션된 테이블</td><td>미지원(Partition)</td></tr>
<td>생성된 열</td><td>미지원(Generated Columns)</td></tr>
<td>명시적 Default 표현식</td><td>미지원, 예를 들어 CREATE TABLE t1（c1 FLOAT DEFAULT(RAND())）ENGINE=ROCKSDB;는 실패하고, ‘Specited storage engine’ is not supported for default value expressions. 라는 오류 보고</td></tr>
<td>암호화된 테이블</td><td>미지원</td></tr>
<tr> 
<td rowspan="3">인덱스</td>
<td>공간 인덱스</td><td>GEOMETRY 및 POINT와 같은 공간 인덱스(Spatial Index) 및 공간 데이터 유형 미지원</td></tr>
<tr> 
<td>전체 텍스트 인덱스</td><td>미지원(Fulltext Index)</td></tr>
<td>다중값 인덱스</td><td>미지원(multi-valued index)</td></tr>
<tr>
<td rowspan="4">복제</td>
<td>그룹 복제</td><td>미지원(Group Replication)</td></tr>
<td>binlog 형식</td><td>ROW 형식만 지원, stmt 및 mixed 형식은 미지원</td></tr>
<td>클론 플러그 인</td><td>미지원(Clone Plugin)</td></tr>
<td>전송 가능한 테이블 스페이스</td><td>미지원(Transportable Tablespace)</td></tr>
<tr>
<td rowspan="5">트랜잭션 및 잠금</td>
<td>LOCK NOWAIT 및 SKIP LOCKED</td><td>미지원(LOCK NOWAIT 및 SKIP LOCKED)</td></tr>
<td>갭 락</td><td>미지원(Gap Lock)</td></tr>
<td>Savepoint</td><td>미지원(Savepoint)</td></tr>
<td>부분적 LOB 필드 업데이트</td><td>미지원</td></tr>
<td>XA 트랜잭션</td><td>권장하지 않음</td></tr>
</tbody></table>	

## 매개변수 설명
>?TencentDB for MySQL 인스턴스 생성 시 RocksDB를 기본 스토리지 엔진으로 선택할 수 있습니다. 아래의 매개변수 설명에 따라 필요에 맞게 매개변수 템플릿을 사용자 정의할 수도 있습니다.

#### MySQL 5.7 매개변수 목록

| 매개변수 | 재시작 필요 | 기본값 | 값 범위/유효 값 | 설명 |
|---------|---------|---------|---------|---------|
| rocksdb_use_direct_io_for_flush_and_compaction | Yes | ON | ON/OFF | compaction 중에 DIO 사용 여부입니다. |
| rocksdb_flush_log_at_trx_commit | No | 1 | 0/1/2 | 디스크에 로그를 기록할 시기를 제어합니다. <br> innodb_flush_log_at_trx_commit과 유사하며 커밋할 때 트랜잭션 동기화 여부를 나타냅니다. <li>0: 커밋할 때 트랜잭션이 동기화되지 않습니다. <li>1: 트랜잭션 커밋될 때 동기화 됩니다. <li>2: 트랜잭션은 1초에 한 번 동기화 됩니다.</li>  |
| rocksdb_lock_wait_timeout | No | 1 | 1-1073741824 | 잠금 대기 초과 시간(초)입니다. |
| rocksdb_deadlock_detect | No | ON | ON/OFF | 교착 상태 감지 활성화 여부입니다. 활성화되면 모든 교착 상태 정보가 mysqld 오류 로그에 기록됩니다. |
| rocksdb_manual_wal_flush | Yes | ON | ON/OFF | WAL 파일의 총 크기가 rocksdb_max_total_wal_size를 초과하면 RocksDB는 가장 오래된 WAL 파일을 삭제할 수 있도록 column 패밀리를 디스크에 강제로 플러시합니다. |

#### MySQL 8.0 매개변수 목록

| 매개변수 | 재시작 필요 | 기본값 | 값 범위/유효한 값 | 설명 |
|---------|---------|---------|---------|---------|
| rocksdb_flush_log_at_trx_commit | No | 1 | 0/1/2 | 디스크에 로그를 기록할 시기를 제어합니다. <br>innodb_flush_log_at_trx_commit과 유사하며 커밋할 때 트랜잭션 동기화 여부를 나타냅니다. <li>0: 커밋할 때 트랜잭션이 동기화되지 않습니다. <li>1: 트랜잭션 커밋될 때 동기화 됩니다. <li>2: 트랜잭션은 1초에 한 번 동기화 됩니다. </li>|
| rocksdb_lock_wait_timeout | No | 1 | 1-1073741824 | 잠금 대기 초과 시간(초)입니다. |
| rocksdb_merge_buf_size | No | 524288(=512K) | 100-18446744073709551615 | 보조 인덱스 생성 중에 사용되는 merge-sort buffer의 크기입니다. |
| rocksdb_merge_combine_read_size | No | 8388608 (=8M) | 524288(=512K)-18446744073709551615 | 보조 인덱스 생성 중 k-way merge가 사용하는 메모리 크기입니다 |
| rocksdb_deadlock_detect | No | ON | ON/OFF | 교착 상태 감지 활성화 여부입니다. |
| rocksdb_manual_wal_flush | Yes | ON | ON/OFF | WAL 파일의 총 크기가 rocksdb_max_total_wal_size를 초과하면 RocksDB는 가장 오래된 WAL 파일을 삭제할 수 있도록 column 패밀리를 디스크에 강제로 플러시합니다. |

## RocksDB 모니터링 지표
RocksDB 모니터링 지표는 다음과 같습니다.

| 지표 | 설명 |
|---------|---------|
| rocksdb_bytes_read | 디스크에서 읽은 데이터 |
| rocksdb_bytes_written | 디스크에 기록된 데이터 |
| rocksdb_block_cache_bytes_read | 블록 읽기 |
| rocksdb_block_cache_bytes_write | 블록 작성 |
| rocksdb_wal_log_capacity | WAL 로그에 기록된 데이터 |

