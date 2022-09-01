### What is the default capacity of a CVM system disk?
Currently, a new CVM system disk has a default capacity of 50 GB.

### Can I change a CVM system disk from a local disk to a cloud disk?
- When purchasing a CVM instance,
you can select the desired disk type for the CVM system disk.
- After purchasing a CVM instance
if there are available cloud disks in the availability zone where the purchased CVM resides, you can use the [change disk media type](https://intl.cloud.tencent.com/document/product/213/32365) feature to change the local system disk to a cloud disk.

### Which regions and availability zones support expanding the system disk capacity to more than 50 GB?
If the system disk is a cloud disk, the system disk capacity can be adjusted to more than 50 GB in all regions that support snapshots.

### Can I expand the system disk capacity of a CVM instance when reinstalling the operating system?
It depends on the system disk type.
- **If the system disk is a cloud disk,**
 the system disk capacity cannot be expanded.
- **If the system disk is a local disk,**
  it depends on the system disk size.
  - If the default system disk capacity of the purchased instance is 50 GB, the system disk cannot be expanded.
  - For instances purchased at an earlier time: if the system disk capacity is 20 GB or less, the system disk can be expanded to 20 GB by default. If the system disk capacity is more than 20 GB, the system disk can be expanded to 50 GB by default.

### Can I reinstall the operating system to reduce the system disk capacity after the expansion?
The capacity of a system disk cannot be reduced.

### How do I save the data on the CVM instance and then expand the system disk capacity?
For detailed directions, see [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/213/32377).

### What is the system disk capacity if I use an image of less than 50 GB to create or reinstall the CVM?
The image capacity does not affect the system disk capacity. The minimum system disk capacity is 50 GB.

### Does the CVM system disk support partitioning?

Yes, but we recommend you not partition a system disk.
If you partition the system disk with a third-party tool, system crash or data loss may occur. You can perform partitioning after expanding the system disk capacity.
