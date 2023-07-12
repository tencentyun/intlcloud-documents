## Overview
This document describes how to use CFS file systems on Linux clients.




## Step 1. Create a File System and Mount Target

For detailed directions, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


## Step 2. Connect to an Instance
This section describes how to log in to a Linux-based CVM instance. Login method varies by scenario. This section shows how to log in to the instance through the console. For alternative login methods, please see [Logging into Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436).

#### Prerequisites
Log in to the CVM instance with an admin account.
 - Admin account ID: `root` for all Linux-based instances (`ubuntu` on Ubuntu).
 - Password: the password you specified when purchasing the CVM instance.

#### Logging in to the CVM instance in the console
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
```plaintext
sudo yum install nfs-utils
```
- Ubuntu or Debian:
```plaintext
sudo apt-get install nfs-common
```

#### 2. Create a destination mount directory
Create a destination mount directory with the following command.
```plaintext
mkdir <target mount directory>
```
 Example:
```plaintext
mkdir /local/
mkdir /local/test
```

#### 3. Mount the file system
**Mount NFS v4.0**
Mount NFS v4.0 with the following command:
```shell
// You can go to the **CFS Console**, click the file system ID and select the **Mount Target Info** tab to get the mount command down below. It's recommended to configure the `norevsport` parameter because it ensures uninterrupted connection between the client and the file system during recovery from a network exception after a new TCP port is used for network reconnection. However, some old versions of file systems do not support the `noresvport` parameter. In this case, please use the mount command just as proposed in the console.
// In addition, some old versions of the Linux kernel require use of "vers=4" instead of "vers=4.0" in the mount command to avoid exceptions.
sudo mount -t nfs -o vers=4.0, noresvport <mount target IP>:/ <destination mount directory>
```

- Mount target IP: it is automatically generated when the file system is created.
- By default, NFS v4 is mounted under the root directory `/` of the file system. It can also be mounted to a subdirectory created in the file system.
- destination mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<mount target IP>:/` and `<destination mount directory>`.


Example:
- Mount to the root directory of CFS:
```plaintext
// You can go to the **CFS Console**, click the file system ID and select the **Mount Target Info** tab to get the mount command down below. It's recommended to configure the `norevsport` parameter because it ensures uninterrupted connection between the client and the file system during recovery from a network exception after a new TCP port is used for network reconnection. However, some old versions of file systems do not support the `noresvport` parameter. In this case, please use the mount command just as proposed in the console.
// In addition, some old versions of the Linux kernel require use of "vers=4" instead of "vers=4.0" in the mount command to avoid exceptions.
sudo mount -t nfs -o vers=4.0，noresvport 10.0.24.4:/ /localfolder
```
- Mount to the subdirectory of CFS:
```plaintext
// You can go to the **CFS Console**, click the file system ID and select the **Mount Target Info** tab to get the mount command down below. It's recommended to configure the `norevsport` parameter because it ensures uninterrupted connection between the client and the file system during recovery from a network exception after a new TCP port is used for network reconnection. However, some old versions of file systems do not support the `noresvport` parameter. In this case, please use the mount command just as proposed in the console.
// In addition, some old versions of the Linux kernel require use of "vers=4" instead of "vers=4.0" in the mount command to avoid exceptions.
sudo mount -t nfs -o vers=4.0，noresvport 10.0.24.4:/subfolder /localfolder 
```

**Mount NFS v3.0**
Mount NFS v3.0 with the following command:
```plaintext
// You can go to the **CFS Console**, click the file system ID and select the **Mount Target Info** tab to get the mount command down below. It's recommended to configure the `norevsport` parameter because it ensures uninterrupted connection between the client and the file system during recovery from a network exception after a new TCP port is used for network reconnection. However, some old versions of file systems do not support the `noresvport` parameter. In this case, please use the mount command just as proposed in the console.
// In addition, some old versions of the Linux kernel require use of "vers=4" instead of "vers=4.0" in the mount command to avoid exceptions.
sudo mount -t nfs -o vers=3,nolock,proto=tcp，noresvport mount target IP>:/<fsid> <destination mount directory>
```
- Mount target IP: it is automatically generated when the file system is created.
- NFS v3.0 can only be mounted to a subdirectory. The default file system subdirectory is FSID.
- destination mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

> There is a space between `<mount target IP>:/<FSID>` and `<destination mount directory>`.

Below is an example of mounting to a CFS subdirectory:
```plaintext
// You can go to the **CFS Console**, click the file system ID and select the **Mount Target Info** tab to get the mount command down below. It's recommended to configure the `norevsport` parameter because it ensures uninterrupted connection between the client and the file system during recovery from a network exception after a new TCP port is used for network reconnection. However, some old versions of file systems do not support the `noresvport` parameter. In this case, please use the mount command just as proposed in the console.
// In addition, some old versions of the Linux kernel require use of "vers=4" instead of "vers=4.0" in the mount command to avoid exceptions.
sudo mount -t nfs -o vers=3,nolock,proto=tcp，noresvport 10.0.24.4:/z3r6k95r /localfolder 
```

#### 4. View the mount target information
After the mount is completed, run the following command to view the mounted file system:
```plaintext
mount -l
```
You may also use the following `df` command to view the capacity information of the file system. Note that there may be small chances that the mount target is not displayed, but actually exists. In this case, check the `mount -l` output to ensure that all mounting information has been listed).
```plaintext
df -h
```

>To avoid subsequent misoperations, unless in special cases, it is strongly recommended not to repeat mounts on the directory where the CFS or any other file system has been mounted.

### Mounting a CIFS/SMB file system
#### 1. Launch a CIFS client
Before mounting, please make sure that `cifs-utils` has already been installed in the system. The installation method is as follows:
CentOS:
```plaintext
sudo yum install cifs-utils.x86_64 –y
```

#### 2. Create a destination mount directory
Create a destination mount directory with the following command.
```plaintext
mkdir <target mount directory>
```
 Example:
```plaintext
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
```plaintext
mount -t cifs -o guest //10.66.168.75/vj3i1135  /local/test
```

#### 4. View the mount target information
After the mount is completed, run the following command to view the mounted file system:
```plaintext
mount -l
```
You may also use the following `df` command to view the capacity information of the file system. Note that there may be small chances that the mount target is not displayed, but actually exists. In this case, check the `mount -l` output to ensure that all mounting information has been listed).
```plaintext
df -h
```


>To avoid subsequent misoperations, unless in special cases, it is strongly recommended not to repeat mounts on the directory where the CFS or any other file system has been mounted.


## Step 4. Unmount a Shared Directory
In case you need to unmount a shared directory, use the following command where "directory name" is the root directory or the full path of the file system.
```plaintext
umount <directory name>
```

 Example: 
```plaintext
umount /local/test
```

>After a `df` command is run, there may be small chances that the mount target is not displayed, but actually exists. In this case, check the `mount -l` output to ensure that all mounting information has been listed). In addition, it is strongly recommended that you unmount the file system before restarting or closing your client to avoid system exceptions.

## Step 5. Terminate a Resource

>Resources cannot be recovered from a deleted file system. We recommend backing up all resources before deleting.

You can terminate a file system in the console. Specifically, go to the [CFS Console](https://console.cloud.tencent.com/cfs), locate the file system to be terminated, and click **Delete** > **Confirm**.


