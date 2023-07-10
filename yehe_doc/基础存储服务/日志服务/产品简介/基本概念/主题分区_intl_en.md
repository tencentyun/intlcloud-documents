## Overview

Partition is the smallest read/write unit of CLS. A log topic can be divided into several partitions and must have at least one partition. CLS uses the value range of MD5 as the valid range and controls the overall throughput performance by merging or splitting partitions. A log topic supports up to 50 partitions. We recommend that you use and work with topic partitions rationally to prevent waste of resources.

Basic attributes of a partition:

- **Partition number**: every partition has a unique number under the same log topic, which is assigned by the system after partition creation or operation.
- **Partition range**: every partition has a left-closed and right-open interval.
- **Partition status**:
  - Read-write: the current partition allows read and write.
  - Read-only: the current partition is read-only and no data can be written to it.

>? Topic partitioning is a complex concept. You are advised to use the [Auto Split](https://intl.cloud.tencent.com/document/product/614/39587) function in actual practice. CLS automatically adjusts topic partitioning based on the volume of log data.
>

## Partition Range

With a partition range, logs can be written in the HashKey mode. The valid range of a log topic is the value range of MD5, which is `[00000000000000000000000000000000,ffffffffffffffffffffffffffffffff)`. All read-write partitions segment the entire value range of a log topic and each occupies a left-closed and right-open interval to ensure that every log record collected is written to the corresponding partition.

CLS provides two write modes: load-balancing mode and HashKey mode.

- **Load-balancing mode**: every data packet is written to a random log topic partition.
- **HashKey mode**: every data packet is written to the topic partition that contains the current Key value.

For example, a log topic has three read-write partitions and their ranges are as follows:

| Partition No. | Status | Partition Range |
| -------- | ---- | ------------------------------------------------------------ |
| 1 | Read-write | `[00000000000000000000000000000000,7fffffffffffffffffffffffffffffff)` |
| 2 | Read-write | `[7fffffffffffffffffffffffffffffff,a0000000000000000000000000000000)` |
| 3 | Read-write | `[a0000000000000000000000000000000,ffffffffffffffffffffffffffffffff)` |

If the write mode is HashKey, log data with the Key value of `2fffffffffffffffffffffffffffffff` is written to partition 1 and log data with the Key value of `9f000000000000000000000000000000` is written to partition 2.

## Read and Write Capability of Partitions

Each partition has a certain level of read and write capability. We recommend that you plan partition count based on the actual log traffic of your business. Split partitions when the traffic is higher than the read and write capability of the log topic, and merge partitions when the traffic is lower than the read and write capability of the log topic to save resources.

<table>
<tr>
   <th>Feature</td>
   <th>Item</td>
   <th>Description</td>
 </tr>
<tr>
   <td rowspan="2">Frequency control</td>
   <td>Write requests</td>
   <td>Every partition supports a maximum of 500 QPS of write operations. It will reject requests and return the status code 429 with an error message of "SpeedQuotaExceed" when the limit is exceeded.</td>
 </tr>
 <tr>
   <td>Read requests</td>
   <td>Every partition supports a maximum of 200 QPS of read operations. It will reject requests and return the status code 429 with an error message of "SpeedQuotaExceed" when the limit is exceeded.</td>
 </tr>
 <tr>
   <td >Traffic throttling</td>
   <td>Write traffic</td>
   <td>Every partition supports the write traffic of up to 5 MB/sec. It will truncate data and return the status code 429 with an error message of "SpeedQuotaExceed" when the limit is exceeded.</td>
 </tr>
</table>



## Partition Status

A partition can be in **read-write** or **read-only** mode. Only read-write partitions support data writing. Read-only partitions do not allow data writing but can be consumed within their lifetime. All partitions are readable and writable when they are created, but merging and splitting operations will change the status to read-only.

#### Merging partitions

Two adjacent read-write partitions can be merged into one partition. After two partitions are merged, the two original partitions become read-only, which only allow data consumption, but not data writing. The new partition is readable and writable and covers the range of the two original partitions.




#### Splitting a partition

A read-write partition can be split into two partitions with smaller ranges. When splitting a partition, you need to specify the MD5 value of a split point, which must be larger than the value of the start point and smaller than the value of the end point. After a partition is split, the original partition becomes read-only, which only allows data consumption, but not data writing. The new partition is readable and writable and covers the range of the original partition.


