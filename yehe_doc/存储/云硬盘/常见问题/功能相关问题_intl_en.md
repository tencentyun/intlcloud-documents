### What is Tencent Cloud Block Storage?
Tencent Cloud Block Storage (CBS) is a highly available and highly reliable block storage device for CVM instances. It provides a wide variety of disks to meet diversified read/write requirements. For more information on CBS, see [Overview](https://intl.cloud.tencent.com/document/product/362/2345).
We recommend CBS when the data frequently changes and you want to persistently store them at a faster read/write speed. CBS can be attached to any running instance in the same availability zone, enabling you to use an instance's file system and database storage without following the instance lifecycle. For more information on the CBS operations, see [Operation Overview](https://intl.cloud.tencent.com/document/product/362/33140).

### What are the features of Tencent Cloud CBS?
Tencent Cloud CBS provides five types of cloud disks: Premium Cloud Disk, Balanced SSD, SSD, Enhanced SSD, and ulTra SSD. They have the following features:
- Elastic attaching and detaching: Elastic cloud disks can be attached and detached. Up to 20 elastic cloud disks can be attached to a CVM as data disks. 
- Elastic expansion: A single disk supports a maximum capacity of 32 TB. You can scale up the disk at any time.
- Snapshot backup: You can create a snapshot to back up data. This improves data reliability and allows rapid data restoration when necessary. You can also create a cloud disk from the snapshot to accelerate your business deployment.

### What is the difference between COS and CBS?
- [Cloud Object Storage](https://www.tencentcloud.com/document/product/436) is available via Web APIs, and is not restricted by file systems, directory structure, number of files, or storage capacity. The service offers various SDKs and tools for business integration, which can also be used independently from CVM. COS is great when you need to access massive amounts of data but is not ideal for millisecond-level response or random read/write scenarios.
- [Cloud Block Storage](https://www.tencentcloud.com/document/product/362) needs to be used together with CVM and can only be attached and used after the file system is partitioned or formatted. COS and CBS both have distinct performance metrics for different use cases.

### What are the limits on cloud disks?
- A single elastic cloud disk can be scaled up to 32 TB, and cannot be scaled down.
- Elastic cloud disks can only be attached to CVMs within the same availability zone.
- Up to 20 elastic cloud disks can be attached to a single CVM as data disks. You can attach elastic cloud disks to a CVM you are purchasing or a CVM created, as instructed in [Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).
- You can purchase up to 50 elastic cloud disks at one time on the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
- If the monthly subscribed elastic cloud disk is not renewed within 7 days after expiration, the system will unbind the attaching relationship between the cloud disk and CVM, and repossess it to the recycle bin. For more information about repossession, see [Overdue Policy](https://intl.cloud.tencent.com/document/product/362/31625).
<dx-alert infotype="explain" title="">
When you attach a monthly subscribed elastic cloud disk to a monthly subscribed CVM, as instructed in [Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401), the following renewal-related options are available:
 - Unified expiry time with the CVM
 - Enable monthly auto-renewal of the cloud disks
 - Attach directly without enabling auto-renewal
</dx-alert>



### What are the advantages of cloud disks?
Cloud disks offer high reliability, elasticity and performance. They are easy to use and support snapshot backup. For more information, see [Product Strengths](https://intl.cloud.tencent.com/document/product/362/3039).

### Can cloud disks be used as system disks?
No. System disks cannot be attached or detached.

[](id:Q1)
### Can cloud disks be used as data disks?
Yes. All types of local disks and cloud disks can be used as data disks.

### Can cloud disks be attached and detached?
- Cloud disks can be attached and detached when they are used as data disks.
- However, they cannot be attached and detached when they are used as system disks.
