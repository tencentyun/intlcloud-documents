## Overview
This document describes how to use CFS file systems on Linux clients.

## Directions
The steps to use a CFS file system are as follows: [create a file system and mount point](#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.8F.8A.E6.8C.82.E8.BD.BD.E7.82.B9) > [connect to a CVM instance](#.E8.BF.9E.E6.8E.A5.E5.AE.9E.E4.BE.8B) > [mount the file system](#.E6.8C.82.E8.BD.BD.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F) > [unmount a shared file system](#.E5.8D.B8.E8.BD.BD.E5.85.B1.E4.BA.AB.E7.9B.AE.E5.BD.95) > [terminate resources](#.E7.BB.88.E6.AD.A2.E8.B5.84.E6.BA.90). For specific directions, please see the sections below.


### Creating a file system and mount point

#### 1. Enter the file system page

Log in to the [CFS Console](https://console.cloud.tencent.com/cfs) and click **File System** on the left sidebar to enter the file system list page.

#### 2. Create a file system and mount point

Click **Create** and configure the following information in the pop-up window. After confirming that everything is correct, click **OK**.

<table>
  <tr>
    <th>Field</th>
    <th>Meaning</th>
  </tr>
  <tr>
    <td>Region</td>
    <td>Select the region where the CFS file system is to be created.</td>
  </tr>
  <tr>
    <td>AZ</td>
    <td>Select the AZ where the CFS file system is to be created.</td>
  </tr>
  <tr>
    <td>File service protocol</td>
    <td>Select the protocol type for the file system, which can be NFS or CIFS/SMB. Among them, NFS is more suitable for Linux/Unix clients, while CIFS/SMB is more suitable for Windows clients. The beta test for CIFS/SMB file systems has ended, and the schedule for future tests will be announced later. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/582/9553">Notes on CIFS/SMB Beta Test</a>.</td>
  </tr>
  <tr>
    <td>Client type</td>
    <td>Select the type of the client that needs to access the CFS file system, which can be a CVM instance (including TKE/BatchCompute) or a CPM instance. As the two types of instances are in different networks, the system will assign the file system to the specified network according to your client type.</td>
  </tr>
  <tr>
    <td>Network type</td>
    <td> 
VPC or basic network. Please create and mount the file system according to the network type in which your CVM instance resides; otherwise, access may fail as network interconnection is unavailable.
    <li>To allow a file system to be shared by CVM instances in the same VPC, you need to select VPC when creating the file system. If a file system resides in a VPC, only CVM instances in the same VPC can be mounted if no specific network settings are made.</li>
    <li>To allow a file system to be shared by CVM instances in the basic network, you need to select basic network when creating the file system. If a file system resides in the basic network, only CVM instances in the basic network can be mounted if no specific network settings are made.</li>
    <li>If a file system needs to be shared across multiple networks, please see <a href="https://intl.cloud.tencent.com/document/product/582/9764">Cross-network Access to File System</a>.</li>
    </td>
  </tr>  
  <tr>
    <td>Permission group</td>
    <td>Each file system must be bound to a permission group, which specifies the access whitelist and read/write permissions.
    </td>
  </tr>
</table>

#### 3. Get the mount point information

Get the mount point information. After the file system and mount point are created, click the instance ID to enter the file system details page and click **Mount Point Info** to get the mount command for the file system on a Linux client. Please use the recommended mount command to perform the mount operation.
**Quantity** refers to the number of mounted sources, i.e., the number of ways of mounting. Currently, only mounting via IP is supported, so this value is 1.



### Connecting to an instance
This section describes how to log in to a Linux-based CVM instance. Login method varies by scenario. This section shows how to log in to the instance through the console. For more information on other login methods, please see [Logging in to a Linux-based Instance](https://intl.cloud.tencent.com/document/product/213/5436).

#### Prerequisites
You need to use an admin account ID and the corresponding password to log in to the CVM instance.
 - Admin account ID: it is `root` for all Linux-based instances (`ubuntu` on Ubuntu).
 - Password: the password is the one you specified when purchasing the CVM instance.

#### Logging in to a CVM instance in the console
- In the "Operation" column of the CVM instance list, click **Log in** to connect to the Linux-based CVM instance via VNC.
- Enter the account ID `root` (or `ubuntu` on Ubuntu) and its password to log in.

>This instance is exclusive, i.e., only one user can log in through the console at a time.


#### Verifying network communication
Before mounting, you need to confirm the network connectivity between the client and the file system. You can use the `telnet` command for verification. The specific protocols and open ports for clients are as follows:

File System Protocol | Open Port for Client | Check Network Connectivity
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 | telnet 111 or 892 or 2049
NFS 4.0 | 2049 |  telnet 2049
CIFS/SMB | 445 |  telnet 445 

>CFS does not support `ping` currently.


### Mounting a file system

#### Mounting an NFS file system

#### 1. Launch the NFS client
Before mounting, please make sure that `nfs-utils` or `nfs-common` has already been installed in the system. The installation method is as follows:
- CentOS:
```shell
sudo yum install nfs-utils
```
- Ubuntu or Debian:
```shell
sudo apt-get install nfs-common
```

#### 2. Create a target mount directory
Create a target mount directory with the following command.
```shell
mkdir <target mount directory>
```
Example:
```shell
mkdir /local/
mkdir /local/test
```

#### 3. Mount the file system
**Mount NFS v4.0**
Mount NFS v4.0 with the following command:
```shell
sudo mount -t nfs -o vers=4 <mount point IP>:/ <target mount directory>
```

- Mount point IP: it is automatically generated when the file system is created.
- By default, NFS v4 is mounted under the root directory `/` of the file system. If a subdirectory is created in the file system, it can be mounted to.
- Target mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<mount point IP>:/` and `<target mount directory>`.


Example:
- Mount to the root directory of CFS:
```shell
sudo mount -t nfs -o vers=4 10.0.24.4:/ /localfolder
```
- Mount to the subdirectory of CFS:
```shell
sudo mount -t nfs -o vers=4 10.0.24.4:/subfolder /localfolder 
```

**Mount NFS v3.0**
Mount NFS v3.0 with the following command:
```shell
sudo mount -t nfs -o vers=3,nolock,proto=tcp <mount point IP>:/<fsid> <target mount directory>
```
- Mount point IP: it is automatically generated when the file system is created.
- NFS v3.0 can only be mounted to a subdirectory. The default file system subdirectory is FSID.
- Target mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<mount point IP>:/<FSID>` and `<target mount directory>`.

Below is an example of mounting to a CFS subdirectory:
```shell
sudo mount -t nfs -o vers=3,nolock,proto=tcp 10.0.24.4:/z3r6k95r /localfolder 
```

#### 4. View the mount point information
After the mount is completed, run the following command to view the mounted file system:
```shell
mount -l
```
You can also run the following command to view the capacity information of the file system:
```shell
df -h
```


#### Mounting a CIFS/SMB file system
>CIFS/SMB file systems are in beta test. For more information, please see [Notes on CIFS/SMB Beta Test](https://intl.cloud.tencent.com/document/product/582/9553).

#### 1. Launch a CIFS client
Before mounting, please make sure that `cifs-utils` has already been installed in the system. The installation method is as follows:
CentOS:
```shell
sudo yum install cifs-utils.x86_64 –y
```

#### 2. Create a target mount directory
Create a target mount directory with the following command.
```shell
mkdir <target mount directory>
```
Example:
```shell
mkdir /local/
mkdir /local/test
```

#### 3. Mount the file system
Mount CIFS with the following command:
```shell
mount -t cifs -o guest //<mount point IP>/<FSID> /<target mount directory>
```
- Mount point IP: it is automatically generated when the file system is created.
- By default, FSID of the file system is used for mount. 
- Target mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<FSID>/` and `<target mount directory>`.

Example:
```shell
mount -t cifs -o guest //10.66.168.75/vj3i1135  /local/test
```

#### 4. View the mount point information
After the mount is completed, run the following command to view the mounted file system:
```shell
mount -l
```
You can also run the following command to view the capacity information of the file system:
```shell
df -h
```

### Unmounting a Shared Directory
In case you need to unmount a shared directory, use the following command where "directory name" is the root directory or the full path of the file system.
```shell
umount <directory name>
```

Example: 
```shell
umount /local/test
```

>You are strongly recommended to unmount the file system before restarting or shutting down the client so as to avoid any system exceptions.

### Terminating a resource
You can terminate a file system in the console. Specifically, go to the [CFS Console](https://console.cloud.tencent.com/cfs), select the file system to be terminated, and click **Delete** > **OK**.


