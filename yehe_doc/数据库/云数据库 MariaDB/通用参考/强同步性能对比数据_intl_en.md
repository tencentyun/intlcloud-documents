This document provides a comparison on the performance of TencentDB for MariaDB and open-source MySQL (unoptimized) for your reference.

## Testing Environment for Comparison

- **Hardware:** 24-core CPU; 128 GB memory; 1.8 TB SSD
- **Network environment:** LAN with an average network latency of 0.80 ms
- **Operating system:** CentOS 7.0
- **Data volume:** 10 tables. Each of them has 2,180,000 data rows of about 5.2 GB. InnoDB buffer: 30 GB
- **Open-source version:** MySQL 5.6 community edition (unoptimized; **async replication enabled**)
- **TencentDB for MariaDB sharding version:** MariaDB 10.1.10 (optimized kernel with **strong sync replication enabled**; thread pool enabled by default)


## Comparison Results
Based on the results, the strong sync performance of optimized TencentDB for MariaDB is slightly better than MySQL's async performance.

## Detailed Comparison Data

### Test operations
#### 1. Data initialization parameters

```
create database caccts ;
./sysbench --num-threads=500 --test=./tests/db/oltp.lua.bak --oltp-table-size=2180000 --oltp-tables-count=10 --oltp-point-selects=1 --oltp-simple-ranges=0 --oltp-sum-ranges=0 --oltp-order-ranges=0 --oltp-index-updates=1 --oltp-non-index-updates=0 --report-interval=1 --mysql-user=xxxxxx --mysql-password=xxxxxx --mysql-host=xxxxxx --mysql-db=caccts --max-time=360000 --max-requests=2000000000 prepare

```

#### 2. Non-index update (UPDATE)

```
./sysbench --num-threads=500 --test=./tests/db/update\_non\_index.lua --oltp-table-size=2180000 --oltp-tables-count=10 --percentile=99 --report-interval=1 --mysql-host=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=caccts --max-time=360000 --max-requests=2000000000 --mysql-port=3306 run

```

#### 3. Read-only (SELECT)

```
./sysbench --num-threads=500 --test=./tests/db/select.lua --oltp-table-size=2180000 --oltp-tables-count=10 --percentile=99 --report-interval=1 --mysql-host=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=caccts --max-time=360000 -- max-requests=2000000000 --mysql-port=3306 run

```

#### 4. Hybrid test

```
./sysbench\_orig --num-threads=500 --test=./tests/db/oltp\_new.lua --oltp-read-only=off --oltp-table-size=2180000 --oltp-tables-count=10 --oltp-point-selects=1 --oltp-simple-ranges=0 --oltp-sum-ranges=0 --oltp-order-ranges=0 --oltp-distinct-ranges=0 --oltp-index-updates=1 --oltp-non-index-updates=0 --percentile=99 --report-interval=1 --mysql-host=xxxx -- mysql-user=xxx --mysql-password=xxx --mysql-db=caccts --max-time=360000 --max-requests=2000000000 --mysql-port=3306 run

```

### Comparison results
#### 1. Read request (READ)

| Concurrence | Version | QPS | Average Response Time (ms) | 99% Response Time (ms) |
| --- | --- | --- | --- | --- |
| 50 | Open-source MySQL | 306,512 | 0.16 | 0.26 |
| 50 | TencentDB for MariaDB | 310,695 | 0.15 | 0.24 |
| 100 | Open-source MySQL | 417,443 | 0.24 | 0.48 |
| 100 | TencentDB for MariaDB | 454,640 | 0.2 | 0.72 |
| 200 | Open-source MySQL | 423,419 | 0.57 | 1 |
| 200| TencentDB for MariaDB | 488,224 | 0.56 | 1.22 |
| 500 | Open-source MySQL | 438,512 | 1.16 | 2.42 |
| 500 | TencentDB for MariaDB | 490,678 | 1.21 | 2.61 |
| 1000 | Open-source MySQL | 412723 | 2.3 | 6.3 |
| 1000 | TencentDB for MariaDB | 481,342 | 2.1 | 4.21 |

#### 2. Write request (UPDATE)

| Concurrence | Version | QPS | Average Response Time (ms) | 99% Response Time (ms) |
| --- | --- | --- | --- | --- |
| 50 | Open-source MySQL | 24,816 | 2.37 | 2.82 |
| 50 | TencentDB for MariaDB | 28,925 | 2.33 | 2.55 |
| 100 | Open-source MySQL | 43,046 | 2.25 | 3.91 |
| 100 | TencentDB for MariaDB | 43,466 | 2.3 | 4 |
| 200 | Open-source MySQL | 54,690 | 3.92 | 7.86 |
| 200 | TencentDB for MariaDB | 54,045 | 3.7 | 7.27 |
| 500 | Open-source MySQL | 70,192 | 7.44 | 14.1 |
| 500 | TencentDB for MariaDB | 70,370 | 7.25 | 15.52 |
| 1000 | Open-source MySQL | 68,447 | 15.2 | 29.47 |
| 1000 | TencentDB for MariaDB | 69,890 | 14.35 | 30.73 |

#### 3. Hybrid scenario (OLTP test)

| Concurrence | Version | QPS | Average Response Time (ms) | 99% Response Time (ms) |
| --- | --- | --- | --- | --- |
| 50 | Open-source MySQL | 154,806 | 2.7 | 4.13 |
| 50 | TencentDB for MariaDB | 162,883 | 1.84 | 3.45 |
| 100 | Open-source MySQL | 162,696 | 3.85 | 7.4 |
| 100 | TencentDB for MariaDB | 173,974 | 3.58 | 6.64 |
| 200 | Open-source MySQL | 204,550 | 5.64 | 12.92 |
| 200 | TencentDB for MariaDB | 208,128 | 5.76 | 11.9 |
| 500 | Open-source MySQL | 235,386 | 13.93 | 28.58 |
| 500 | TencentDB for MariaDB | 232,543 | 13.58 | 27.23 |
| 1000 | Open-source MySQL | 201,765 | 28.29 | 60.72 |
| 1000 | TencentDB for MariaDB | 226,130 | 27.76 | 54.38 |



