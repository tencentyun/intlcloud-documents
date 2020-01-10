### Mount Point
Each file system provides a mount point, which can be a target address (i.e., IP address) for access in a VPC or the basic network. You can mount the file system to your local system by specifying the IP address of the mount point.

### Permission Group
A permission group is a whitelist for access control provided by CFS. You can create permission groups and add rules for them to allow CVM instances to access the file system with different permissions.
>Each file system must be bound to a permission group.

### NFS File System  
CFS supports NFS v3.0/v4.0 protocol, which is better applicable to Linux and Unix clients.

### CIFS/SMB File System  
Server Message Block (SMB), developed by Microsoft, is an application-layer communication protocol used for sharing access to files, printers, serial ports, and other resources in a network.
Common Internet File System (CIFS) is the public or open version of SMB. CIFS/SMB file systems can better support access on Windows clients.
>CIFS/SMB file systems are in beta test. For more information, please see [Notes on CIFS/SMB Beta Test](https://intl.cloud.tencent.com/document/product/582/9553).
