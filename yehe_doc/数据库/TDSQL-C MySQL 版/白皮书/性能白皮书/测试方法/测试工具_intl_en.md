
This document describes how to install SysBench, a performance testing tool for TDSQL-C for MySQL, in a CVM instance.

## SysBench overview
SysBench is a modular, cross-platform, and multi-threaded benchmark tool for evaluating OS parameters that are important for a system running a database under intensive load. The idea of this benchmark suite is to quickly get an impression about system performance without setting up complex database benchmarks or even without installing a database at all.

## SysBench parameter description
| Parameter | Description | 
|---------|---------|
| db-driver | Database engine  | 
| mysql-host | TDSQL-C for MySQL server host  |
| mysql-port | TDSQL-C for MySQL server port  |
| mysql-user | TDSQL-C for MySQL account |
| mysql-password | TDSQL-C for MySQL password |
| mysql-db | 	TDSQL-C for MySQL database name |
| table_size| Test table size  |
|tables | Number of test tables |
| events | Number of test requests |
| time | Test time |
| threads | Number of test threads |
| percentile | The percentile range to be counted, which is 95% by default, i.e., the execution times of requests in 95% of the cases |
| report-interval | Interval for outputting a test progress report in seconds. 0 indicates to output only the final result but not the test progress report |
| skip-trx | Whether to skip transactions<br>1: Yes<br>0: No |

## Installation method
This stress test uses SysBench 1.0.20 (using bundled LuaJIT 2.1.0-beta2). For more information, see [here](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS).
>!One client offers a concurrency of 1,000. One more client is added after the concurrency exceeds 1,000, and so on.

1. Run the following command to install SysBench in a CVM instance:
```
yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql
git clone https://github.com/akopytov/sysbench.git
##Download SysBench from GitHub
cd sysbench
##Open the SysBench directory
git checkout 1.0.20
##Switch to SysBench 1.0.20
./autogen.sh
##Run `autogen.sh`
./configure --prefix=/usr --mandir=/usr/share/man
make
##Compile
make install
```
2. Run the following command to configure the client, so that the kernel can use all CPU cores to process data packets and reduce context switches within each CPU core.
```
sudo sh -c 'for x in /sys/class/net/eth0/queues/rx-*; do echo ffffffff>$x/rps_cpus; done'
sudo sh -c "echo 32768 > /proc/sys/net/core/rps_sock_flow_entries"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-1/rps_flow_cnt"
```
>?`ffffffff` indicates that 32 CPU cores are used (one `f` represents four CPU cores).


