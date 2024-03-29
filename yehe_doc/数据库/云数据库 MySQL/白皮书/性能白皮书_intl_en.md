## Test Tool
Sysbench 0.5 is the tool used to test the database benchmark performance.

Tool configuration:
The OTLP script that comes with Sysbench was modified. Specifically, the read/write ratio was changed to 1:1 and controlled by the testing command parameters `oltp_point_selects` and `oltp_index_updates`. In this document, all test cases involve four SELECT operations and one UPDATE operation with the read/write ratio at 4:1.

#### Tool installation
Run the following code to install Sysbench 0.5:
```
git clone https://github.com/akopytov/sysbench.git
git checkout 0.5
yum -y install make automake libtool pkgconfig libaio-devel
yum -y install mariadb-devel
./autogen.sh
./configure
make -j
make install
```
>?The installation directions above apply to performance stress testing on a CentOS CVM instance. For directions on installing the tool on other operating systems, please see [the official Sysbench documentation](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS).

## Test Environment

| Type | Description |
|--|--|
| Physical machine | A single machine can support two-node database instances with up to 488 GB memory and 6 TB disk |
| Instance specification | Specifications which are commonly available (please see the [test cases](#cscs) below) |
| Client configuration | 4-core CPU and 8 GB memory |
| Number of clients | 1-6 (more clients need to be added as the configuration is upgraded) |
| Network environment | Data center with 10-Gigabit connection and a network latency below 0.05 ms |
| Environment load | Load on the machine where MySQL is installed is above 70% (for non-exclusive instances) |

- Note on client specification: high-spec client machines are used so as to ensure that the database instance performance can be measured through stress testing on a single client. For low-spec clients, it is recommended to use multiple clients for concurrent stress testing and aggregate the results.
- Note on network latency: in the testing environment, it should be ensured that clients and database instances are in the same availability zone so as to prevent the testing result from being affected by network factors.

## Test Method
### 1. Structure of testing database tables
```
CREATE TABLE `sbtest1` ( 
`id` int(10) unsigned NOT NULL AUTO_INCREMENT, 
`k` int(10) unsigned NOT NULL DEFAULT '0', 
`c` char(120) NOT NULL DEFAULT '', 
`pad` char(60) NOT NULL DEFAULT '',
 PRIMARY KEY (`id`), KEY `k_1` (`k`) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 2. Format of testing data rows
```
id: 1
k: 20106885
c: 08566691963-88624912351-16662227201-46648573979-64646226163-77505759394-75470094713-41097360717-15161106334-50535565977
pad: 63188288836-92351140030-06390587585-66802097351-4928296184
```

### 3. Data preparations
```
sysbench --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --mysql-table-engine=innodb --test=tests/db/oltp.lua --oltp_tables_count=20 --oltp-table-size=10000000  --rand-init=on prepare
```

Descriptions of data preparation parameters:
- `--test=tests/db/oltp.lua` indicates to implement the OLTP test by calling the `tests/db/oltp.lua` script.
- `--oltp_tables_count=20` indicates that the number of tables for testing is 20.
- `--oltp-table-size=10000000` indicates that each testing table is populated with 10 million rows of data.
- `--rand-init=on` indicates that each testing table is populated with random data.
  

### 4. Command for stress testing
```
sysbench --mysql-host=xxxx --mysql-port=xxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua --oltp_tables_count=xx --oltp-table-size=xxxx --num-threads=xxx --oltp-read-only=off --rand-type=special --max-time=600 --max-requests=0 --percentile=99 --oltp-point-selects=4 run
```

Descriptions of stress testing parameters:
- `--test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua` indicates to implement the OLTP test by calling the `/root/sysbench_for_z3/sysbench/tests/db/oltp.lua` script.
- `--oltp_tables_count=20` indicates that the number of tables for testing is 20.
- `--oltp-table-size=10000000` indicates that each testing table is populated with 10 million rows of data.
- `--num-threads=128` indicates that the concurrent connections of clients for testing is 128.
- `--oltp-read-only=off` indicates that the read-only testing model is disabled and the hybrid read/write model is used.
- `--rand-type=special` indicates that the random model is specific.
- `--max-time=1800` indicates the execution time of this test.
- `--max-requests=0` indicates that no limit is imposed on the total number of requests and the test is executed according to `max-time`.
- `--percentile=99` indicates the sampling rate. Here, 99 means discarding 1% long requests of all the requests and taking the maximum value among the remaining 99% requests. The default value is 95%.
- `--oltp-point-selects=4` indicates that the number of SELECT operations in the SQL testing command in the OLTP script is 4. The default value is 1.

### 5. Scenario model
All test cases in this document adopt the `lua` script of Sysbench which was modified to run four SELECT operations and one UPDATE operation (index column) with the read/write ratio at 4:1.
For the maximum configuration, the parameter tuning model is added to the data scenario. For the test results, please see [Test Results](#document_test_result) below.


<span id="cscs"></span>
## Test Parameters

| Instance Specification | Storage Capacity | Number of Tables | Number of Rows | Data Set Size | Concurrence | Execution Time (Minutes) |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1-core, 1 GB|200 GB|4|20 million |19 GB|128|30|
|1-core, 2 GB|200 GB|4|40 million |38 GB|128|30|
|2-core, 4 GB|200 GB|8|40 million|76 GB|128|30|
|4-core, 8 GB|200 GB|15|40 million |142 GB|128|30|
|4-core, 16 GB|400 GB|25|40 million|238 GB|128|30|
|8-core, 32 GB|700 GB|25|40 million|238 GB|128|30|
|16-core, 64GB|1 TB|40|40 million|378 GB|256|30|
|16-core, 96 GB|1.5 TB|40|40 million|378 GB|128|30|
|16-core, 128 GB|2 TB|40|40 million|378 GB|128|30|
|24-core, 244 GB|3 TB|60|40 million|567 GB|128|30|
|48-core, 488 GB|6 TB|60|40 million|567 GB|128|30|
|48-core, 488 GB (tuned)|6 TB|60|10 million|140 GB|128|30|

<span id="document_test_result"></span>
## Test Results

| Instance Specification | Storage Capacity | Data Set | Number of Clients | Single-client Concurrence | QPS | TPS |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1-core, 1 GB|200 GB|19 GB|1|128|1,757|97|
|1-core, 2 GB|200 GB|38 GB|1|128|3,016|167|
|2-core, 4 GB|200 GB|76 GB|1|128|4,082|816|
|4-core, 8 GB|200 GB|142 GB|1|128|6,551|1,310|
|4-core, 16 GB|400 GB|238 GB|1|128|11,098|2,219|
|8-core, 32 GB|700 GB|238 GB|2|128|20,484|3,768|
|16-core, 64 GB|1 TB|378 GB|2|128|36,395|7,279|
|16-core, 96 GB|1.5 TB|378 GB|3|128|56,464|11,292|
|16-core, 128 GB|2 TB|378 GB|3|128|81,752|16,350|
|24-core, 244 GB|3 TB|567 GB|4|128|98,528|19,705|
|48-core, 488 GB|6 TB|567 GB|6|128|142,246|28,449|
|48-core, 488 GB (tuned) |6 TB|140 GB|6|128|245,509|46,304|
