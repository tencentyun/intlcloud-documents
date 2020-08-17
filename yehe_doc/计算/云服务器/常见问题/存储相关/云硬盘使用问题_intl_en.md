### How can I view the data disk?
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
2. Click **Cloud Block Storage** in the left sidebar to access the Cloud Block Storage management page.
3. Click the **Attribute** column, select **Data disk** and click **OK** to view all data disks in the region.

### How do I read data from and write data to the original NTFS data disk after the operating system is changed from Windows to Linux?
Windows employs two major file systems, NTFS or FAT32, while EXT is the file system for Linux. When an operating system is changed from Windows to Linux after reinstallation, the data disk remains in its original format. Therefore, the system might be unable to access data disk’s file system. In these cases, you will need to use a format converter to read the data disk. For details, see [Reading/Writing NTFS Data Disks after Reinstalling a Windows CVM to Linux CVM](https://intl.cloud.tencent.com/document/product/213/3857).

### How do I read data from the original EXT data disk after the operating system is changed from Linux to Windows?
Windows employs two major file systems, NTFS or FAT32, while EXT is the file system for Linux. When an operating system is changed from Linux to Windows after reinstallation, the data disk remains in its original format. Therefore, the system might be unable to access data disk’s file system. In these cases, you will need to use a format converter to read the data disk. For details, see [Reading/Writing EXT Data Disks after Reinstalling a Linux CVM to Windows CVM](https://intl.cloud.tencent.com/document/product/213/3856).

### What are the similarities and differences among Premium Cloud Storage, SDD and enhanced SSD.

- HDD cloud disk: Tencent Cloud HDD cloud disk is a previous generation. It is suitable for use cases with low I/O load and infrequent access.
- Premium Cloud Storage: Tencent Cloud Premium Cloud Storage is a hybrid storage type. It adopts the Cache mechanism to provide a high-performance SSD-like storage, and employs a three-copy distributed mechanism to ensure data reliability. Premium Cloud Storage is suitable for small and medium applications with high requirements for data reliability and standard requirements for performance.
- SSD: SSD uses NVMe SSD as the storage media, and employs a three-copy distributed mechanism. It provides high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for applications with high requirements for I/O performance.
- Enhanced SSD: Enhanced SSD is provided with the the latest storage engine design, NVMe SSD storage media and latest network infrastructure. It employs a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for I/O-intensive applications with high requirements for I/O performance such as large databases and NoSQL.


Pricing of the three cloud disks varies with region. You can choose the right cloud disk based on your application requirements and budget. For pricing details, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
For more information about the type and performance of cloud disks, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).

### How do I test the disk performance?
We recommend using FIO to perform stress test and verification on cloud disks. For more information about the directions, see [Measuring Cloud Disk Performance](https://intl.cloud.tencent.com/document/product/362/6741).

### What are the most common operations with cloud disks?
For common operations with cloud disks, see [Operation Overview](https://intl.cloud.tencent.com/document/product/362/33140).

### How do I check the used space and remaining space of cloud disks?
You can check the used space and remaining space of cloud disks on the associated CVM instance.

### Why is the cloud disk I separately created released together with my instance?
When mounting a cloud disk, you can set its automatic release with the instance. This can be done via the [CBS Console] (https://console.cloud.tencent.com/cvm/cbs/index) or [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659) API.

### How do I partition and format the cloud disks mount?
For more information, see [Initializing Cloud Disks (Smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing Cloud Disks (Larger than 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).




