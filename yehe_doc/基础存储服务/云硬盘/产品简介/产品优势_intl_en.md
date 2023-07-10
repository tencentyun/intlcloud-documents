## Reliable
Cloud disks use a three-copy distribution mechanism, and the system ensures that data is written in three copies before returning a response of "written successfully". If any of the copies fail, the backend data replication mechanism can quickly replicate a new copy by using methods such as data migration, ensuring the availability of three data copies at all times to provide you with a secure storage service. Data is stored across racks, and reliability reaches up to 99.9999999%.

## Elastic

You can configure the storage capacity freely, and expand the capacity on demand without business interruption.
The maximum capacity of cloud disks is 32 TB. A single CVM can attach up to 20 elastic cloud disks as data disks, to efficiently handle TB/PB-level big data processing scenarios and meet the requirements of large-capacity file systems for big data, data warehouse, log processing and other businesses.

## High Performance

Premium Cloud Disk uses a cache mechanism to satisfy the normal business requirements of users. SSD uses NVMe standards and can provide 26,000 random read-write Input/Output Operations per Second (IOPS) on a single disk. This is suitable for scenarios with high requirements for I/O capability.
				
## Easy-to-Use
You can easily manage and use your cloud disks through simple operations such as creation, attaching, detaching, and deletion, reducing both costs and business deployment time.

## Snapshot Backup
You can create a snapshot of the cloud disk to back up data at any time, and you can also quickly create a cloud disk by using a snapshot file, achieving rapid business deployment.
