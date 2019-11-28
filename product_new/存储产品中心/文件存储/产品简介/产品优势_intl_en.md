## Features

### CFS Features

#### Integrated management

- CFS provides a standard POSIX and file system access syntax (such as strong data consistency and file locking). You can mount CFS to Tencent Cloud CVM instances using mount commands for standard operating systems and NFS v3.0/v4.0 protocol.
- The CFS console allows you to quickly create and configure file systems while minimizing the workload of deploying and maintaining the file system.

#### Automatic expansion

- CFS can automatically expand the storage capacity of the file system based on file size without interrupting requests and applications. It ensures exclusive storage resources while reducing management workload.


#### Secure and reliable

- CFS is highly available and reliable, and each CFS instance has several redundant copies in multiple availability zones.
- CFS can tightly control access to the file system via POSIX permission, and combine permission groups for access control when using a basic network or VPC.

#### Low cost

- CFS can dynamically adjust the capacity as needed, without early storage provision. You only need to pay by usage and no minimum spend or deployment/OPS cost is required.
- CFS allows CVMs to share the same storage space via the NFS protocol, eliminating the need of purchasing other storage services or considering cache.


### Application scenarios: CFS vs. CBS

Item | CFS | CBS
------- | ------- | -------
Throughput | Single client: 100 MB/s (max. 1.5 GB/s) | Max. 600 MB/s
Shareability | Yes | No
Number of redundant copies | 3 | 3
How to use | Use directly after mounting | Need to install a file system first





