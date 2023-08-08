## Overview
TXSQL supports the Contention-Aware Transaction Scheduling (CATS) algorithm. This new algorithm automatically detects lock contention between transactions and schedules them based on their scheduling weights.
MySQL supports another transaction scheduling algorithm, aka First In First Out (FIFO), which was introduced earlier than CATS. When multiple transactions are waiting for the same lock, CATS prioritizes them by assigning a scheduling weight which is computed based on the number of transactions that a transaction blocks. The transaction with a higher scheduling weight will be executed sooner. Thus, transaction throughput is improved.

## Supported Versions
- Kernel version: MySQL 5.7 20190230 and above.
- Kernel version: MySQL 8.0 20200630 and above.

## Use Cases
This feature is suitable for use cases under high concurrency and heavy lock contention.

## Performance Data
TPS is improved by more than 50% under high concurrency and heavy lock contention.

- Test method: use the oltp_read_write.lua script of sysbench (pareto random type enabled) to test TPS on eight tables (10 MB data) at the REPEATABLE READ transaction isolation level
- Test environment: TencentDB instance with 32 cores and 128 GB memory

| Thread Count | FCFS (FIFO) | CATS  | Performance Improvement |
| :----- | :--------- | :---- | :------- |
| 128    | 11,999      | 12,005 | 0%       |
| 256    | 6,609       | 10,137 | 53%      |
| 512    | 3,453       | 9,365  | 171%     |
| 1,024   | 2,196       | 7,015  | 219%     |

## Instructions
In MySQL 5.7, you can use the global parameter `innodb_trx_schedule_algorithm` to specify the transaction scheduling algorithm. The default value is `auto`.
Valid values:
- auto: Automatically adjust the transaction scheduling algorithm based on current system status. If the number of threads waiting for a lock exceeds 32, adopt CATS; otherwise, adopt First Come First Serve (FCFS), an algorithm similar to FIFO.
- fcfs: Adopt the FCFS algorithm.
- cats: Adopt the Contention-Aware Transaction Scheduling algorithm.


| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ----------------------------- | ---- | ------ | ---- | ---------------- | ---------------- |
| innodb_trx_schedule_algorithm | Yes  | string | auto | [auto,fcfs,cats] | Specify the transaction scheduling algorithm |
>?Currently, you cannot directly modify the values of the above parameter. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
In MySQL 8.0, `auto` is the only valid value.

