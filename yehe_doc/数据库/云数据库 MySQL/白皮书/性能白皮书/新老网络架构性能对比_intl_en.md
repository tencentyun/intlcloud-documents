TencentDB for MySQL has upgraded the network architecture of database instances for a higher performance and lower latency. This document describes the performance tests on the old and new versions.
>?
>- **Starting from November 9, 2022, the new network architecture has been applied to newly purchased instances to deliver lower latency and higher performance.
>- **On January 21, 2023, all existing database instances have been switched to the new network architecture**.
>- Single-node instances of cloud disk edition are already in the optimal network architecture, so their details page does not indicate whether the network architecture is new.
>- The new network architecture cannot be used in the classic network. To use it, switch to VPC as instructed in [Network Switch](https://intl.cloud.tencent.com/document/product/236/31915) and wait for the network architecture to upgrade.
>- For more information, see [Network Architecture Upgrade](https://www.tencentcloud.com/document/product/236/51945).

## Test environment
- Region/AZ: Beijing - Beijing Zone 6.
- Client specification: S5.2XLARGE16 (8 CPU cores and 16 GB memory).
- Client OS: TencentOS Server 3.2.
- Network: Both the CVM and TencentDB for MySQL instances are in the same VPC subnet.
- Storage type: Local SSD disk
- Instance specification: General (4 CPU cores and 16 GB memory).
- Parameter template: High-performance template
- Replication method: Async replication

## Test tool
SysBench is a modular, cross-platform, and multi-threaded benchmark tool for evaluating OS parameters that are important for a system running a database under intensive load. The idea of this benchmark suite is to quickly get an impression about system performance without setting up complex database benchmarks or even without installing a database at all. This stress test uses SysBench 1.0.20.

## Test scenario
This stress test involves write-only, read-only, and read-write scenarios, each with 2–3,000 threads tested. The QPS is used as the performance metric.

## Test method
**Step 1. Prepare the data**
Run the following command:
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300 --threads={2~3000} oltp_read_write prepare
```

**Step 2. Run the workload**
Run the workload in write-only, read-only, and read-write scenarios. Make sure that the configuration is correct.
- OLTP write-only scenario
Run the following command:
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300  --threads={2~3000} --percentile=95 --report-interval=1 oltp_write_only
run
```
- OLTP read-only scenario
Run the following command:
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300 --threads={2~3000} --percentile=95 --skip-trx=1 --report-interval=1
oltp_read_only
run
```
- OLTP read-write scenario
Run the following command:
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300  --threads={2~3000} --percentile=95 --report-interval=1 oltp_read_write
run
```

**Step 3. Clear the data**
Run the following command to clear the data after the test is executed:
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX
--mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_write cleanup
```

## Test metric
The test metric is queries per second (QPS).

## Test result
**Test result in the write-only scenario**
In the write-only scenario, the new architecture of TencentDB for MySQL always outperforms the old architecture as the thread quantity increases, with the QPS peaking at 256 threads and being 20% higher than the old architecture's at 512 threads.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EXhD388_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

**Test result in the read-only scenario**
In the read-only scenario, the new architecture of TencentDB for MySQL sees a great linear QPS rise as the thread quantity increases from a small number, with the QPS 22% being higher than the old architecture's at 16 threads and going up steadily at 64 threads or more.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/p62d341_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-3.png)

**Test result in the read-write scenario**
In the read-write scenario, the new architecture of TencentDB for MySQL sees a great QPS rise as the thread quantity increases from a small number, with the QPS hitting the peak (18% higher than the old architecture's) at 512 threads and falling steadily after that.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/p62d341_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-3.png)

## Conclusion
>? The above performance test results are for reference only.
>
The above scenario tests show that the new network architecture of TencentDB for MySQL greatly outperforms the old architecture. In the range of 2–3,000 threads, the QPS is improved by 20% on average.
