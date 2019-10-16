## What is Tencent Cloud Block Storage?
Cloud Block Storage (CBS) is a highly available, highly reliable, low-cost, and customizable block storage device. It can be used as an independent and scalable disk for CVM, providing efficient and reliable [storage](https://intl.cloud.tencent.com/document/product/213/4952) devices for CVM instances. CBS provides long-term storage at the data block level. It is typically used as the primary storage device for data that requires frequent and fine-grained updates (such as file system and database), and has high availability, high reliability, and high performance. CBS uses a three-copy distribution mechanism to back up your data on different physical machines to avoid data loss caused by a single point of failure, improving data reliability.
You can easily purchase, adjust, and manage your cloud disk devices through the console, and create a storage space that has larger capacity than a single cloud disk by building a file system. Cloud disks can be classified according to different lifecycles as follows:

- Lifecycle of non-elastic cloud disk completely follows that of CVM. It is purchased with the CVM and used as a system disk. It does not support mounting and unmounting.
- Lifecycle of elastic cloud disk is independent of that of CVM. It can be purchased separately and then manually mounted to the CVM. It can also be purchased with the CVM and automatically mounted to the CVM to be used as a data disk. Elastic cloud disk supports the mounting and unmounting on CVM in the same availability zone at any time. You can mount multiple elastic cloud disks to the same CVM, or unmount a cloud disk from CVM A and then mount it to CVM B.

Tencent Cloud places corresponding limits on users’ cloud disk quotas. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/362/5145).

## Typical use cases
- CVM discovers during use that disk space is insufficient. You can purcahse a disk or mount multiple cloud disks to the CVM to satisfy storage capacity requirements.
- When you purchase a cloud server, you do not need additional storage space. When you have storage requirements, you can expand the storage capacity of the CVM by purchasing a cloud disk.
- When there is a data exchange request between multiple CVMs, you can unmount cloud disks (data disks) and remount them to other CVMs.
- You can break through the maximum storage capacity of a single cloud disk by purchasing multiple cloud disks and configuring a Logical Volume Manager (LVM).
- You can break through the maximum I/O capacity of a single cloud disk by purchasing multiple cloud disks and configuring a Redundant Array of Independent Disks (RAID) policy.

## Product Features
Tencent Cloud provides a variety of long-term storage devices, allowing user to select an appropriate type of cloud disk to store files, build databases, etc.
- 5 disk options: Local Disk, SSD Local Disk, HDD Cloud Storage, Premium Cloud Storage, and SSD Cloud Storage.
- Elastic mounting and unmounting: All types of elastic cloud disks support elastic mounting and unmounting. You can mount multiple cloud disks on a CVM to build a file system with high capacity.
- Elastic expansion: You can perform elastic expansion to a cloud disk at any time, and a single disk supports a maximum capacity of 16TB.
- Snapshot backup: It supports snapshot creation and rollback, the timely backup of key data, and the creation of disks using snapshots to achieve rapid business deployment.
