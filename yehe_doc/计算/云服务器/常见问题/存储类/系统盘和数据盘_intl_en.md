### What is the default capacity of a CVM system disk?

The system disk of a new CVM has 50 GB free space by default.

### Can I change the local system disk of a CVM to a cloud disk?

- When purchasing a CVM instance,
you can select the desired disk type for the CVM system disk.
- For a purchased CVM instance,
if the availability zone where the purchased CVM is located has available cloud disks, you can use the [change disk media type](https://intl.cloud.tencent.com/document/product/213/32365) feature to change the local system disk to a cloud disk.

### Which regions and availability zones support expanding the system disk capacity to more than 50 GB?

If the system disk is a cloud disk, the system disk capacity can be adjusted to more than 50 GB in all regions that support snapshots.

### Can I expand the system disk capacity of a CVM when reinstalling the operating system?

It depends on the system disk type.
**If the system disk is a cloud disk,**
  the system disk capacity can be increased but cannot be decreased.
**If the system disk is a local disk,**
  it depends on the system disk size.
  - If the default system disk capacity of the purchased instance is 50 GB, the system disk cannot be expanded.
  - For instances purchased at an earlier time: if the system disk capacity is 20 GB or less, the system disk can be expanded to 20 GB by default. If the system disk capacity is more than 20 GB, the system disk can be expanded to 50 GB by default.

### How do I expand the capacity of a cloud disk?

If your CVM uses a cloud disk, the cloud disk is expandable. For details on how to expand a cloud disk, see [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5747).

### Can I increase the system disk capacity and then reinstall the operating system to decrease the system disk capacity?

The capacity of a system disk cannot be decreased.

### How do I save the data on the CVM instance and then expand the system disk capacity?

To expand the system disk capacity, you can create an image and then use the image to reinstall the operating system.

### What is the system disk capacity if I use an image of less than 50 GB to create or reinstall the CVM?

The image capacity does not affect the system disk capacity. The minimum system disk capacity is 50 GB.

### How can I check the data disk?

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Click **Cloud Block Storage** in the leftside bar to go to the cloud disk management page.
3. Click the **Attribute** column, select **Data Disk**, and click **OK**. Then, you can view all data disks in relevant regions.

### How do I read data from and write data to the original NTFS data disk after the operating system is changed from Windows to Linux?

A Windows file system normally adopts the NTFS or FAT32 format, whereas a Linux file system usually adopts the EXT series format. When the operating system of a CVM is changed from Windows to Linux, the data disk format remains unchanged. As a result, the operating system may be unable to access the file system of the data disk. If this is the case, you need to use a format converter to read data from the data disk. For details, see [Reading or Writing NTFS Data Disks After Changing a Windows CVM to a Linux CVM](https://intl.cloud.tencent.com/document/product/213/3857).

### How do I read data from the original EXT data disk after the operating system is changed from Linux to Windows?

A Windows file system normally adopts the NTFS or FAT32 format, whereas a Linux file system usually adopts the EXT series format. When the operating system of a CVM is changed from Linux to Windows, the data disk format remains unchanged. As a result, the operating system may be unable to access the file system of the data disk. If this is the case, you need to use a format converter to read data from the data disk. For details, see [Reading or Writing EXT Data Disks After Changing a Linux CVM to a Windows CVM](https://intl.cloud.tencent.com/document/product/213/3856).
