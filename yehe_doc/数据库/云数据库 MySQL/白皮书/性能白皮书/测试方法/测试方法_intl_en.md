
This document describes the method of TencentDB for MySQL performance test.

## Directions
Use SysBench to test the mixed read/write performance of the TencentDB for MySQL instance.
1. Prepare the data.
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600  oltp_read_write prepare
```
2. Run the workload.
```
sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_read_write run
```
3. Clear the data.
```
sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_write cleanup
```
