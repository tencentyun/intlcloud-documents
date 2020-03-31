## 1. Testing Tool
sysbench v0.5 is the tool used to test the database benchmark performance.
Modifications to the tool:
The OTLP script that comes with sysbench was modified. Specifically, the read/write ratio was changed to 1:1 and controlled by the testing command parameters `oltp_point_selects` and `oltp_index_updates`. In this document, all test cases involve 4 Select operations and 1 Update operation with the read/write ratio at 4:1.

## 2. Testing Environment

| Type | Description |
|:--:|:--:|
| Physical machine | High-IO edition where a single machine can support database instances with up to 488 GB memory and 6 TB disk |
| Instance specification | Currently purchasable mainstream specification (please see the test cases below) |
| Client configuration | 4-core CPU and 8 GB memory |
| Number of clients | 1–6 (more clients need to be added as the configuration is upgraded) |
| Network environment | Data center with 10-Gigabit connection and a network latency below 0.05 ms |
| Environment load | Load on the machine where MySQL is installed is above 70% (for non-exclusive instances) |

* Note on client specification: high-spec client machines are used so as to ensure that the database instance performance can be measured through stress testing on a single client. For low-spec clients, it is recommended to use multiple clients for concurrent stress testing and aggregate the results.
* Note on network latency: it should be ensured that clients and database instances are in the same AZ so as to prevent the testing result from being affected by network factors.

## 3. Testing Method
### 3.1. Structure of testing tables

```
CREATE TABLE `sbtest1` ( 
`id` int(10) unsigned NOT NULL AUTO_INCREMENT, 
`k` int(10) unsigned NOT NULL DEFAULT '0', 
`c` char(120) NOT NULL DEFAULT '', 
`pad` char(60) NOT NULL DEFAULT '',
 PRIMARY KEY (`id`), KEY `k_1` (`k`) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 3.2. Format of testing data rows

```
id: 1
k: 20106885
c: 08566691963-88624912351-16662227201-46648573979-64646226163-77505759394-75470094713-41097360717-15161106334-50535565977
pad: 63188288836-92351140030-06390587585-66802097351-4928296184
```


### 3.3. Data preparation

```
/root//sysbench/sysbench --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --mysql-table-engine=innodb --test=tests/db/oltp.lua --oltp_tables_count=20 --oltp-table-size=10000000  --rand-init=on prepare
```

Description of data preparation parameters:
`--test=tests/db/oltp.lua` indicates to implement the OLTP test by calling the tests/db/oltp.lua script.
   
`--oltp_tables_count=20` indicates that the number of tables for testing is 20.
   
`--oltp-table-size=10000000` indicates that each testing table is populated with 10 million rows of data.
   
`--rand-init=on` indicates that each testing table is populated with random data.
   

### 3.4. Commands for performance stress testing
```
/root//sysbench/sysbench --mysql-host=xxxx --mysql-port=xxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua --oltp_tables_count=xx --oltp-table-size=xxxx --num-threads=xxx --oltp-read-only=off --rand-type=special --max-time=600 --max-requests=0 --percentile=99 --oltp-point-selects=4 run
```

Description of performance stress testing parameters:
 
--test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua
 
`--oltp_tables_count=20` indicates that the number of tables for testing is 20.
 
`--oltp-table-size=10000000` indicates that each testing table is populated with 10 million rows of data.
 
`--num-threads=128` indicates that the concurrent connections of clients for testing is 128.
 
`--oltp-read-only=off` indicates that the read-only testing model is disabled and the hybrid read/write model is used.
 
`--rand-type=special` indicates that the random model is specific.
 
`--max-time=1800` indicates the execution time of this test.
 
`--max-requests=0` indicates that no limit is imposed on the total number of requests and the test is executed according to `max-time`.
 
 `--percentile=99` indicates the sampling rate. Here, 99 means discarding 1% long requests of all the requests and taking the maximum value among the remaining 99% requests. The default value is 95%.
 
 `--oltp-point-selects=4` indicates that the number of Select operations in the SQL testing command in the OLTP script is 4. The default value is 1.

### 3.5. Scenario model

All test cases in this document adopt the scenario script `our_oltp.lua` which is modified to run four `Select` operations and one `Update` operation (index column) with the read/write ratio at 4:1.

For the maximum configuration, the parameter tuning model is added to the data scenario. For the test results, please see "Test Results" below.

## 4. Testing Parameters
| Memory | Storage Capacity | Number of Tables | Number of Rows | Data Set Size | Concurrence | Execution Time (Min) |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| 4 GB | 200 GB | 8 | 40 million | 76 GB | 128 | 30 |
| 8 GB | 200 GB | 15 | 40 million | 142 GB | 128 | 30 |
| 16 GB | 400 GB | 25 | 40 million | 238 GB | 128 | 30 |
| 32 GB | 700 GB | 25 | 40 million | 238 GB | 128 | 30 |
| 64 GB | 1 TB | 40 | 40 million | 378 GB | 256 | 30 |
| 96 GB | 1.5 TB | 40 | 40 million | 378 GB | 128 | 30 |
| 128 GB | 2 TB | 40 | 40 million | 378 GB | 128 | 30 |
| 244 GB | 3 TB | 60 | 40 million | 567 GB | 128 | 30 |
| 488 GB | 6 TB | 60 | 40 million | 567 GB | 128 | 30 |
| 488 GB (tuned) | 6 TB | 60 | 10 million | 140 GB | 128 | 30 |

## 5. Test Results
| Memory | Storage Capacity | Data Set | Number of Clients | Single-client Concurrence | QPS | TPS |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| 4 GB | 200 GB | 76 GB | 1 | 128 | 4,082 | 816 |
| 8 GB | 200 GB | 142 GB | 1 | 128 | 6,551 | 1,310 |
| 16 GB | 400 GB | 238 GB | 1 | 128 | 11,098 | 2,219 |
| 32 GB | 700 GB | 238 GB | 2 | 128 | 20,484 | 3,768 |
| 64 GB | 1 TB | 378 GB | 2 | 128 | 36,395 | 7,279 |
| 96 GB | 1.5 TB | 378 GB | 3 | 128 | 56,465 | 11,292 |
| 128 GB | 2 TB | 378 GB | 3 | 128 | 82,007 | 16,120 |
| 244 GB | 3 TB| 567 GB | 4 | 128 | 99,868 | 19,505 |
| 488 GB | 6 TB | 567 GB | 6 | 128 | 141,136 | 28,449 |
| 488 GB (tuned) | 6 TB | 140 GB | 6 | 128 | 245,408 | 47,201 |
