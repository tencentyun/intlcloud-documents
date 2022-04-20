Tencent Cloud Block Storage (CBS) provides a persistent block storage service for CVM instances.

- CBS automatically stores data in multiple redundant copies in an availability zone to eliminate the risk of single points of data failure, providing up to 99.9999999% data reliability.
- CBS offers cloud disks of multiple types and specifications to achieve stable and low-latency storage performance.
- Cloud disks can be attached to and detached from CVM instances in the same availability zone. It takes only a few minutes to adjust the disk capacity. 


## Typical Use Cases
- When your CVM is running out of disk space, you can purchase one or more cloud disks and attach them to the CVM.
- You don’t need to purchase extra storage capacity while purchasing a CVM. You can purchase cloud disks later when it’s necessary.
- When you need to transfer data from one CVM to another, just detach the cloud data disk from the source CVM and attach it to the target CVM.
- Use multiple cloud disks to form a Logical Volume Manager (LVM) to go beyond the physical limit of a single cloud disk.
- Use multiple cloud disks to form a Redundant Array of Independent Disks (RAID) configuration to go beyond the I/O performance limit of a single cloud disk.


## Lifecycle
- The lifecycle of a **non-elastic cloud disk** is the same as that of the CVM. It is purchased with the CVM and used as a system disk. It cannot be attached to or detached from CVMs.
- The lifecycle of an **elastic cloud disk** is independent from CVM instances. You can attach multiple cloud disks to a CVM instance as data disks, detach them, and then reattach them to another instance.

## Types
Four types of cloud disks are provided, including **Premium Cloud Storage**, **SSD**, **Enhanced SSD**, and **Tremendous SSD**. Each type has unique performance and characteristics, and the price varies. You can choose the cloud disk type that best suits your application requirements. For more information, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636) and [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

## Relevant Operations
- For information on CVM instance and cloud disk configurations, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744) and [Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).
- For information about best practices for capacity expansion, detachment, termination, and other operations, see the [CBS documentation](https://intl.cloud.tencent.com/document/product/362).



