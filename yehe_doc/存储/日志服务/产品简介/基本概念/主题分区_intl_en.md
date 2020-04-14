## Overview

Partition is the smallest read/write unit of Cloud Log Service (CLS). A log topic can be divided into several partitions and must have at least one partition. CLS uses the value range of MD5 as the valid range and controls the overall throughput performance by merging or splitting partitions. A log topic supports up to 50 partitions. It is recommended that you perform operations and use topic partitions rationally to prevent waste of resources.

Basic attributes of a partition:

- **Partition number**
  Every partition has a unique number under the same log topic, which is assigned by the system after partition creation or operation.
- **Partition range**
  Every partition has a left-closed and right-open interval.
- **Partition status**
  - Read-write: the current partition allows read and write.
  - Read-only: the current partition is read-only and no data can be written to it.

  

## Partition Range

With a partition range, logs can be written in the HashKey mode. The valid range of a log topic is the value range of MD5, which is `[00000000000000000000000000000000,ffffffffffffffffffffffffffffffff)`. All read-write partitions segment the entire value range of a log topic and each occupies a left-closed and right-open interval to ensure that every log record collected is written to the corresponding partition.

CLS provides two write modes: load-balancing mode and HashKey mode.

- **Load-balancing mode**: every data packet is written to a random log topic partition.
- **HashKey mode**: every data packet is written to the topic partition that contains the current Key value.

For example, a log topic has three read-write partitions and their ranges are as follows:

| Partition No. | Status | Partition Range |
| -------- | ---- | ------------------------------------------------------------ |
| 1 | Read-write | `[00000000000000000000000000000000,7fffffffffffffffffffffffffffffff）` |
| 2 | Read-write | `[7fffffffffffffffffffffffffffffff,a0000000000000000000000000000000）` |
| 3 | Read-write | `[a0000000000000000000000000000000,ffffffffffffffffffffffffffffffff）` |

If the write mode is HashKey, log data with the Key value of `2fffffffffffffffffffffffffffffff` is written to partition 1 and log data with the Key value of `9f000000000000000000000000000000` is written to partition 2.



## Read and Write Capability of Partitions

Each partition has a certain level of read and write capability. We recommend that you plan partition count based on the actual log traffic of your business. Split partitions when the traffic is higher than the read and write capability of the log topic, and merge partitions when the traffic is lower than the read and write capability of the log topic to save resources.

- Every partition provides read capability of 5 MB/s.
- Every partition provides write capability of 5 MB/s.



## Partition Status

A partition can be in **read-write** or **read-only** mode. Only read-write partitions support data writing. Read-only partitions does not allow data writing but can be consumed within their lifetime. All partitions are readable and writable when they are created, but merging and splitting operations will change the status to read-only.

#### Merging partitions

Two adjacent read-write partitions can be merged into one partition. After two partitions are merged, the two original partitions become read-only, which only allow data consumption, but not data writing. The new partition is readable and writable and covers the range of the two original partitions.

![](https://main.qcloudimg.com/raw/cbe51af3ace4388f1ca8b5a36d30dbe6.png)

#### Splitting a partition

A read-write partition can be split into two partitions with smaller ranges. When splitting a partition, you need to specify the MD5 value of a split point, which must be larger than the value of the start point and smaller than the value of the end point. After a partition is split, the original partition becomes read-only, which only allows data consumption, but not data writing. The new partition is readable and writable and covers the range of the original partition.

![](https://main.qcloudimg.com/raw/2c13d5f4948a22306b880763908fe72a.png)
