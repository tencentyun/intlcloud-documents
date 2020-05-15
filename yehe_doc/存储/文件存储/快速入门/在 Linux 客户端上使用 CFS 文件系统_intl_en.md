## Overview
This document describes how to use CFS file systems on Linux clients.




## Step 1. Create a File System and Mount Target

For detailed directions, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


## Step 2. Connect to an Instance
This section describes how to log in to a Linux-based CVM instance. Login method varies by scenario. This section shows how to log in to the instance through the console. For more information on other login methods, please see [Logging in to a Linux-based Instance](/doc/product/213/5436).

#### Prerequisites
You need to use an admin account ID and the corresponding password to log in to the CVM instance.
 - Admin account ID: it is `root` for all Linux-based instances (`ubuntu` on Ubuntu).
 - Password: the password is the one you specified when purchasing the CVM instance.

#### Logging in to a CVM instance in the console
- In the "Operation" column of an instance in the [CVM instance](https://console.cloud.tencent.com/cvm/index) list, click **Log In** to connect to the Linux CVM instance through VNC.
- Enter the account ID and its password to log in.

>This instance is exclusive, i.e., only one user can log in through the console at a time.


#### Verifying network communication
Before mounting, you need to confirm the network connectivity between the client and the file system. You can use the `telnet` command for verification. The specific protocols and open ports for clients are as follows:

File System Protocol | Open Port for Client | Check Network Connectivity
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 | telnet 111 or 892 or 2049
NFS 4.0 | 2049 |  telnet 2049
CIFS/SMB | 445 |  telnet 445 

>CFS does not support `ping` currently.


## Step 3. Mount a File System

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
sudo mount -t nfs -o vers=4.0 <mount point IP>:/ <target mount directory>
```

- Mount point IP: it is automatically generated when the file system is created.
- By default, NFS v4 is mounted under the root directory `/` of the file system. If a subdirectory is created in the file system, it can be mounted to.
- Target mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<mount point IP>:/` and `<target mount directory>`.


Example:
- Mount to the root directory of CFS:
```shell
sudo mount -t nfs -o vers=4.0 10.0.24.4:/ /localfolder
```
- Mount to the subdirectory of CFS:
```shell
sudo mount -t nfs -o vers=4.0 10.0.24.4:/subfolder /localfolder 
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

## Step 4. Unmount a Shared Directory
In case you need to unmount a shared directory, use the following command where "directory name" is the root directory or the full path of the file system.
```shell
umount <directory name>
```

Example: 
```shell
umount /local/test
```

>You are strongly recommended to unmount the file system before restarting or shutting down the client so as to avoid any system exceptions.

## Step 5. Terminate a Resource

>Resources cannot be recovered from a deleted file system, so we recommend that you back up them first before the deletion.

You can terminate a file system in the console. Specifically, go to the [CFS Console](https://console.cloud.tencent.com/cfs), select the file system to be terminated, and click **Delete** > **OK**.


