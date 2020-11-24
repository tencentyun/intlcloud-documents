## Overview
A local disk is a storage device on the same physical server as the CVM instance. It features high read/write IO and low latency.
The local disk is a local storage device on the same physical server as the CVM instance. It is a reserved storage space on the physical server (currently only available to high IO and big data CVMs). The reliability of data stored on a local disk depends on that of the physical server. There may be a single point of failure.



>! 
> - If a hardware failure occurs on the physical server of the CVM instance, local disk may lose valuable data. We recommend data redundancy at the application layer to ensure reliability. If your application does not support this, consider using [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) to improve data reliability.
> - You cannot upgrade the hardware (CPU, memory, storage) of a CVM instance with only local disks. You can only upgrade its bandwidth.
> 

## Scenario
- **IO-intensive applications**: for large relational databases, NoSQL, ElasticSearch and other I/O-intensive applications that are more sensitive to latency, you can use the NVME SSD local disk that comes with high IO CVMs, but take note that it carries the risk of a single point of failure.
- **Big data applications**: for big data applications such as EMR that are less sensitive to latency and feature data redundancy at the upper layer to tolerate a single point of failure, you can use the SATA HDD disk that comes with big data CVMs.


## Lifecycle
The lifecycle of a local disk is the same as that of the CVM instance it is mounted to. Therefore, local disks launch and terminate with CVM instances.

## Types

Local disks are local storage devices on the same physical server as the CVM instance. There are two types of local disks by media: SATA HDD and NVME SSD.

| CVM | Specification and Performance |
|---------|---------|
| SATA HDD local disk | [Big data CVMs](https://intl.cloud.tencent.com/document/product/213/11518#D) |
| NVME SSD local disk | [High IO CVMs](https://intl.cloud.tencent.com/document/product/213/11518#I) |

## Purchase
A local disk can only be purchased together with a CVM instance. For more information on purchasing a CVM instance, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).

