## Limits and Notes
### Limits

- File system protocols supported by CFS: NFS v3.0/v4.0 and CIFS/SMB (the beta test has ended; the schedule for future tests will be announced later).
- Maximum capacity of a single standard file system: 160 TB (2 PB for a single high-performance file system).
- A single standard file system can be mounted on up to 1,000 compute nodes, and a single high-performance file system on tens of thousands of compute nodes.
- You can have up to 10 file systems (standard/high-performance) in a region.
- Maximum size of a single file: 8 TB.


### Notes
#### UID and GID

- When NFS v3.0 protocol is used, if UID or GID of the file does not exist in the local account, UID and GID will be displayed directly; otherwise, relevant user and group names will be displayed based on the mapping relationship of the local UID and GID.
- When NFS v4.0 protocol is used, if the Linux version is above 3.0, the UID and GID rules are the same as those of the NFS v3.0 protocol; otherwise, the UID and GID of all files will be displayed as `nobody`.

> When you mount a file system to a Linux version below 3.0 by using the NFS v4.0 protocol, you are recommended not to perform "change owner" or "change group" on the file or directory; otherwise, its UID and GID will become `nobody`.


#### Supported CIFS/SMB protocol
- Supported protocol versions: CIFS/SMB 1.0 and above are supported. However, it is not recommended to mount file systems by using SMB 1.0, as it is inferior to SMB 2.0 and higher versions in terms of performance and features. Another reason is that Windows has stopped technical support service for Windows versions supporting SMB 1.0 or below.
- You cannot use NFS and SMB to access the same file system at the same time or directly access an SMB file system via WAN.
- Read/write ACL is provided only at the file system level. No ACL is provided at the file/directory level.
- IOCTL/FSCTL operations such as sparse files setting, file compression, ENI status query, and reparse point setting are not supported.
- Alternate Data Streams is not supported.
- Some protocol features in SMB 3.0 or above are not supported, such as SMB Direct, SMB Multichannel, SMB Directory Leasing, and Persistent File Handle.
 <!--
 * Attributes not supported by NFS v4.0 include FATTR4_MIMETYPE, FATTR4_QUOTA_AVAIL_HARD, FATTR4_QUOTA_AVAIL_SOFT, FATTR4_QUOTA_USED, FATTR4_TIME_BACKUP, and FATTR4_TIME_CREATE. If these attributes are attempted, an `NFS4ERR_ATTRNOTSUPP` error will be displayed on the client.
 * OPs not supported by NFS v4.0 include OP_DELEGPURGE, OP_DELEGRETURN, and NFS4_OP_OPENATTR. If these OPs are attempted, an `NFS4ERR_NOTSUPP` error will be displayed on the client.
 * Currently, NFS v4 does not support the lock and delegation features.
 -->
