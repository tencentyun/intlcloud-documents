## Overview
A local disk is a storage device on the same physical server as the CVM instance. It features high read/write I/O and low latency.
The local disk is a local storage device on the same physical server as the CVM instance. It is a reserved storage space on the physical server (currently only available to high I/O and big data CVM instances). The reliability of data stored on a local disk depends on that of the physical server. There may be a single point of failure.



<dx-alert infotype="notice" title="">
- In case of a hardware failure on the physical server of the CVM, local disk data lose may occur. We recommend data redundancy at the application layer to ensure reliability. If your application does not support this, consider using [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) to improve data reliability.
- For a CVM using a local disk as the system disk, hardware (CPU, memory, and storage) upgrade is not supported. You can only adjust the bandwidth of the instance.
</dx-alert>



## Use Cases
- **IO-intensive applications**: For large relational databases, NoSQL, ElasticSearch, and other I/O-intensive applications that are more sensitive to latency, you can use the NVME SSD local disk that comes with high I/O CVM instances, but note that it carries the risk of a single point of failure.
- **Big data applications**: For big data applications such as EMR that are less sensitive to latency and feature data redundancy at the upper layer to tolerate a single point of failure, you can use the SATA HDD disk that comes with big data CVM instances.


## Local Disk Lifecycle
The lifecycle of a local disk is the same as that of the CVM instance it is attached. Therefore, local disks launch and terminate with CVM instances.

## Local Disk Types

Local disks are local storage devices on the same physical server as the CVM instance. There are two types of local disks by media: SATA HDD and NVME SSD.

| Disk Type | CVM |
|---------|---------|
| Local SATA HDD | [Big data CVM](https://intl.cloud.tencent.com/document/product/213/11518) |
| Local NVME SSD | [High I/O CVM](https://intl.cloud.tencent.com/document/product/213/11518) |

## Purchasing a Local Disk
A local disk can only be purchased together with a CVM instance. For more information on purchasing a CVM instance, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).
