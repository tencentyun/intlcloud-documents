
Cloud File Storage (CFS) provides a scalable shared file storage service that can be used with Tencent Cloud services such as CVM, TKE, and BatchCompute. CFS offers standard NFS and CIFS/SMB file system access protocols as well as shared data sources for multiple CVM instances or other computing services. It supports elastic capacity expansion and performance scaling. Your existing applications can be mounted for use without modification. As a highly available and reliable distributed file system, CFS is suitable for various scenarios such as big data analysis, media processing, and content management.

CFS is easy to integrate, eliminating your need to adjust your business structure or make complex configurations. To integrate and use CFS, simply complete three steps: creating a file system, launching a file system client on a server, and mounting the created file system.

## Features
#### Integrated management
CFS supports NFS v3.0/v4.0 and CIFS/SMB2.0/SMB2.5/SMB3.0 protocols as well as POSIX access syntax (such as strong data consistency and file locking). You can mount a file system by running the standard mount command on the corresponding operating system.

#### Automatic expansion
CFS can automatically expand the storage capacity of a file system based on file size without interrupting requests and applications during the process, thereby ensuring exclusive use of storage resources while reducing management workload.

#### Security settings
CFS features extremely high availability and persistence. Each file stored in a CFS instance has 3 redundant copies.
It supports access from VPC and classic network as well as access control.

#### Pay-as-you-go
CFS is billed by actual usage with no minimum fees or deployment or OPS fees. It allows multiple CVM instances to share the same storage capacity via the NFS and CIFS/SMB protocols, eliminating your need to purchase other storage services or care about cache.


