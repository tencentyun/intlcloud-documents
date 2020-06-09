### What is a device name (mount target)?
A device name (mount target) is the location of a cloud disk mounted to the CVM instance on the disk controller bus. The selected device name matches the disk device number in Linux and matches the disk sequence number in the disk manager in Windows.

### Can I mount one cloud disk to multiple CVM instances at the same time?
No, this is not supported currently. You can mount up to 20 cloud disks to the same CVM, but cannot mount the same cloud disk to multiple CVMs. To do so, you need to [Unmount Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32400) from CVM A and then [Mount](https://intl.cloud.tencent.com/document/product/362/32401) it to CVM B.

### Do I need to partition the cloud disk after I purchase and mount it to a CVM instance?
Yes. After you purchase a cloud disk, you must mount it to a CVM instance in the same availability zone, and then initialize it including formatting, partitioning, and creating the file system before using it as a data disk. For more information, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645) and [Initializing Cloud Disks]((https://intl.cloud.tencent.com/document/product/362/31646).

### Why am I unable to find the data disk that I purchased for a Linux instance?
If you purchase a data disk separately, you must partition, format and mount it to an instance, so that you can view and use its storage space. For more information, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645) and [Initializing Cloud Disks]((https://intl.cloud.tencent.com/document/product/362/31646).

### How many cloud disks can be mounted to one CVM instance?
A maximum of 20 data disks can be mounted to one CVM instance.

### Why can’t I find the CVM to which I want to mount a cloud disk?
Check whether the CVM instance has been released. If not, ensure that it is in the same availability zone of the region as the cloud disk.

### Can I mount a cloud disk to a CVM instance in another availability zone?
No. A cloud disk can only be mounted to or unmounted from a CVM instance in the same availability zone as the cloud disk.

### Will I lose data in the cloud disk when I unmount it or a data disk?
Data in cloud disks will not be modified during mounting or unmounting. To ensure data consistency, we recommend that you follow the steps below:
- In Windows, we recommend that you stop all read and write operations on all file systems of the cloud disk to ensure data integrity. Otherwise, the data that is not being read or written will be lost.
- In Linux, log in to the CVM instance and run the `umount` command on the cloud disk. After the command is executed, log in to the CVM console to unmount the disk.

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


