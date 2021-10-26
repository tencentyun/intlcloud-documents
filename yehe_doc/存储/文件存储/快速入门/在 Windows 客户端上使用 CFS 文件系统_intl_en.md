## Overview

This document describes how to use CFS file systems on Windows clients. The example below shows how to do so on Windows Server 2012 R2. The operations are the same on other Windows editions such as Windows Server 2008 and Windows Server 2016.


## Step 1. Create a File System and Mount Target

For detailed directions, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


## Step 2. Connect to an Instance

This section describes how to log in to a Windows-based CVM instance. Login method varies by scenario. This section shows how to log in to the instance through the console. For alternative login methods, please see [Logging in to a Windows Instance Using the RDP File](https://intl.cloud.tencent.com/document/product/213/5435).

#### Prerequisites

You have logged in to the CVM instance with an admin account.

- Admin account ID: `Administrator` for all Windows-based instances.
- Password: the password you specified when purchasing the CVM instance.

#### Logging in to a CVM instance in the console

1. Locate the instance in the [CVM instance](https://console.cloud.tencent.com/cvm/index) list, click **Log In** under **Operation**. Click **Log in Now** under **Alternative login methods** to connect to the Windows CVM instance through VNC.
2. Select **Ctrl-Alt-Delete** in the top-left corner to go to the login page.
3. Enter the account ID `Administrator` and its password to log in.

> !This terminal is exclusive, that is, only one user can log in through the console at a time.

#### Verifying network communication

Before mounting, you need to confirm the network connectivity between the client and the file system (the Telnet service needs to be enabled on Windows clients). You can use the `telnet` command for verification, such as `telnet 192.168.1.1 445`. The specific protocols and open ports for clients are as follows:

| File System Protocol | Ports | Check Network Connectivity |
| ------------ | -------------- | ------------------------- |
| NFS v3.0 | 111, 892, 2049 | telnet 111 or 892 or 2049 |
| NFS 4.0      | 2049           | telnet 2049               |
| CIFS/SMB     | 445            | telnet 445                |


## Step 3. Mount a File System

### Mounting an NFS file system

#### 1. Enable the NFS service

Before mounting, please make sure that the NFS service has been enabled.

Select **Control Panel** > **Programs** > **Turn Windows Features on or off** > **Features** and check **Client for NFS** to enable the NFS client service for Windows.
<img src="https://mc.qcloudimg.com/static/img/4f9d7ac7b877ceffc5bc2b1d7c050a24/image.png" width="80%">

#### 2. Verify whether the NFS service is enabled

Open the Windows command-line tool and run the following command. If NFS information is returned, the NFS client is running properly.
```bash
mount -h
```
<img src="https://mc.qcloudimg.com/static/img/4e4f9db217874ccec91ac1f888c8e451/image.png" width="80%">


#### 3. Add an anonymous user and user group

3.1. Open the Registry
Enter the `regedit` command in the command-line tool and press Enter to open the Registry.
<img src="https://mc.qcloudimg.com/static/img/c9fca9a1b123a5b2dbc69b0ce66d539f/image.png" width="80%">

3.2. Add configuration items `AnonymousUid` and `AnonymousGid.`
Find the following path in the registry and select it. 
```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default
```

Right-click the blank space on the right, click **New**, and select **DWORD (32-bit) Value** or **QWORD (64-bit) Value** (depending on the bit count of your OS) in the menu. At this point, a new record will appear in the list. Change the name field to `AnonymousUid` and use the default value of 0. Add a record named `AnonymousGid` with the default value of 0 too by using this method.
<img src="https://mc.qcloudimg.com/static/img/381cdc3b68fb35be5dcceb2a4c962e33/image.png" width="80%">

Then, the configuration items are successfully added as shown below:
<img src="https://main.qcloudimg.com/raw/9af3f35d4b78a2e17cf2ef44fa6863d7.png" width="80%">

3.3. Restart the system for the configuration to take effect
Close the Registry and then run the commands below in sequence to restart the NFS client service so that the modified Registry can take effect. You can also restart the Windows OS for the modified Registry to take effect.
```
net stop nfsclnt
```
```
net stop nfsrdr
```
```
net start nfsrdr
```
```
net start nfsclnt
```

#### 4. Mount the file system

A file system can be mounted via a graphical interface or command line (CMD).

- Mount via a graphical interface
  a. Open "Map Network Drive"
  Log in to the Windows instance where you need to mount the file system, find "Computer" in the "Start" menu, right-click it, and then click "Map Network Drive" in the menu that appears. 

  ![](https://main.qcloudimg.com/raw/759b315c65db82db3feacd811aa93bdd.png)
  b. Enter the access path
  In the pop-up window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the NFS file system).
  ![](https://main.qcloudimg.com/raw/1527f4e7e72b465abc374c2ccb954830.png)
	<img src="https://main.qcloudimg.com/raw/3de493b63f5687253caf9cf99322b17b.png" width="80%">
	
	c. Check file system permissions
	Check whether the above file system is mounted with root permissions in the following way: open a Windows command-line tool and enter the `mount` command.
	Check whether the UID and GID values are 0. If so, the file system has been mounted with root permissions and can be used. If the UID and GID are -2 or other values, data may not be written properly, and you should repeat the previous steps to ensure that the file system is mounted with root permissions.
	<img src="https://main.qcloudimg.com/raw/3ccc26279bb8d73c16eae43f89fea8c7.png" width="80%">
  

If the Windows command-line tool displays "Locking=yes", to avoid read/write exception (NFS v3 does not support locking), you can modify the Registry by performing the following steps:

(1) Find the following registry path: **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Microsoft** > **ClientForNFS** > **CurrentVersion** > **User** > **Default** > **Mount**.
(2) Move the mouse to the right pane and right-click there. Click **New** and choose **DWORD (32-bit) Value** from the drop-down menu. Then, change the name to **Locking** and set the value to `0`.

d. Verify reads/writes
  After checking the file system, the page goes directly to the file system that has been mounted. You can right-click to create a file to verify reads/writes.

- Mount via CMD
  Enter the following command on the Windows command-line tool to mount the file system. The default subdirectory is `FSID`.
```bash
mount <mount target IP>:/<FSID> <shared directory name>:
```
Example:
```bash
mount 10.10.0.12:/z3r6k95r X:
```
> ! You can go to the **CFS console**, click the file system ID, and choose the **Mount Target Info** tab to obtain the `FSID` mount command.
> 

### Mounting a CIFS/SMB file system

A CIFS/SMB file system can be mounted via a graphical interface or command line.

#### Mounting a file system via a graphical interface

1. Open "Map Network Drive"
   Log in to the Windows instance where you need to mount the file system, find "Computer" in the "Start" menu, right-click it, and then click "Map Network Drive" in the menu that appears. 
   ![](https://main.qcloudimg.com/raw/759b315c65db82db3feacd811aa93bdd.png)
2. Enter the access path
   In the pop-up window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the CIFS/SMB file system).
   ![](https://main.qcloudimg.com/raw/1527f4e7e72b465abc374c2ccb954830.png)
3. Verify read/write
   After checking the file system, the page goes directly to the file system that has been mounted. You can right-click to create a file to verify reads/writes.
	 <img src="https://main.qcloudimg.com/raw/598f69f5f327c1acc663b4a3eed5ba03.png" width="80%">

#### Mounting a file system via command line
Use FSID to mount the file system. The mount command is as follows:
```bash
net use <shared directory name>: \\10.10.11.12\FSID 
```

Example:
```bash
net use X: \\10.10.11.12\fjie120
```

>! You can go to the [CFS console](https://console.cloud.tencent.com/cfs), click the file system ID, and choose the **Mount Target Info** tab to obtain the `FSID` mount command.
>



## Step 4. Unmount the File System
#### Unmounting a shared directory via a graphical interface

To disconnect a mounted file system, simply right-click the disk and click **Disconnect** in the menu that appears.
 <img src="https://main.qcloudimg.com/raw/3c6c6649a6df3513ea2d7436c0ab7cf3.png" width="80%">

#### Unmounting an NFS shared directory via CMD 

If you need to unmount a shared directory, please open the Windows Command Prompt and run the following command, where "directory name" is the root directory or the full path of the file system.
```bash
umount <directory name>:
```

Example:
```bash
umount X:
```

## Step 5. Terminate Resources

>! Resources cannot be recovered from a deleted file system. Therefore, you are advised to back up all resources before deleting the file system.
>

You can terminate a file system in the console. Specifically, go to the [CFS console](https://console.cloud.tencent.com/cfs/fs), locate the file system to be terminated, and click **Delete** > **Confirm**.


