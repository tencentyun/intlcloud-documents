## Overview
This document describes how to use CFS file systems on Linux clients.




## Step 1. Create a File System and Mount Target

For detailed directions, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


## Step 2. Connect to an Instance
This section describes how to log in to a Linux-based CVM instance. The login method varies depending on the scenarios. Logging in to the instance through the console is described herein. For alternative login methods, please see [Logging in to Linux Instance Using Standard Login Method](/doc/product/213/5436).

#### Prerequisites
You have logged in to the CVM instance with an admin account.
 - Admin account ID: `root` for all Linux-based instances (`ubuntu` on Ubuntu).
 - Password: the password you specified when purchasing the CVM instance.

#### Logging in to a CVM instance in the console
- Locate the instance in the [CVM instance](https://console.cloud.tencent.com/cvm/index) list, click **Log In** under **Operation**. Click **Log in Now** under **Alternative login methods** to connect to the Linux CVM instance through VNC.
- Enter the account ID and its password to log in.

>?This instance is exclusive, meaning only one user can log in through the console at a time.


#### Verifying network communication
Before mounting, you need to check the network connectivity between the client and the file system. You can use the `telnet` command for verification. The specific protocols and ports as follows:

File System Protocol | Port  | Check Network Connectivity
------- | ------- | ---------
NFS 3.0 | 111, 892,and 2049 | telnet 111,892,and 2049
NFS 4.0 | 2049 |  telnet 2049
CIFS/SMB | 445 |  telnet 445 

>?Currently, CFS does not support `ping`.


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
Create a destination mount directory with the following command:
```plaintext
mkdir <destination mount directory>
```
Example:
```plaintext
mkdir /localfolder/
mkdir /localfolder/test

```

#### 3. Mount the file system
**Mount NFS v4.0**
Mount NFS v4.0 with the following command:
```shell
// You can go to the CFS console > File System > Mount Target Info to obtain the following command. As some old file system versions do not support the noresvport parameter, you are advised to use the version-specific commands provided in the console. After norevsport is configured, a new TCP port can be used for reconnection, which guarantees that the client and file system can stay connected during network recovery. Therefore, the norevsport parameter is recommended.
// Some old versions of Linux kernels need to be mounted using vers=4. If an exception occurs when you use vers=4.0, you can change it to vers=4.
sudo mount -t nfs -o vers=4.0,noresvport <mount target IP>:/ <destination mount directory>
```

- Mount target IP: It is automatically generated when the file system is created.
- By default, NFS v4 is mounted under the root directory `/` of the file system. It can also be mounted to a subdirectory created in the file system.
- Destination mount directory: This refers to the target directory to be mounted to on the current server. It needs to be created in advance.

>!Note that there is a space between `<mount target IP>:/` and `<destination mount directory>`.


Example:
- Mount to the root directory of CFS:
```plaintext
// You can go to the CFS console > File System > Mount Target Info to obtain the following command. As some old file system versions do not support the noresvport parameter, you are advised to use the version-specific commands provided in the console. After norevsport is configured, a new TCP port can be used for reconnection, which guarantees that the client and file system can stay connected during network recovery. Therefore, the norevsport parameter is recommended.
// Some old versions of Linux kernels need to be mounted using vers=4. If an exception occurs when you use vers=4.0, you can change it to vers=4.
sudo mount -t nfs -o vers=4.0,noresvport 10.0.24.4:/ /localfolder
```
- Mount to the subdirectory of CFS:
```plaintext
// You can go to the CFS console > File System > Mount Target Info to obtain the following command. As some old file system versions do not support the noresvport parameter, you are advised to use the version-specific commands provided in the console. After norevsport is configured, a new TCP port can be used for reconnection, which guarantees that the client and file system can stay connected during network recovery. Therefore, the norevsport parameter is recommended.
// Some old versions of Linux kernels need to be mounted using vers=4. If an exception occurs when you use vers=4.0, you can change it to vers=4.
sudo mount -t nfs -o vers=4.0,noresvport 10.0.24.4:/subfolder /localfolder 
```

**Mount NFS v3.0**
Mount NFS v3.0 with the following command:
```plaintext
// You can go to the CFS console > File System > Mount Target Info to obtain the following command. As some old file system versions do not support the noresvport parameter, you are advised to use the version-specific commands provided in the console. After norevsport is configured, a new TCP port can be used for reconnection, which guarantees that the client and file system can stay connected during network recovery. Therefore, the norevsport parameter is recommended.
// Some old versions of Linux kernels need to be mounted using vers=4. If an exception occurs when you use vers=4.0, you can change it to vers=4.
sudo mount -t nfs -o vers=3,nolock,proto=tcp,noresvport <mount target IP>:/<fsid> <destination mount directory>
```
- Mount target IP: It is automatically generated when the file system is created.
- NFS v3.0 can only be mounted to a subdirectory. The default file system subdirectory is FSID.
- Destination mount directory: This refers to the target directory to be mounted to on the current server. It needs to be created in advance.

>! Note that there is a space between `<mount target IP>:/<FSID>` and `<destination mount directory>`.

Below is an example of mounting to a CFS subdirectory:
```plaintext
// You can go to the CFS console > File System > Mount Target Info to obtain the following command. As some old file system versions do not support the noresvport parameter, you are advised to use the version-specific commands provided in the console. After norevsport is configured, a new TCP port can be used for reconnection, which guarantees that the client and file system can stay connected during network recovery. Therefore, the norevsport parameter is recommended.
// Some old versions of Linux kernels need to be mounted using vers=4. If an exception occurs when you use vers=4.0, you can change it to vers=4.
sudo mount -t nfs -o vers=3,nolock,proto=tcp,noresvport 10.0.24.4:/z3r6k95r /localfolder 
```

#### 4. View the mount target information
After the mount is completed, run the following command to view the mounted file system:
```plaintext
mount -l
```
You can also run the following command to view the capacity information about the file system. (After you run the `df` command, note that it is possible that an existing mount target is not displayed. In this case, you can check the output of `mount -l` to ensure that all mount target information is listed.)
```plaintext
df -h
```

>!To avoid misoperations, do not repeatedly mount a mounted CFS file system or file system directory unless it is necessary.

### Mounting a CIFS/SMB file system

#### 1. Launch a CIFS client
Before mounting, please make sure that `cifs-utils` has already been installed in the system. The installation method is as follows:
CentOS:
```plaintext
sudo yum install cifs-utils.x86_64 –y
```

#### 2. Create a destination mount directory
Create a destination mount directory with the following command:
```plaintext
mkdir <destination mount directory>
```
Example:
```plaintext
mkdir /local/
mkdir /local/test
```

#### 3. Mount the file system
Mount CIFS with the following command:
```shell
// Parameter description:
// vers: supports 2.1 and 3.0. Defaults to 1.0.
// uid: owner of the file when the mount is completed. If not specified, uid=0 is used by default.
// gid: user group that owns the file when the mount is completed. If not specified, gid=0 is used by default.
// The uid and gid parameters are for apps that need to check the file owner during execution. In this case, you need to set uid and gid to the app account.
// noperm: The client does not perform permission verification. If a permission is denied, you can add this parameter.
// actimeo: file attribute (metadata timestamps) cached by the client
// nocase: By default, using version 1.0 on mount is case-sensitive. However, Windows clients are case-insensitive. If you create a file on the Linux CIFS client, and the file name already exists on the Windows client, an exception may occur when you access the file through the Windows client.
// An example is as follows:
mount -t cifs -o guest,vers=1.0,uid=1000,gid=100,noperm,actimeo=1,nocase //<mount target IP>/<FSID> /<destination mount directory>
```
- Mount target IP: It is automatically generated when the file system is created.
- By default, FSID of the file system is used for the mount. 
- Destination mount directory: This refers to the target directory to be mounted to on the current server. It needs to be created in advance.

>!Note that there is a space between `<FSID>/` and `<destination mount directory>`.

Example:
```plaintext
mount -t cifs -o guest //10.66.168.75/vj3i1135  /local/test
```

#### 4. View the mount target information
After the mount is completed, run the following command to view the mounted file system:
```plaintext
mount -l
```
You can also run the following command to view the capacity information about the file system. (After you run the `df` command, note that it is possible that an existing mount target is not displayed. In this case, you can check the output of `mount -l` to ensure that all mount target information is listed.)
```plaintext
df -h
```


>!To avoid misoperations, do not repeatedly mount a mounted CFS file system or file system directory unless it is necessary.


## Step 4. Unmount a Shared Directory
If you need to unmount a shared directory, you can run the following command, where "directory name" is the root directory or the full path of the file system:
```plaintext
umount <directory name>
```

Example: 
```plaintext
umount /local/test
```

>!After you run the `df` command, note that it is possible that an existing mount target is not displayed. In this case, you can check the output of `mount -l` to ensure that all mount target information is listed. In addition, you are advised to unmount the file system before restarting/shutting down the client to avoid exceptions.

## Step 5. Terminate Resources

>!Resources cannot be recovered from a deleted file system. Therefore, you are advised to back up all resources before deleting the file system.

You can terminate a file system in the console. Specifically, go to the [CFS console](https://console.cloud.tencent.com/cfs/fs), locate the file system to be terminated, and click **Delete** > **Confirm**.


