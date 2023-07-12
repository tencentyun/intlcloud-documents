### What operating systems are supported by CFS?
You can use CFS over the Tencent Cloud private network (e.g., Linux, Unix or Windows CVM, TKE, SCF, BatchCompute, and BMS instances). Customer IDCs and compute nodes of other vendors can also access CFS via VPN, Direct Connect, or CCN ([click here for more information](https://intl.cloud.tencent.com/document/product/215/35504)).

### How is CFS billed?
CFS is billed hourly based on the peak storage usage for the hour.

### Why would my CFS bill includes fees for Guangzhou region while I have never used any resource in the Guangzhou region?
As storage usage in the Chinese mainland is billed in a consolidated manner, the billing zone displayed in CFS bills is "South China (Guangzhou)". The specific regions are shown in the extended fields.



### Which access protocols are supported by CFS?
NFS v3.0/v4.0 and CIFS/SMB2.0/SMB2.5/SMB3.0 are supported.

As clients on Windows and Linux 3.10 and its previous kernel version (e.g., CentOS 6.\*) are incompatible with NFS v4.0, they cannot work normally after mount. Please use NFS v3.0 instead.


### What are the common concepts used in CFS?
File system: a file system is a CFS instance. After a file system is mounted to a CVM instance, you can use it in the same way as a local storage system. It can be mounted to a subdirectory.

Mount target: a mount target is an entry for the compute node to access CFS. It defines the type of network for the node and the permission to access CFS.


### How many file systems can a user create?
Up to 10 file systems can be created in a region by each user. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) if you need to create more.


### How do I ensure data consistency if multiple applications read and write to the same file?
We recommend that you lock a file before an application reads or writes to the file to avoid errors caused by multiple applications modifying the same file simultaneously.


### How fast can I copy/migrate data to CFS?
It depends on the host where the data is originally stored, the storage medium used, network conditions, and the file size. The higher performance the host delivers, the better the storage medium, and the higher the outbound bandwidth, the faster data migration will be. Assume that a host comes with 8 cores and 16 GB memory, and the bandwidth is 1.5 Gbps. The speed of migrating a small file of 4 KB from the host’s local storage to CFS using the migration tool CFS Filetruck will be about 40 KB/s, and that of migrating a large file of 1 TB will be about 140 MB/s. If you copy/migrate primarily small files, we recommend that you use NFS v3 to mount CFS to improve the speed.


### What if a mount target is unavailable?
You can troubleshoot the issue as follows:
- View the error message.
- Check whether `nfs-utils`, `nfs-common`, and `cifs-utils` are installed.
- Check whether the local mount directory exists.
- Check whether the mount target is in the same VPC as the client server and whether they are in the same region.
- Check whether the client server has a security group policy prohibiting access to external ports. For more information on the specific ports, please see [the ports that need to be opened in a file system](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E9.9C.80.E8.A6.81.E5.BC.80.E6.94.BE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.EF.BC.9F).

### What do I do if an error is reported when I use the "vers=4.0" mount command?

As some clients support NFS v4.1 Protocol, the client will first negotiate with the server to try to mount using NFS v4.1 Protocol. In this case, because CFS currently only supports NFS v4.0 Protocol, a NFS4ERR_MINOR_VERS_MIMATCH error may be reported, which will not affect the mount and can be ignored. Once the negotiation fails, the client and server will continue to negotiate the use of NFS v4.0 for the mount.

### What do I do if I installed Windows IIS web server in the Windows Server 2016 OS, but IIS and CIFS are incompatible?
When default security policies are changed in the Windows Server 2016 OS, the following configurations are needed.

1. Modify the registry key for SMB client:
```plaintext
HKEY_LOCAL_MACHINE> SYSTEM> CurrentControlSet> Services> LanmanWorkstation> Parameters> AllowInsecureGuestAuth
```
If the registry key already exists, set it to `1`. Otherwise, right-click to select **New** > **DWORD (32-bit) Value**, and set it to `AllowInsecureGuestAuth` with a value of `1`.
2. Specify a local user for storage access:
Open the Internet Information Services (IIS) Manager, and under the current host:
	1. Select **Sites**>**Default Web Site**, and click **Basic Settings".
	2. In the “Edit Site” dialog box, click **Connect as** to select a specific user.
	3. Click **Set** to set the user name and password.
	4. Click **OK**.



### What if data cannot be written to CFS?
You can troubleshoot the issue as follows:
- View the error message.
- Check the client server’s network condition and run `telnet` to verify whether the port of the mount target is open. For more information on the specific ports, please see [the ports that need to be opened in a file system](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E9.9C.80.E8.A6.81.E5.BC.80.E6.94.BE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.EF.BC.9F). 
- If the file system is not mounted to the mount target's root directory, check whether the corresponding mount target directory exists (in this case, the common error message is `Stale file handle`. You can check whether the subdirectory exists through a device mounted to the root directory).

### Which ports need to be opened for the file system?

File System Protocol | Port | Check Network Connectivity
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 | telnet file system IP 2049
NFS 4.0 | 2049 | telnet file system IP 2049
CIFS/SMB | 445 | telnet file system IP 445 

### What if the configured access permission does not take effect?
For an NFS file system, multiple rules can be configured, which will take effect based on their priorities:
- If the permission of a single IP conflicts with that of an IP within an IP range in the same permission group, the permission with a higher priority will prevail. If their priority levels are the same, the permission of the single IP will prevail.
- If two overlapping IP ranges are configured with different permissions and the same priority levels, the permissions of the overlapping ranges will take effect randomly. Please avoid configuring overlapping IP ranges. 

>!Priority configuration is not supported for CIFS/SMB file systems and will not take effect.

### How can I speed up copying local files to CFS?
For Linux, use the shell script below to accelerate copying local files to CFS. The "number of threads" in the code can be changed as needed.
```bash
threads=<number of threads>; src=<source path/>; dest=<target path/>; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )

<!--Example: threads=24; src=/root/github/swift/; dest=/nfs/; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )-->
```

### What should I do if an exception occurs when renaming a file or directory on Windows?
Due to issues between the client and the supported protocols, renaming a file or directory may fail if a Windows client mounts the file system with NFS. In this case, we recommend using CIFS/SMB for CFS file systems on Windows.


### What if a file system has no write permission on Windows after being mounted with NFS?
Add `AnonymousUid` and `AnonymousGid` to the Registry as described in the operation guide and try again after restarting the system.
For more information, please see [Using CFS File Systems on Windows Clients](https://intl.cloud.tencent.com/document/product/582/11524)

### What if mapped drives cannot be used with Windows IIS?
You can configure the correct NFS client program and modify the Registry (by adding users for access) as instructed in [Using CFS File Systems on Windows Clients](https://intl.cloud.tencent.com/document/product/582/11524).
Restart the client, open the IIS configuration page, add a site, and click **Advanced Settings**.
![](https://main.qcloudimg.com/raw/871a0b585060646f662fa4c8e111df36.png)
In **Advanced Settings**, set **Physical Path** to the CFS mount target.
![](https://main.qcloudimg.com/raw/44777ef4949311c8db84f972b2885af9.png)

### Mounting a CFS file system on Docker or Kubernetes can succeed sometimes but fail at other times. How to solve this problem?

This issue is caused by protocol compatibility. NFS v3 is recommended for mounting CFS with clients such as Docker and Kubernetes. Using NFS v4 may lead to issues with some clients.

### What if I want to use a CFS file system on Window Server 2012 R2 as IIS server directory, but the file system cannot be mounted?

IIS will convert the FSID needed for mounting with NFS v3.0 to uppercase, which prevents the file system from being mounted. We recommend using Windows Server 2016 to avoid this issue.

### How can I continue using CFS in an AZ where CFS resources are sold out?

Assume that there is a CVM instance in Guangzhou Zone 1 that needs to use CFS, but file systems cannot be directly created in Guangzhou Zone 1 as the resources are sold out there.
**In a VPC**
If the CVM instance is in the "Guangzhou Zone 1" subnet of a VPC, you can log in to the [VPC console](https://console.cloud.tencent.com/vpc) to create a subnet whose AZ is "Guangzhou Zone 2" for the VPC.
![](https://main.qcloudimg.com/raw/8fcb0be11627236c99cef6b54d129ac6.png)
![](https://main.qcloudimg.com/raw/261ea1f31f78b0955221cc0f1288285f.png)

After the subnet is successfully created, go back to the CFS console and select this VPC and the subnet you just created to create resources in Guangzhou Zone 2. The CFS file system can be directly mounted to the CVM instance in the subnet of Guangzhou Zone 1 in this VPC.
CIFS/SMB file system user guide:
- [Linux](https://intl.cloud.tencent.com/document/product/582/11523)
- [Windows](https://intl.cloud.tencent.com/document/product/582/11524)

**In the classic network** 
If the CVM instance resides in the classic network, you can create a VPC and a subnet in Guangzhou Zone 2, and then create a file system in this network. With Classiclink, you can connect the classic network and the VPC for access. For more information, please see [Managing Basic Networks](https://intl.cloud.tencent.com/document/product/215/31807).

### The file content update is out of sync. How can I fix this?
#### Symptoms
An NFS file system is mounted on two Linux-based CVM instances. `append` is used to write to a file on CVM instance A, and `tail -f` is used to view changes to the file on CVM instance B. After data is written to the file on CVM instance A, it takes 10-30 seconds for the change to be visible to CVM instance B. However, if you open the file directly on CVM instance B (e.g., using the `vi` command), you can view the change immediately.

#### Cause
This issue is related to the option of the NFS mount command and the implementation of `tail -f`. The following mount command is used:   
```bash
sudo mount -t nfs -o vers=4.0 <mount target IP>:/ <destination mount directory>
```

If CVM instance B mounts the file system with the NFS mount command, the kernel will maintain a metadata cache of the file and directory attributes (e.g., permissions, size, and timestamp) by default. The purpose of caching is to reduce the number of `NFSPROC_GETATTR` remote procedure calls (RPCs).

`tail -f` observes the changes to file attributes (mainly the file size) through `sleep+fstat` and then reads the file and outputs the content. The result of `fstat` determines whether `tail -f` can output the file content in real time. However, due to the metadata cache of file and directory attributes, `fstat` cannot poll real-time file attributes. As a result, although the file on the NFS server has been updated, `tail -f` cannot observe the change, which causes an output delay.

#### Solution
Add the `noac` option when mounting the file system with the mount command to disable the caching of file and directory attributes. The mount command is as follows:
```bash
sudo mount -t nfs -o vers=4 noac <mount target IP>:/ <destination mount directory>
sudo mount -t nfs -o vers=3,noac,nolock,proto=tcp <mount target IP>:/<FSID or subdirectory> <destination mount directory>
```

### What should I do if the error `0x800704C9` occurs when an NFS file system is mounted to a client based on Windows 7 or Windows Server 2008 R2?

#### Cause
The issue occurs because Windows 7-based and Windows Server 2008 R2-based clients cache the original port numbers used to communicate with nlockmgr. For details, see the [Microsoft help documentation](https://support.microsoft.com/en-us/help/2761774/0x800704c9-error-when-you-copy-files-to-an-nfs-server-from-a-windows-7).

#### Solution
Run Windows Update to upgrade the OS to the latest version to fix this issue.

### What do I do if I use the NFS v3 protocol to mount the file system on a Windows client, but an error occurs when I create or modify a file?

#### Cause
The NFS v3 protocol does not support locking. The locking needs to be disabled. Otherwise, files may fail to be modified.

#### Solution
After the file system is mounted, open the command-line tool and enter "mount". If "Locking=yes" is displayed, you can modify the registry to forcibly disable locking.
![](https://main.qcloudimg.com/raw/a5fb998be190e55009ff82a22b520195.png)

#### Directions
1. Find the following registry path: **HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > ClientForNFS > CurrentVersion > User > Default > Mount**.
2. Move the mouse to the right pane and right-click there. Click **New** and choose **DWORD (64-bit) Value** from the drop-down menu. Then, change the name to **Locking** and set the value to `0`.
