### Which operating systems are supported by CFS?
Linux, Unix, and Windows clients are supported.

### How is CFS billed?
CFS is billed based on actual storage capacity (peak storage capacity per hour).


### Which access protocols are supported by CFS?
NFS v3.0/v4.0 and CIFS/SMB. CIFS/SMB file systems are in beta test. For more information, please see [Notes on CIFS/SMB Beta Test](https://intl.cloud.tencent.com/document/product/582/9553).

As clients on Windows and Linux 3.10 and its previous kernel version (e.g., CentOS 6.\*) are incompatible with NFS v4.0, they cannot work normally after mount. Please use NFS v3.0 instead.

### What concepts are used in CFS?
File system: a file system is a CFS instance. After a file system is mounted to a CVM instance, you can use it in the same way as a local storage system. It can be mounted to a subdirectory.

Mount point: A mount point is an entry for the compute node to access CFS. It defines the type of network for the node and the permission to access CFS.

### How many file systems can be created for each user?
Up to 10 ones can be created in a region for each user. If you have special requirements, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for scaling.

### What if a mount point is unavailable?
You can troubleshoot the problem in the following steps:
- View the error message.
- Check whether `nfs-utils`, `nfs-common`, and `cifs-utils` are installed.
- Check whether the local mount directory exists.
- Check whether the mount point is in the same VPC as the client server and whether they are in the same region.
- Check whether the client server has a security group policy prohibiting access to external ports. For more information on the specific ports, please see [Notes on Open Ports in a File System](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E9.9C.80.E8.A6.81.E5.BC.80.E6.94.BE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.EF.BC.9F).

### What if data cannot be written to CFS?
You can troubleshoot the problem in the following steps:
- View the error message.
- Check whether the network of the client server is normal and run `telnet` to verify whether the port of the mount point is open. For more information on the specific ports, please see [Notes on Open Ports in a File System](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E9.9C.80.E8.A6.81.E5.BC.80.E6.94.BE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.EF.BC.9F). 
- If the file system is not mounted to the mount point's root directory, check whether the corresponding mount point directory exists (the common error message in this case is "Stale file handle". You can check whether the subdirectory exists through a device mounted to the root directory).

### Which ports need to be opened in a file system?

File System Protocol | Open Port | Check Network Connectivity
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 | telnet file system IP 2049
NFS 4.0 | 2049 | telnet file system IP 2049
CIFS/SMB | 445 | telnet file system IP 445 

> CFS does not support `ping` currently.

### What if the configured access permission does not take effect?
For an NFS file system, multiple rules can be configured, which will take effect based on their priorities:
- If the permission of a single IP conflicts with that of an IP within an IP range in the same permission group, the permission with a higher priority will prevail, and if their priority levels are the same, the permission of the single IP will prevail.
- If two IP ranges that have overlaps are configured with different permissions but the same priority levels, the permissions of the overlapping ranges will take effect randomly. Please avoid configuring overlapping IP ranges. 

>Priority configuration is not supported for CIFS/SMB file systems and will not take effect.

### How to speed up copying local files to CFS?
For Linux, use the `shell` script below to accelerate copying local files to CFS. The "number of threads" in the following code can be adjusted as needed.
```
threads=<number of threads>; src=<source path/>; dest=<target path/>; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )

<!--Example: threads=24; src=/root/github/swift/; dest=/nfs/; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )-->
```

### What if an exception occurs when renaming a file or directory on Windows?
Given the client's support for protocols, renaming a file or directory may fail if a Windows client mounts the file system with NFS. In this case, you are recommended to use CIFS/SMB for CFS file systems on Windows.


### What if a file system has no write permission on Windows after being mounted with NFS?
Please strictly follow the operation guide. Add `AnonymousUid` and `AnonymousGid` to the Registry and try again after restarting the system.
For more information, please see [Using CFS File Systems on Windows Clients](https://intl.cloud.tencent.com/document/product/582/11524)

### What if mapped drives cannot be used with Windows IIS?
You can configure the correct NFS client program and modify the Registry (by adding users for access) as instructed in [Using CFS File Systems on Windows Clients](https://intl.cloud.tencent.com/document/product/582/11524).
Restart the client, open the IIS configuration page, add a site, and click **Advanced Settings**.
![](https://main.qcloudimg.com/raw/871a0b585060646f662fa4c8e111df36.png)
Set the "Physical Path" in the "Advanced Settings" to the CFS mount point.
![](https://main.qcloudimg.com/raw/44777ef4949311c8db84f972b2885af9.png)

### Mounting a CFS file system on Docker or Kubernetes can succeed sometimes but fail at other times. How to solve this problem?

This problem is caused by protocol compatibility. NFS v3 is recommended for mounting CFS with clients such as Docker and Kubernetes (using NFS v4 may lead to mounting problems on some clients).

### What if I want to use a CFS file system on Window Server 2012 R2 as IIS server directory, but the file system cannot be mounted?

IIS will convert the FSID needed for mounting with NFS v3.0 to uppercase, leading to the problem that the file system cannot be mounted normally. You are recommended to use Windows Server 2016 to avoid this problem.

### How can I continue using CFS in an AZ where CFS resources are sold out?

For example, assume that there is a CVM instance in Guangzhou Zone 1 that needs to use CFS, but file systems cannot be directly created in Guangzhou Zone 1 as the resources are sold out there.
**In a VPC**
If the CVM instance is in the "Guangzhou Zone 1" subnet of a VPC, you can log in to the [VPC Console](https://console.cloud.tencent.com/vpc) to create a subnet whose AZ is "Guangzhou Zone 2" for the VPC.
![](https://main.qcloudimg.com/raw/8fcb0be11627236c99cef6b54d129ac6.png)
![](https://main.qcloudimg.com/raw/261ea1f31f78b0955221cc0f1288285f.png)

After the subnet is successfully created, go back to the CFS Console and select this VPC and the subnet you just created to create resources in Guangzhou Zone 2. The CFS file system can be directly mounted to the CVM instance in the subnet of Guangzhou Zone 1 in this VPC.
CIFS/SMB file system user guide:
- [Linux](https://intl.cloud.tencent.com/document/product/582/11523)
- [Windows](https://intl.cloud.tencent.com/document/product/582/11524)

**In the basic network** 
If the CVM instance resides in the basic network, you can create a VPC and a subnet in Guangzhou Zone 2 and then create a file system in this network. With Classiclink, you can connect the basic network and the VPC for access.<!-- For more information, please see [Classiclink]().-->

### File content update is out of sync. How can I fix this?
#### Issue
An NFS file system is mounted to two Linux-based CVM instances. Use `append` to write a file to CVM instance A, and use `tail -f` to observe the changes to the file on CVM instance B. After data is written to the file on CVM instance A, it will take 10–30 seconds for the updated content to display on CVM instance B. However, in the same scenario, if you open the file directly on CVM instance B (e.g., using the `vi` command), you can view the update immediately.

#### Cause
This issue is related to the option of the NFS mount command and the implementation of `tail -f`. You can use the following mount command:   
```sh
sudo mount -t nfs -o vers=4 <mount point IP>:/ <target mount directory>
```

If CVM instance B mounts the file system with the NFS mount command, the kernel will maintain a metadata cache of the file and directory attributes (e.g., permissions, size, and timestamp) by default. The purpose of caching is to reduce the number of `NFSPROC_GETATTR` remote procedure calls (RPCs).

`tail -f` observes the changes to file attributes (mainly the file size) through `sleep+fstat` and then reads the file and outputs the content. The result of `fstat` determines whether `tail -f` can output the file content in real time. However, due to the metadata cache of file and directory attributes, `fstat` cannot poll real-time file attributes. As a result, although the file on the NFS server has been updated, `tail -f` cannot observe the change, which causes an output delay.

#### Solution
Add the `noac` option when mounting the file system with the mount command to disable the caching of file and directory attributes. The mount command is as follows:
```sh
sudo mount -t nfs -o vers=4 noac <mount point IP>:/ <target mount directory>
sudo mount -t nfs -o vers=3 noac,nolock,proto=tcp <mount point IP>:/<FSID or subdirectory> <target mount directory>
```

### What if error 0x800704C9 occurs when a file system is mounted with NFS to a client based on Windows 7 or Windows Server 2008 R2?

#### Cause
These clients cache the original port numbers used to communicate with nlockmgr. For the specific cause, please see the help documentation on Microsoft's website [here](https://support.microsoft.com/en-us/help/2761774/0x800704c9-error-when-you-copy-files-to-an-nfs-server-from-a-windows-7).

#### Solution
Turn on the Automatic Updates feature on Windows to upgrade the system to the latest version to fix this problem.
