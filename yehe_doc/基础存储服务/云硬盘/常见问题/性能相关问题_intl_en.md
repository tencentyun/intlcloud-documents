### How to measure the performance of a cloud disk?
The following metrics are generally used to describe the performance of a storage device:
- IOPS: Read/write count per second. IOPS varies by the underlying drive type of the storage device.
- Throughput: Read/written data volume per second, unit in MB/s.
- Latency: Time elapsed from sending an I/O operation to receiving an acknowledgement (in seconds).

### How to test the disk performance?
We recommend you use FIO to perform pressure testing and verification on the cloud disk. For more information, see [Measuring the performance of cloud disks](https://intl.cloud.tencent.com/document/product/362/6741).

### Does the I/O size of the application read-write affect the IOPS performance?
Yes. For a given resource, the IOPS you get is determined by the I/O size of the read and write operations of the application. Usually, when reading and writing small blocks (for example, I/O size of 256 KB), the IOPS performance of the disk can be fully used.

### Does the I/O size of the application read-write affect the throughput performance?
Yes. For a given resource, the throughput you get is determined by the I/O size of the read and write operations of the application. Usually, when reading and writing large blocks (for example, I/O size of 1MB), the throughput performance of the disk can be fully used.

### Can multiple disks be logically combined into one disk to get better performance?
Yes. You can stripe these multiple cloud disks that are mounted to the CVM to balance I/O load to multiple disks, increasing I/O parallel capacity to implement better performance than a single disk. For more information, see [Building LVM logical volumes from multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).

