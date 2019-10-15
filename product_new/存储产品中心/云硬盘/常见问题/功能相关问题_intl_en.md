### What are the characteristics of Tencent Cloud CBS?
Tencent Cloud CBS provides three disk types: HDD cloud disk, premium cloud storage, and SSD cloud disk. Cloud disk characteristics are as follows:
- Elastic mounting and unmounting: Elastic cloud disk supports mounting and unmounting. Each CVM supports the mounting of up to 20 elastic cloud disks as data disks. 
- Elastic expansion: A single disk supports a maximum capacity of 16TB, you can perform cloud disk expansion at any time.
- Snapshot backup: You can back up data by creating a snapshot, improving data reliability and allowing rapid data recovery when necessary. You can also create a new cloud disk based on the snapshot, achieving rapid business deployment.

### What limits do cloud disks have?
- A single elastic cloud disk has a maximum capacity of 16TB.  Expansion within its maximum capacity is supported, but not capacity reduction.
- Elastic cloud disk only supports mounting to CVMs in the same availability zone.
- A single CVM supports the mounting of up to 20 elastic cloud disks as data disks. They can be added directly when you purchase the CVM, or [mounted](https://intl.cloud.tencent.com/document/product/362/31594) after the CVM purchase.
- In the [CBS console](https://console.cloud.tencent.com/cvm/cbs), you can purchase up to 50 elastic cloud disks at one time. Under a single Tencent Cloud account, you can purchase up to 500 elastic cloud disks.
  
  >When [mounting cloud disks](https://intl.cloud.tencent.com/document/product/362/31594), the system automatically enables the automatic renewal feature of the elastic cloud disk, preventing business interruption that may happen if you forget to pay the renewal fee.

### What is the difference between different types of cloud disk?
Cloud disks provide three volume options:
- HDD cloud disk: Suitable for sequential read-write of large files such as logs, and for infrequent access scenarios.
- Premium cloud storage: Suitable for most I/O scenarios such as web servers and all types of small and mid-sized databases.
- SSD cloud disk: Suitable for transactional workloads, and large-sized databases.

The performance and pricing of different types of cloud disks are different. You can choose the type of cloud disk you need based on your budget and application requirements. For more information on disk types and performance, see [Cloud disk types](https://intl.cloud.tencent.com/document/product/362/31636).

### What advantages do cloud disks have?
Cloud disks have advantages such as reliability, elasticity, high performance, ease of use, and snapshot backup. For more information, see [Product Advantages](https://intl.cloud.tencent.com/document/product/362/3039).

### Can elastic cloud disks be used as system disks?
No. System disks cannot be unmounted or mounted.

<span id="Q1"></span>
### Can cloud disks be used as data disks?
All types of local disks and cloud disks can be used as data disks.

### Do cloud disks support mounting and unmounting?
- Elastic cloud disks support mounting and unmounting.
- System disks do not support mounting and unmounting.

### Do elastic cloud disks support batch mounting and unmounting?
-  Elastic cloud disks support batch mounting and unmounting.
- System disks do not support mounting and unmounting. 
