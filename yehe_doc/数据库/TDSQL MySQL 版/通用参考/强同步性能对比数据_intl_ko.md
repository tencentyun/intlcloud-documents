
본문은 참고용으로 TDSQL for MySQL 샤드와 오픈 소스 MySQL(최적화되지 않음) 간의 성능 비교를 제공합니다.

## 비교를 위한 테스트 환경
**하드웨어:** 24core CPU, 128GB 메모리, 1.8TB SSD
**네트워크 환경:** 평균 네트워크 대기 시간이 0.80ms인 LAN
**운영 체제:** CentOS 7.0
**데이터 볼륨:** 10개 테이블. 각각에는 약 5.2GB의 2180000개의 데이터 행이 있습니다. innodb buffer: 30GB
**오픈 소스 버전:** MySQL 5.7.17 커뮤니티 버전(최적화되지 않음, 반동기화 활성화됨)
**TDSQL MySQL 샤드 버전:** 다음 매개변수가 있는 MySQL 5.7(강력한 동기화 활성화, 스레드 풀은 기본적으로 활성화됨):
- thread\_pool\_max\_threads=2000
- thread\_pool\_oversubscribe = 10
- thread\_pool\_stall\_limit = 50
- thread\_handling = 2

## 자세한 비교 데이터
#### 1. 데이터 초기화 매개변수
```
create database caccts ;
./sysbench --num-threads=500 --test=./tests/db/oltp.lua.bak --oltp-table-size=2180000 --oltp-tables-count=10 --oltp-point-selects=1 --oltp-simple-ranges=0 --oltp-sum-ranges=0 --oltp-order-ranges=0 --oltp-index-updates=1 --oltp-non-index-updates=0 --report-interval=1 --mysql-user=xxxxxx --mysql-password=xxxxxx --mysql-host=xxxxxx --mysql-db=caccts --max-time=360000 --max-requests=2000000000 prepare

```

#### 2. 비 인덱스 업데이트(update)
```
./sysbench --num-threads=500 --test=./tests/db/update\_non\_index.lua --oltp-table-size=2180000 --oltp-tables-count=10 --percentile=99 --report-interval=1 --mysql-host=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=caccts --max-time=360000 --max-requests=2000000000 --mysql-port=3306 run

```

#### 3. 읽기 전용(select)
```
./sysbench --num-threads=500 --test=./tests/db/select.lua --oltp-table-size=2180000 --oltp-tables-count=10 --percentile=99 --report-interval=1 --mysql-host=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=caccts --max-time=360000 -- max-requests=2000000000 --mysql-port=3306 run

```

#### 4. 하이브리드 테스트
```
./sysbench\_orig --num-threads=500 --test=./tests/db/oltp\_new.lua --oltp-read-only=off --oltp-table-size=2180000 --oltp-tables-count=10 --oltp-point-selects=1 --oltp-simple-ranges=0 --oltp-sum-ranges=0 --oltp-order-ranges=0 --oltp-distinct-ranges=0 --oltp-index-updates=1 --oltp-non-index-updates=0 --percentile=99 --report-interval=1 --mysql-host=xxxx -- mysql-user=xxx --mysql-password=xxx --mysql-db=caccts --max-time=360000 --max-requests=2000000000 --mysql-port=3306 run

```

### 읽기 요청(read) 테스트 결과

| 동시성 | 버전 | qps | 평균 응답 시간(ms) | 99% 응답 시간(ms) |
| --- | --- | --- | --- | --- |
| 50 | 오픈 소스 MySQL | 304585 | 0.16 | 0.26 |
| 50 | TDSQL for MySQL | 330695 | 0.15 | 0.24 |
| 100 | 오픈 소스 MySQL | 407443 | 0.24 | 0.48 |
| 100 | TDSQL for MySQL | 484640 | 0.2 | 0.72 |
| 200 | 오픈 소스 MySQL | 433401 | 0.57 | 1 |
| 200| TDSQL for MySQL | 498215 | 0.55 | 1.22 |
| 500 | 오픈 소스 MySQL | 428542 | 1.16 | 2.42 |
| 500 | TDSQL for MySQL | 494874 | 1.01 | 2.61 |
| 1000 | 오픈 소스 MySQL | 412775 | 2.4 | 6.3 |
| 1000 | TDSQL for MySQL | 478393 | 2.08 | 4.21 |

### 쓰기 요청(write)테스트 결과

| 동시성 | 버전 | qps | 평균 응답 시간(ms) | 99% 응답 시간(ms) |
| --- | --- | --- | --- | --- |
| 50 | 오픈 소스 MySQL | 14816 | 3.37 | 4.82 |
| 50 | TDSQL for MySQL | 28925 | 1.73 | 2.55 |
| 100 | 오픈 소스 MySQL | 25046 | 3.99 | 6.91 |
| 100 | TDSQL for MySQL | 43466 | 2.3 | 4 |
| 200 | 오픈 소스 MySQL | 32690 | 6.12 | 10.86 |
| 200 | TDSQL for MySQL | 54045 | 3.7 | 7.27 |
| 500 | 오픈 소스 MySQL | 37192 | 13.44 | 21.1 |
| 500 | TDSQL for MySQL | 70370 | 7.25 | 15.52 |
| 1000 | 오픈 소스 MySQL | 35447 | 28.2 | 40.47 |
| 1000 | TDSQL for MySQL | 69890 | 14.35 | 30.73 |

### 하이브리드 시나리오(OLTP) 테스트 결과

| 동시성 | 버전 | qps | 평균 응답 시간(ms) | 99% 응답 시간(ms) |
| --- | --- | --- | --- | --- |
| 50 | 오픈 소스 MySQL | 63806 | 4.7 | 7.13 |
| 50 | TDSQL for MySQL | 162883 | 1.84 | 3.45 |
| 100 | 오픈 소스 MySQL | 102516 | 5.85 | 11.4 |
| 100 | TDSQL for MySQL | 173974 | 3.58 | 6.64 |
| 200 | 오픈 소스 MySQL | 124550 | 9.64 | 18.92 |
| 200 | TDSQL for MySQL | 208128 | 5.76 | 11.9 |
| 500 | 오픈 소스 MySQL | 125386 | 23.93 | 39.68 |
| 500 | TDSQL for MySQL | 232543 | 13.58 | 27.81 |
| 1000 | 오픈 소스 MySQL | 121765 | 49.29 | 80.71 |
| 1000 | TDSQL for MySQL | 226130 | 27.76 | 54.78 |

