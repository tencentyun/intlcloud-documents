## What is Tencent Cloud Block Storage?
Cloud Block Storage (CBS) is a highly available, highly reliable, low-cost, and customizable block storage device. It can be used as an independent and scalable disk for CVM, providing efficient and reliable [storage](https://intl.cloud.tencent.com/document/product/213/4952) devices. CBS provides long-term storage at the data block level. It is typically used as the primary storage device for data that requires frequent and fine-grained updates (such as file system and database), featuring high availability, reliability, and performance. CBS uses a three-copy distributed mechanism to back up your data on different physical machines to avoid data loss caused by a single point of failure, improving data reliability.
You can easily purchase, adjust, and manage your cloud disk devices through the console, and build a file system to create storage space larger than that of a single cloud disk. Cloud disks can be classified according to different lifecycles as follows:
- Lifecycle of non-elastic cloud disk completely follows that of the CVM. It is purchased with the CVM and used as a system disk. It does not support mounting and unmounting.
- Lifecycle of elastic cloud disk is independent of that of the CVM. It can be purchased separately and manually mounted to the CVM. It can also be purchased with the CVM and automatically mounted to the CVM as a data disk. Elastic cloud disk supports mounting to and unmounting from the CVM in the same availability zone at any time. You can mount multiple elastic cloud disks to the same CVM, or unmount a cloud disk from CVM A and then mount it to CVM B.

Tencent Cloud places quota limits on users’ cloud disks. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/362/32406).

## Typical Use Cases
- You can purchase and mount one or more cloud disks to meet the requirements for storage capacity when the disk space on your CVM is insufficient.
- When purchasing the CVM, you do not need additional storage space. When you have storage requirements, you can expand the CVM storage capacity by purchasing a cloud disk.
- When there is a data exchange request between multiple CVMs, you can unmount cloud disks (data disks) and remount them to other CVMs.
- You can expand the maximum storage capacity of a single cloud disk by purchasing multiple cloud disks and configuring a Logical Volume Manager (LVM).
- You can expand the maximum I/O capacity of a single cloud disk by purchasing multiple cloud disks and configuring a Redundant Array of Independent Disks (RAID) policy.

## Features
Tencent Cloud provides a variety of long-term storage devices, allowing the user to select an appropriate type of cloud disk to store files, build databases, etc.
- Tencent Cloud CBS comes with the following disk types: Premium Cloud Disk, SSD, Enhanced SSD, and ulTra SSD.
- Elastic mounting and unmounting: all types of elastic cloud disks support elastic mounting and unmounting. You can mount multiple cloud disks on a CVM to build a file system with high capacity.
- Elastic expansion: a single disk supports a maximum capacity of 32 TB. You can scale up the disk at any time.
- Snapshot backup: you can create and roll back a snapshot to back up data. You can also create a cloud disk from the snapshot to accelerate your business deployment.
