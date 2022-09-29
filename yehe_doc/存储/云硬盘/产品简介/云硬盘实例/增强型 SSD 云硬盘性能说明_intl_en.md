Starting from January 2021, a single Enhanced SSD disk performance consists of **basic performance** and **extra performance**:
- Basic performance varies linearly with cloud disk capacity and reaches the maximum value at the critical point.
- If you have a higher performance requirement, you can enable and configure extra performance.

This document introduces basic performance and extra performance.

## Overall Performance

For a single Enhanced SSD disk, its performance consists of two parts: **basic performance** and **extra performance**. The following table specifies the maximum performance, regardless of the performance proportion.

| Performance Metric | Maximum Value |
| --------------------- | ------ |
| Random IOPS             | 100,000 |
| Max throughput (MB/s)    | 1000   |



## Basic Performance

For Enhanced SSD, its basic performance varies linearly with the disk capacity. The basic performance cannot be adjusted independently, which is calculated by the following formula.

| Basic Performance Metric    | Calculation Formula         | Maximum Value |
| ---------------------------- | --------------------------- | -------------- |
| Random IOPS         | min {1800 + capacity (GB) x 50, 50000} | 50000          |
| Max throughput (MB/s) | min {120 + capacity (GB) x 0.5, 350}   | 350            |

According to the formula,

- If the disk capacity is 460 GB, the throughput reaches the maximum value and its basic performance is: random IOPS: 24,800; max throughput: 350 MB/s.
- If the disk capacity is 964 GB, the random IOPS reaches the maximum value and its basic performance is: random IOPS: 50,000; max throughput: 350 MB/s.



## Extra Performance

If you have a higher performance requirement, you can enable extra performance.

### Prerequisites

The following requirements must be met to enable extra performance:

- Currently, this feature is only available to **Enhanced SSD** and **ulTra SSD** disks.
- The extra performance can be configured only after either basic performance metric reaches its maximum value. In other words, the disk capacity must be greater than 460 GB according to the basic performance formula.

### Extra performance formula

Refer to the following formula to configure the extra performance.

| Extra Performance Metric  | Calculation Formula      | Maximum Value |
| ---------------------------- | --------------------- | -------------- |
| Random IOPS         | min {configured value x 128, 50,000} | 50,000          |
| Max throughput (MB/s) | min {configured value x 1, 650}     | 650            |

### Extra performance price
For more information on extra performance prices, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

## Examples

**Sample 1: An Enhanced SSD disk requires a capacity of 2,000 GB and throughput of 500 MB/s**

This capacity configuration reaches the throughput limit of basic performance and needs to configure extra throughput performance: (500-350)/1 = 150. Therefore, you need to purchase an Enhanced SSD disk with a capacity of 2,000 GB and extra throughput performance of 150 MB/s.

**Sample 2: An Enhanced SSD disk requires a capacity of 1,000 GB and IOPS of 50,000**
This capacity configuration reaches the random IOPS limit of basic performance, and the required IOPS is met. Therefore, you only need to purchase an Enhanced SSD disk with a capacity of 1,000 GB.

