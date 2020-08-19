### What are the features of Tencent Cloud CBS?
Tencent Cloud CBS provides three disk types: Premium Cloud Storage, SSD and Enhanced SSD. The cloud disks have the following features:
- Elastic mounting and unmounting: elastic cloud disks can be mounted and unmounted. Up to 20 elastic cloud disks can be mounted to each CVM to serve as data disks. 
- Elastic expansion: a single disk supports a maximum capacity of 16 TB. You can scale up the disk at any time.
- Snapshot backup: cloud disks enable you to back up data by creating a snapshot. This improves data reliability and allow rapid data restoration when necessary. Cloud disks also enable you to create a new cloud disk based on a snapshot, speeding up your business deployment.

### What limits do cloud disks have?
- A single elastic cloud disk has a maximum capacity of 16 TB. It can be scaled up to 16 TB, but cannot be scaled down.
- Elastic cloud disks can only be mounted to CVMs that are in the same availability zone.
- Up to 20 elastic cloud disks can be mounted to a single CVM. You can add the elastic cloud disks directly when purchasing a CVM or [mount the elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/32401) after purchase.
- You can purchase up to 50 elastic cloud disks at one time on the [CBS console](https://console.cloud.tencent.com/cvm/cbs). 


### What are the differences between different types of cloud disks?
CBS supports the latest three volume types:
- Premium Cloud Storage: suitable for most I/O applications including Web/APP services, logical processing, as well as small and medium sites.
- SSD: suitable for applications including transactional workload, as well as small and medium databases.
- Enhanced SSD: suitable for latency-sensitive or high-performance applications including medium and large databases, NoSQL, and log analysis.

The performance and pricing vary with type. You can choose cloud disks based on your budget and application requirements. For more information on disk types and performance, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).

### What advantages do cloud disks have?
Cloud disks have advantages such as high reliability, elasticity, high performance, ease of use, and snapshot backup. For more information, see [Product Strengths](https://intl.cloud.tencent.com/document/product/362/3039).

### Can elastic cloud disks be used as system disks?
No. System disks cannot be unmounted or mounted.

<span id="Q1"></span>
### Can cloud disks be used as data disks?
All types of local disks and cloud disks can be used as data disks.

### Can cloud disks be mounted and unmounted?
- Elastic cloud disks can be mounted and unmounted.
- System disks cannot be mounted or unmounted.

### Can elastic cloud disks be mounted and unmounted in batches?
- Elastic cloud disks can be mounted and unmounted in batches.
- System disks cannot be mounted or unmounted.
