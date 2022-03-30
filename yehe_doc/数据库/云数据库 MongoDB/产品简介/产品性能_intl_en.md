This document describes how to perform standard performance testing on TencentDB for MongoDB instances. The result data is for your reference only.

## Test Environment
- Test date: August 2020.
- Client specification: The client is installed in an 8-core 32 GB CVM instance. Tests show that if the TencentDB for MongoDB instance has a low specification, the CPU utilization of its replica instance can reach 100% under the test pressure of an 8-core 32 GB CVM instance. In this case, one CVM instance achieves even better test results than multiple CVM instances. However, if the CPU utilization can't reach 100% when only one CVM instance is used, four CVM instances can be used to share the concurrent threads.
- Test object: TencentDB for MongoDB 4.0 replica set instance.

## Test Tool
[YCSB download address](https://github.com/brianfrankcooper/YCSB)

## Test Scenario
Prepare about 10 GB of data. Then, run 100 and 200 concurrent threads and use YCSB to test the throughput (ops/sec), read average latency (RAL in μs), and write average latency (WAL in μs) of instances with different specifications under the pressure of 50% read requests and 50% update requests as well as 95% read requests and 5% update requests.

### Latency
The average latency from the CVM instance to the TencentDB for MongoDB instance is 0.35 ms.
Latency: Minimum = 0.30 ms; maximum = 0.44 ms; average = 0.35 ms

### Relevant commands
1. Prepare data (about 10 GB)

```
nohup ./ycsb-0.15.0/bin/ycsb load mongodb -s -P workloads/workloada
-p mongodb.url=mongodb://mongouser:password@10.xx.xx.30:27017,10.xx.xx.28:27017,10.xx.xx.5:27017/admin?w=0 -p table=test -threads 300 -p recordcount=10000000>loadlog.txt &
```

2. Test with 50% read requests and 50% update requests

```
nohup ./ycsb-0.15.0/bin/ycsb run mongodb -s -P workloads/workloada -p mongodb.url=mongodb://mongouser: password @10.xx.xx.30:27017,10.xx.xx.28:27017,10.xx.xx.5:27017/admin?w=0 -p table=test -p recordcount=10000000 -p readproportion=0.5 -p updateproportion=0.5 -p insertproportion=0 -p operationcount=100000 -threads 100 >runlog.txt &
```

3. Test with 95% read requests and 5% update requests

```
nohup ./ycsb-0.15.0/bin/ycsb run mongodb -s -P workloads/workloada -p mongodb.url=mongodb://mongouser: password @10.xx.xx.30:27017,10.xx.xx.28:27017,10.xx.xx.5:27017/admin?w=0 -p table=test -p recordcount=10000000 -p readproportion=0.95 -p updateproportion=0.05 -p insertproportion=0 -p operationcount=100000 -threads 100 >runlog.txt &
```

>?
>- You need to adjust `-p operationcount=100000` dynamically according to the specific execution time to ensure that the execution time is longer than 20 minutes; otherwise, the result data will not be representative.
>- `w` in `?w=0` represents write concern.
>  - `w:1` (acknowledged write) requires an acknowledgment that the write operation has propagated to the specified mongod instance or the primary node in the replica set. The default value is 1.
>  - `w:0` (unacknowledged write) returns no response and therefore will not report whether the write operation succeeds. However, it may return the exception information when data is written to a closed socket or the network is abnormal.
>  - `w:>1` (used in a replica set) is used to set the number of nodes where data is to be written, including the primary node.

## Test Data
### 50:50 read/update request ratio

|  MongoDB Specification      | Threads | Throughput (Ops/Sec) | RAL (μs) | WAL (μs)  | CPU Utilization |
| ------- | ------- | ------------------- | ------- | ------- | --------- |
| 2-core 4 GB    | 100     | 3188                | 24091   | 38254   | 100%      |
| 2-core 4 GB    | 200     | 5510                | 34475   | 38022   | 100%      |
| 4-core 8 GB    | 100     | 7058                | 8355    | 19887   | 100%      |
| 4-core 8 GB        | 200     | 13590               | 14391   | 14983   | 100%      |
| 6-core 16 GB   | 100     | 8970                | 22132   | 51      | 100%      |
| 6-core 16 GB        | 200     | 10041               | 28696   | 10966   | 100%      |
| 12-core 32 GB  | 100     | 29462               | 6727    | 35      | 100%      |
| 12-core 32 GB      | 200     | 47815               | 4673    | 3681    | 100%      |
| 24-core 64 GB  | 100     | 107047              | 1826    | 33      | 100%      |
| 24-core 64 GB       | 200     | 51046               | 7802    | 27      | 100%      |
| 24-core 128 GB | 100     | 130811              | 1486    | 32      | 100%      |
| 24-core 128 GB       | 200     | 49274               | 8054    | 27      | 100%      |
| 32-core 240 GB | 100     | 154253              | 1254    | 32      | 100%      |
| 32-core 240 GB        | 200     | 52148               | 8243    | 1108    | 100%      |
| 48-core 512 GB | 100     | 174284              | 1103    | 28      | 100%      |
| 48-core 512 GB       | 200     | 121713              | 3237    | 32      | 100%      |

### 95:5 read/update request ratio

|  MongoDB Specification      | Threads | Throughput (Ops/Sec) | RAL (μs) | WAL (μs)  | CPU Utilization |
| ------- | ------- | ------------------- | ------- | ------- | --------- |
| 2-core 4 GB	   | 100     | 2738                | 38216   | 178     | 100%      |
| 2-core 4 GB	       | 200     | 10093               | 20178   | 11561   | 100%      |
| 4-core 8 GB	    | 100     | 14380               | 6864    | 7631    | 100%      |
| 4-core 8 GB	        | 200     | 26459               | 7651    | 5369    | 100%      |
| 6-core 16 GB	   | 100     | 13707               | 7650    | 56      | 100%      |
|  6-core 16 GB	       | 200     | 45796               | 4383    | 3928    | 100%      |
| 12-core 32 GB	  | 100     | 115529              | 902     | 37      | 100%      |
| 12-core 32 GB	       | 200     | 56751               | 3658    | 31      | 100%      |
| 24-core 64 GB	  | 100     | 160227              | 668     | 29      | 100%      |
| 24-core 64 GB	        | 200     | 112755              | 1876    | 32      | 100%      |
| 24-core 128 GB	 | 100     | 159130              | 659     | 26      | 100%      |
| 24-core 128 GB	       | 200     | 112993              | 1936    | 32      | 100%      |
| 32-core 240 GB	 | 100     | 167518              | 634     | 28      | 74%       |
| 32-core 240 GB	        | 200     | 172424              | 1244    | 35      | 100%      |
| 48-core 512 GB	 | 100     | 173768              | 608     | 31      | 50%       |
|  48-core 512 GB	       | 200     | 211986              | 1012    | 33      | 85%       |

