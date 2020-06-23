When configuring an instance, you can choose a local disk or cloud disk as your system disk or data disk. Before this, you need to get familiar with the characteristics and use cases of [Local Storage](https://intl.cloud.tencent.com/document/product/213/5798) and [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953).
> 
> - The types of system disk and data disk on the purchase page vary by the instance you select. For example, SSD local disk is only available for IO instances.
> - You cannot upgrade the hardware (CPU, memory, or storage) of a CVM instance with local disks. You can only upgrade its bandwidth.
> - The media type of system disks cannot be changed after purchase.
> 

The following table lists the differences and use cases of storage media including SATA HDD local disk, NVME SSD disk, Premium Cloud Storage, and SSD.

| Storage Media | Strengths | Use Cases |
|---------|---------|---------|
| NVME SSD local disks (only available for IO instances including IT3 and IT5) | Low latency: provides a latency low to microsecond. | **Acts as temporary read cache**: NVME SSD excels in random read performance (4 KB/8 KB/16 KB random read) and is suitable for read-only slaves for relational databases including MySQL and Oracle.<br>Since the cost for using memories is still higher than using SSDs, NVME SSD local disk can also be used as the secondary cache of Redis, Memcache, and other cache business.<br>**Note:** NVME SSD has a risk of single point of failures. We recommend implementing data redundancy at the application layer to ensure reliability, and using SSD cloud disk for your core business. |
| SATA HDD local disk (only available for big data instances including D2) | <ul style="margin: 0;"><li>Provides the same data persistence as SSD at a fraction of the cost. It can be used as cold data backup and archive for important business, with a maximum capacity of 16 TB for a single disk.</li><li>High throughout: provides the same throughout as local HDDs.</li></ul> | It is suitable for **scenarios that involve sequential reading and writing of large files**, such as EMR. |
| Premium Cloud Storage | It is the most cost-effective option that applies to 90% of I/O scenarios. | It is suitable for **medium to small sized databases, web servers** and many more scenarios, and provides consistent I/O performance.<br>It meets the I/O demands for testing core business and developing joint testing environments. |
| SSD | High performance and high data reliability: SSD uses best-in-class NVMe solid state storage as the disk media. It is suitable for I/O-intensive business and provides long-term and ultra-excellent single disk performance. | Applicable use cases: <ul style="margin: 0;"><li>**Medium and large databases**: Supports medium and large relational database applications containing tables with millions of rows, such as MySQL, Oracle, and SQL Server.</li><li>**Core business systems**: Supports I/O-intensive applications and other core business systems with high data reliability requirements.</li><li>**Big data analysis**: Supports distributed processing of TB/PB-level data for applications including data analysis, data mining, and business intelligence.</li></ul> |

- For more information about type and use case of cloud disks, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/213/33000).
- For more information about price of cloud disks, see [Pricing List](https://intl.cloud.tencent.com/document/product/213/2255).
