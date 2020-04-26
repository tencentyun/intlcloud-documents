Tencent Cloud Cloud Block Storage (CBS) provides a persistent block storage service for CVM instances.

- CBS automatically stores data in multiple redundant copies in an availability zone to eliminate the risk of single points of data failure, providing up to 99.9999999% data reliability.
- CBS offers cloud disks of multiple types and specifications to achieve stable and low-latency storage performance.
- CBS supports mounting and unmounting to instances in the same availability zone. You can use it to adjust storage capacity in minutes to satisfy elastic demands and pay for only what you use.


## Typical use cases
- When disk space becomes insufficient during use, you can purchase one or more cloud disks to satisfy storage capacity requirements.
- Purchase cloud disks to meet storage demands you did not plan for when buying the CVM instance.
- Store data on a cloud disk, unmount it, then mount it to another CVM instance to transfer data.
- Use multiple cloud disks to form a Logical Volume Manager (LVM) to go beyond the physical limit of a single cloud disk.
- Use multiple cloud disks to form a RAID configuration to improve the I/O performance of a single cloud disk.


## Lifecycle
The lifecycle of an Elastic Cloud Disk is independent of CVM instances. You can mount multiple cloud disks to a CVM instance and unmount them in order to mount them to another CVM instance.

### Purchase and Use
- For information on cloud disk types, refer to [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).
- For information on how to purchase cloud disks, refer to the [Price Overview of CBS](https://intl.cloud.tencent.com/document/product/362/2413)
- For information on CVM instance and cloud disk specifications, refer to [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744) and [CBS documentation](https://intl.cloud.tencent.com/document/product/362/5745).
- For information about cloud disk best practices for capacity expansion, unmounting, termination, and other operations, refer to the [CBS documentation](https://intl.cloud.tencent.com/document/product/362).
