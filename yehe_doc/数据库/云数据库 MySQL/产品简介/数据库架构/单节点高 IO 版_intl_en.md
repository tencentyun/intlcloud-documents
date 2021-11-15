TencentDB for MySQL supports four types of architectures: the High-availability Edition, the Finance Edition, the Single-node High IO Edition, and the Basic Edition. This document describes the Single-node High IO Edition.


The Single-node High IO Edition adopts a single-physical node architecture with high cost performance.

## Use Cases
Ideal for various industries with read/write separation requirements.

## Features
The Single-node High IO Edition uses local NVMe SSD disks for underlying storage with excellent IO performance and is ideal for [read-only instances](https://intl.cloud.tencent.com/document/product/236/7270) to share business read load.

## Basic Framework Diagram
![Alt text](https://main.qcloudimg.com/raw/6e3a6ad27f806f2485668cdfae8dc19f.png)
>!
>- Single-node deployment is susceptible to single points of failure. If only one read-only instance is purchased, it is impossible to ensure high availability for your business, because a failure of the single read-only instance will lead to business disruption.
>- As the time taken to recover a single read-only instance depends on the business data volume, the recovery time cannot be guaranteed. As a result, if your business requires high availability, we recommend you purchase at least two read-only instances for the [RO group](https://intl.cloud.tencent.com/document/product/236/11361).


## Relevant Operations
- You can create one or more read-only instances, which can be applied to read/write separation and one-source-multiple-replica application scenarios. For more information, please see [Read-only Instances](https://intl.cloud.tencent.com/document/product/236/7270).
- You can create one or more read-only instances and put them in an RO group to ensure availability. For more information, please see [RO Group of Read-only Instance](https://intl.cloud.tencent.com/document/product/236/11361).

