## Overview
This document describes how to use CFS file systems on Linux clients.




## Step 1. Create a File System and Mount Target

For detailed directions, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


## Step 2. Connect to an Instance
This section describes how to log in to a Linux-based CVM instance. Login method varies by scenario. This section shows how to log in to the instance through the console. For alternative login methods, please see [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).

#### Prerequisites
Log in to the CVM instance with an admin account.
 - Admin account ID: `root` for all Linux-based instances (`ubuntu` on Ubuntu).
 - Password: the password you specified when purchasing the CVM instance.

#### Logging in to a CVM instance in the console
- Locate the instance in the [CVM instance](https://console.cloud.tencent.com/cvm/index) list, click **Log In** under **Operation**. Click **Log in Now** under **Alternative login methods** to connect to the Linux CVM instance through VNC.
- Enter the account ID and its password to log in.

>This instance is exclusive, i.e., only one user can log in through the console at a time.


#### Verifying network communication
Before mounting, you need to check the network connectivity between the client and the file system. You can use the `telnet` command for verification. The specific protocols and ports as follows:

File System Protocol | Port  | Check Network Connectivity
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 | telnet 111 or 892 or 2049
NFS 4.0 | 2049 |  telnet 2049
CIFS/SMB | 445 |  telnet 445 

>CFS currently do not support `ping`.


## Step 3. Mount a File System

### Mounting an NFS file system

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

#### 2. Create a destination mount directory
Create a destination mount directory with the following command.
```shell
mkdir <destination mount directory>
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
sudo mount -t nfs -o vers=4.0 <mount target IP>:/ <destination mount directory>
```

- Mount target IP: it is automatically generated when the file system is created.
- By default, NFS v4 is mounted under the root directory `/` of the file system. It can also be mounted to a subdirectory created in the file system.
- destination mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<mount target IP>:/` and `<destination mount directory>`.


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
sudo mount -t nfs -o vers=3,nolock,proto=tcp <mount target IP>:/<fsid> <destination mount directory>
```
- Mount target IP: it is automatically generated when the file system is created.
- NFS v3.0 can only be mounted to a subdirectory. The default file system subdirectory is FSID.
- destination mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<mount target IP>:/<FSID>` and `<destination mount directory>`.

Below is an example of mounting to a CFS subdirectory:
```shell
sudo mount -t nfs -o vers=3,nolock,proto=tcp 10.0.24.4:/z3r6k95r /localfolder 
```

#### 4. View the mount target information
After the mount is completed, run the following command to view the mounted file system:
```shell
mount -l
```
You can also run the following command to view the capacity information of the file system:
```shell
df -h
```


#### Mounting a CIFS/SMB file system

#### 1. Launch a CIFS client
Before mounting, please make sure that `cifs-utils` has already been installed in the system. The installation method is as follows:
CentOS:
```shell
sudo yum install cifs-utils.x86_64 –y
```

#### 2. Create a destination mount directory
Create a destination mount directory with the following command.
```shell
mkdir <destination mount directory>
```
Example:
```shell
mkdir /local/
mkdir /local/test
```

#### 3. Mount the file system
Mount CIFS with the following command:
```shell
mount -t cifs -o guest //<mount target IP>/<FSID> /<destination mount directory>
```
- Mount target IP: it is automatically generated when the file system is created.
- By default, FSID of the file system is used for mount. 
- destination mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<FSID>/` and `<destination mount directory>`.

Example:
```shell
mount -t cifs -o guest //10.66.168.75/vj3i1135  /local/test
```

#### 4. View the mount target information
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

>We strongly recommend that you unmount the file system before restarting or shutting down the client so as to avoid any system exceptions.

## Step 5. Terminate a Resource

>Resources cannot be recovered from a deleted file system. We recommend backing up all resources before deleting.

You can terminate a file system in the console. Specifically, go to the [CFS Console](https://console.cloud.tencent.com/cfs), locate the file system to be terminated, and click **Delete** > **Confirm**.


