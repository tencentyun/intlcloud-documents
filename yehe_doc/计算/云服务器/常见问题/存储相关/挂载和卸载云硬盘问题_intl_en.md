### What is a device name (mount point)?
A device name (mount point) is the location of a cloud disk mounted to the CVM instance on the disk controller bus. The selected device name matches the disk device number in Linux and matches the disk sequence number of the disk manager in Windows.

### Can I mount one cloud disk to multiple CVM instances?
No. You can mount up to 20 cloud disks to the same CVM, but you cannot mount the same cloud disk to multiple CVMs. You can only share data by [unmounting the cloud disk](https://intl.cloud.tencent.com/document/product/362/32400) from CVM A and then [mounting](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.

### Do I need to partition the cloud disk after purchasing and mounting it to a CVM instance?
Yes. After you purchase a cloud disk, you must mount it to a CVM instance in the same availability zone, and then initialize it by formatting, partitioning, and creating the file system before using it as a data disk. For more information, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645) and [Initializing Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645).

### Why am I unable to locate the data disk that I purchased for a Linux instance?
If you purchase a data disk separately, you must partition, format, and mount it to an instance to view and use its storage space. For more information, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645) and [Initializing Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645).

### How many cloud disks can be mounted to one CVM instance?
A maximum of 20 data disks can be mounted to one CVM instance.

### Why can’t I locate the CVM to which I want to mount a cloud disk?
Make sure that the CVM instance has not been released and ensure that it is in the same region and availability zone as the cloud disk is in.

### Can I mount a cloud disk to a CVM instance in another availability zone?
No. A cloud disk can only be mounted to or unmounted from a CVM instance in the same availability zone as the cloud disk is in.

### When I unmount a cloud disk (data disk), will its data be lost?
Data in cloud disks will not be modified during mounting or unmounting. To ensure data consistency, we recommend that you follow the steps below:
- In Windows, we recommend that you stop all read and write operations on all file systems of the cloud disk to ensure data integrity. Otherwise, the data that has not finished being read or written will be lost.
- In Linux, log in to the CVM instance and run the `umount` command on the cloud disk. After the command is executed, log in to the CVM Console to unmount the cloud disk.

### How do I unmount a cloud disk?
For more information, see [Unmounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32400).

### Can cloud disks be mounted and unmounted?
- Cloud disks can be mounted and unmounted.
- System disks cannot be mounted or unmounted.

### Can cloud disks be mounted and unmounted in batches?
- Cloud disks can be mounted and unmounted in batches.
- System disks cannot be mounted or unmounted.

### Can system disks be unmounted?
No.


