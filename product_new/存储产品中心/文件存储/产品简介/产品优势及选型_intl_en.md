## Benefits

#### Integrated management

- CFS supports POSIX access syntax (such as strong data consistency and file locking). Tencent Cloud's computing resources can be mounted to CFS through the NFS v3.0/v4.0 protocol.
- CFS comes with a console where you can quickly create and configure a file system, reducing the time needed for deployment and the workload of file system maintenance.

#### Automatic scaling

CFS can automatically expand the storage capacity of a file system based on file size without interrupting requests and applications during the process, thereby ensuring exclusive use of storage resources while reducing the time cost and workload of management.


#### Security and reliability

- CFS features an extremely high availability and reliability. Each file stored in a CFS instance has multiple redundant copies in an AZ.
- CFS can strictly control access to file systems, allowing you to implement access control by using the security groups in the basic network or VPCs together with permission groups.

#### Low costs

- CFS can dynamically adjust the capacity as needed, without early storage capacity scheduling required. You only need to pay for what you use with no minimum fees or deployment or OPS fees.
- CFS allows multiple compute nodes to share the same storage capacity via the NFS and CIFS/SMB protocols, eliminating your need to purchase other storage services or care about cache.

  

## Model Selection
#### Application scenarios: CFS vs. CBS

Category | Single CFS File System (Standard) | Single Cloud Disk
------- | ------- | -------
Throughput | Up to 40 GB/s for high-performance CFS<p>Up to 1.2 GB/s for standard CFS</p> | Up to 260 MB/s for SSD cloud disk<p>Up to 150 MB/s for premium cloud disk</p>
IOPS | Up to 60K IOPS for high-performance CFS<p>Up to 4K IOPS for standard CFS</p> | Up to 26K IOPS for SSD cloud disk<p>Up to 6K IOPS for premium cloud disk</p>
Sharing | Shared by tens of thousands of clients with strong data consistency | Shared by dozens of clients with no guarantee for consistency 
Number of redundant copies | 3 | 3
How to use | Usable directly after mount | File system installation required


#### 



