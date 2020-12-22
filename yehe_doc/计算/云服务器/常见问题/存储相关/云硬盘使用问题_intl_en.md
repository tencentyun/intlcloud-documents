### How can I view the data disk?
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Click **Cloud Block Storage** in the left sidebar to access the **Cloud Block Storage** management page.
3. Click the filter icon next to the **Attribute** column title, select **Data disk** and click **OK** to view all data disks in the region.

### How do I read and write the original NTFS data disk after the Windows operating system is reinstalled to Linux?
Windows employs two major file systems, NTFS or FAT32, while EXT is the file system for Linux. When an operating system is changed from Windows to Linux after reinstallation, the data disk remains in its original format. Therefore, the system might be unable to access data disk’s file system. In these cases, you will need to use a format converter to read the data disk. For details, see [Reading/Writing NTFS Data Disks after Reinstalling a Windows CVM to Linux CVM](https://intl.cloud.tencent.com/document/product/213/3857).

### How do I read the data disk in EXT format after the Linux operating system is reinstalled to Windows?
Windows employs two major file systems, NTFS or FAT32, while EXT is the file system for Linux. When an operating system is changed from Linux to Windows after reinstallation, the data disk remains in its original format. Therefore, the system might be unable to access data disk’s file system. In these cases, you will need to use a format converter to read the data disk. For details, see [Reading/Writing EXT Data Disks after Reinstalling a Linux CVM to Windows CVM](https://intl.cloud.tencent.com/document/product/213/3856).

### What are the differences among Premium Cloud Storage, SDD and Enhanced SSD?

- Premium Cloud Storage: Tencent Cloud Premium Cloud Storage is a hybrid storage type. It adopts the Cache mechanism to provide a high-performance SSD-like storage, and employs a three-copy distributed mechanism to ensure data reliability. Premium Cloud Storage is suitable for small and medium applications with high requirements for data reliability and standard requirements for performance.
- SSD: SSD uses NVMe SSD as the storage media, and employs a three-copy distributed mechanism. It provides high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for applications with high requirements for I/O performance.
- Enhanced SSD: Enhanced SSD is based on Tencent Cloud’s latest storage engine, NVMe SSD storage media and the latest network infrastructure. It employs a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for I/O-intensive applications with high requirements for latency, such as large databases and NoSQL.


Pricing of the three types of cloud disks varies with region. You can select the cloud disk that best suits your application requirements and budget. For pricing details, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
For more information on disk types and performance, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).

### How do I test the disk performance?
We recommend using FIO to perform stress test and verification on cloud disks. For instructions, see [Measuring Cloud Disk Performance](https://intl.cloud.tencent.com/document/product/362/6741).

### What are the most common cloud disk operations?
For common cloud disk operations, see [Operation Overview](https://intl.cloud.tencent.com/document/product/362/33140).

### How do I check the available and used space on the cloud disks?
You can log in to the CVM instance to check the available and used space on the cloud disks. This information can also be seen on the CVM console as follows.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index) and access the **Instances** page.
2. Select the ID/Name of the target instance to access the details page.
3. Click on the **Monitoring** tab to view the instance disk usage:
![](https://main.qcloudimg.com/raw/25270ae80b513d497527a0e9f2af1bac.png)

### Why was the cloud disk I separately created released together with my instance?
When mounting a cloud disk, you can decide if it should be released with the instance automatically. This can be configured via the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index) or [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659) API.

### How do I partition and format the a mounted cloud disk?
For more information, see [Initializing Cloud Disks (Smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) or [Initializing Cloud Disks (Larger than 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).




