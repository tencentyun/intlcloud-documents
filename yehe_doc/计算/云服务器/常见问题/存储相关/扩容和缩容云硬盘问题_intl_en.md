### How do I expand the capacity of a cloud disk?
If your CVM uses a cloud disk, you can expand the disk capacity. For more information on how to expand the disk capacity, see [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5747).

### Can I reduce the capacity of a cloud disk?
No. If you want to reduce the capacity of a cloud disk you purchased, we recommend that you create a cloud disk of your desired capacity and mount it to the same instance that the original cloud disk is mounted to. Then, copy the data stored in the original disk to the new disk and release the original disk.

### How do I expand a system disk?
For data security reasons, a CVM system disk cannot be expanded directly on the Console. You must [reinstall the operating system of the instance](https://intl.cloud.tencent.com/document/product/213/4933) to expand the capacity of its system disk.


### Can the system disks of all types of cloud disks be expanded?
Yes. The system disks of all types of cloud disks, including SSD, Premium Cloud Storage, and HDD, can be expanded.

### Can the system disks of pay-as-you-go CVM instances be expanded?
Yes. The system disks of pay-as-you-go CVM instances can be expanded.

### What is the capacity range of the system disk? What is its maximum capacity?
The expanded system disk’s capacity must be greater than its existing capacity but less than or equal to 500 GB.



