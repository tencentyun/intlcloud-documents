Welcome to Tencent Cloud Cloud Block Storage (CBS).

CBS is a highly available, highly reliable, low-cost, customizable network block storage device. For more information, see [CBS Product Overview](https://intl.cloud.tencent.com/document/product/362/2345).

You can use the APIs described in this documentation to perform operations on cloud disks and snapshots, such as creating an elastic cloud disk, creating a snapshot, or rolling back a snapshot. For more information about supported operations, see [API Overview](https://intl.cloud.tencent.com/document/product/362/15634).

Before you use CBS APIs, make sure that you fully understand the [CBS product overview](https://intl.cloud.tencent.com/document/product/362/2345), [usage](https://intl.cloud.tencent.com/document/product/362/5744), and [billing modes](https://intl.cloud.tencent.com/document/product/362/2413).

## Glossary

The following table introduces some commonly used terms in CBS to quickly familiarize you with the cloud disk and snapshot services.

| Term | Full Name | Description |
| --- |  --- | --- |
| [CBS](https://intl.cloud.tencent.com/document/product/213/4953) | Cloud Block Storage | Distributed block storage independently developed by Tencent Cloud. CBS includes cloud disks purchased with CVMs and elastic cloud disks purchased separately. For more information, see [CBS Product Overview](https://intl.cloud.tencent.com/doc/product/362/%E4%BA%A7%E5%93%81%E6%A6%82%E8%BF%B0). |
| [Elastic Cloud Disk](https://intl.cloud.tencent.com/document/product/213/4953#1.2.-.E5.BC.B9.E6.80.A7.E4.BA.91.E7.A1.AC.E7.9B.98) | Elastic Cloud Disk | A cloud disk that is not purchased along with a CVM (purchased separately), with an independent lifecycle (billing cycle). It can be mounted and unmounted among different CVMs. It cannot be simultaneously mounted to multiple CVMs. |
| [Snapshot](https://intl.cloud.tencent.com/document/product/362/31638) | Cloud Disk Snapshot | Used to save a copy of a cloud disk at a specific point in time. You can use the snapshot to restore the cloud disk to the point in time when the snapshot was created. |

#### Description of input and output parameters

* `Limit` and `Offset`
>These parameters are used for paging control. `Limit` indicates the maximum number of entries returned at a time, and `Offset` indicates the offset value. If the number of results exceeds the value of `Limit`, the number of returned results is equal to the value of `Limit`.
>
>For example, if `Offset` is set to 0 and `Limit` is set to 20, the 0th to 19th entries are returned; if `Offset` is set to 20 and `Limit` is set to 20, the 20th to 39th entries are returned; if `Offset` is set to 40 and `Limit` is set to 20, the 40th to 59th entries are returned.
    
* `Ids.N`
>Format for inputting multiple parameters at a time. If a parameter is in such a format, you can specify multiple values for the parameter. For example:
>   
>`Ids.0=10.12.243.21&Ids.1=10.11.243.21&Ids.2=10.12.243.21&Ids.3=10.13.243.21…`
>   
>`N` starts from 0.

## Getting Started with APIs

To use an elastic cloud disk through APIs, complete the following 3 steps:

1. Create an elastic cloud disk: call the [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312) API to create an elastic cloud disk.
2. Mount the elastic cloud disk to the specified CVM: after the elastic cloud disk is created, call the [AttachDisks](https://intl.cloud.tencent.com/document/product/362/16313) API to mount it to the specified CVM. **Note: the term "mount" in this documentation refers to assigning the elastic cloud disk to the specified CVM, which is equivalent to hot-plugging a disk to a server.**
3. Log in to the CVM to initialize the elastic cloud disk: when using the new elastic cloud disk for the first time, you need to perform operations such as partitioning and formatting. For more information, see [Data Disk Partitioning and Formatting on Windows Systems](https://intl.cloud.tencent.com/document/product/213/2158) and [Partitioning, Formatting, Mounting, and File System Creation on Linux Systems](https://intl.cloud.tencent.com/document/product/362/31598). Note: for Linux systems, partitioning is not necessary. You can skip the partitioning process and directly proceed to formatting.


To use cloud disk snapshots through APIs, complete the following 2 steps:

1. Create a cloud disk snapshot: call the [CreateSnapshot](https://intl.cloud.tencent.com/document/product/362/15648) API to create a snapshot of the specified cloud disk.
2. Roll back the cloud disk snapshot: if necessary, you can call the [ApplySnapshot](https://intl.cloud.tencent.com/document/product/362/15643) API to roll back the snapshot to the specified cloud disk.


## Use Limits

For limits on how to use cloud disks and snapshots, see [CBS Use Limits](https://intl.cloud.tencent.com/document/product/362/32406). For limits on specific parameters, see the descriptions of output parameters in related API documents.

