Cloud File Storage (CFS) provides a scalable shared file storage service that can be used with Tencent Cloud services such as CVM. CFS offers standard NFS file system access protocol as well as shared data sources for multiple CVM instances. It supports elastic capacity and performance scaling. Your existing applications can be mounted for use without modification required. As a highly available and reliable distributed file system, CFS is suitable for various scenarios such as big data analysis, media processing, and content management.

CFS operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------|------|------------------------------|
| Adding file system      | cfs  | CreateCfsFileSystem          |
| Creating permission group       | cfs  | CreateCfsPGroup              |
| Creating permission group rule     | cfs  | CreateCfsRule                |
| Deleting file system      | cfs  | DeleteCfsFileSystem          |
| Deleting permission group       | cfs  | DeleteCfsPGroup              |
| Deleting permission group rule     | cfs  | DeleteCfsRule                |
| Deleting mount target       | cfs  | DeleteMountTarget            |
| Querying file system      | cfs  | DescribeCfsFileSystems       |
| Querying permission group list     | cfs  | DescribeCfsPGroups           |
| Querying permission group rule list   | cfs  | DescribeCfsRules             |
| Querying KMS key     | cfs  | DescribeKmsKeys              |
| Querying file system mount target   | cfs  | DescribeMountTargets         |
| Activating CFS     | cfs  | SignUpCfsService             |
| Updating file system name     | cfs  | UpdateCfsFileSystemName      |
| Updating the permission group of file system | cfs  | UpdateCfsFileSystemPGroup    |
| Updating file system space limit  | cfs  | UpdateCfsFileSystemSizeLimit |
| Updating permission group information     | cfs  | UpdateCfsPGroup              |
| Updating permission group rule     | cfs  | UpdateCfsRule                |
