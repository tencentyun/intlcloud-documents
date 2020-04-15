## Overview

This document describes how to use CFS file systems on Windows clients. The example below shows how to do so on Windows Server 2012 R2. The operations are the same on other Windows editions such as Windows Server 2008 and Windows Server 2016.


## Step 1. Create a file system and mount target

For detailed directions, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


## Step 2. Connect to an instance

This section describes how to log in to a Windows CVM instance. Login method varies by scenario. This section shows how to log in to the instance through the console. For more information on other login methods, please see [Logging in to a Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435).

#### Prerequisites

You need to use an admin account ID and the corresponding password to log in to the CVM instance.

- Admin account ID: it is `Administrator` for all Windows instances.
- Password: the password is the one you specified when purchasing the CVM instance.

#### Logging in to a CVM instance in the console

1. In the "Operation" column of an instance in the [CVM instance](https://console.cloud.tencent.com/cvm/index) list, click **Log In** to connect to the Windows CVM instance through VNC.
2. Select **Ctrl-Alt-Delete** in the top-left corner to go to the login page.
3. Enter the account ID `Administrator` and its password to log in.

>This instance is exclusive, i.e., only one user can log in through the console at a time.

#### Verifying network communication

Before mounting, you need to confirm the network connectivity between the client and the file system (the Telnet service needs to be enabled on Windows clients). You can use a telnet command (such as `telnet 192.168.1.1 445`) for verification. The specific protocols and open ports for clients are as follows:

| File System Protocol | Open Port for Client | Check Network Connectivity |
| ------------ | -------------- | ------------------------- |
| NFS v3.0 | 111, 892, 2049 | telnet 111 or 892 or 2049 |
| NFS v4.0 | 2049 | telnet 2049 |
| CIFS/SMB | 445 | telnet 445 |

>CFS does not support `ping` currently.

## Step 3. Mount the file system

### Mounting an NFS file system

#### 1. Enable the NFS service

Before mounting, please make sure that the NFS service has been turned on.
1.1. Select **Control Panel** > **Programs** > **Turn Windows Features on or off** > **Server Roles** and check **Server for NFS**.
<img src="https://mc.qcloudimg.com/static/img/eaeed922e9d1f673e47137d80a88fa70/image.png" width="80%">
1.2. Select **Control Panel** > **Programs** > **Turn Windows Features on or off** > **Features** and check **Client for NFS** to enable the NFS client service for Windows.
<img src="https://mc.qcloudimg.com/static/img/4f9d7ac7b877ceffc5bc2b1d7c050a24/image.png" width="80%">

#### 2. Verify whether the NFS service is enabled

Open the command line tool on Windows and run the following command. If NFS-related information is returned, the NFS client is running properly.
```bash
mount -h
```
<img src="https://mc.qcloudimg.com/static/img/4e4f9db217874ccec91ac1f888c8e451/image.png" width="80%">


#### 3. Add an anonymous user and user group

3.1. Open the Registry
Enter the `regedit` command in the command line window and press Enter to open the Registry.
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


3.3. Restart the system to make the configuration take effect
Close the Registry and restart Windows to complete the Registry modification.

#### 4. Mount the file system

A file system can be mounted through graphical interface or command line (CMD).

- Mount through graphical interface
  a. Open "Map Network Drive"
  Log in to Windows where you need to mount the file system, find "Computer" in the "Start" menu, right-click it, and then click "Map Network Drive" in the menu that appears. 
  
  ![](https://mc.qcloudimg.com/static/img/c9fca9a1b123a5b2dbc69b0ce66d539f/image.png)
  b. Enter the access path
  In the pop-up window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the NFS file system).
  ![](https://main.qcloudimg.com/raw/1527f4e7e72b465abc374c2ccb954830.png)
	<img src="https://main.qcloudimg.com/raw/3de493b63f5687253caf9cf99322b17b.png" width="80%">
	
	c. Check file system permissions
	Check whether the above file system is mounted with root permissions in the following way: open a Windows command line tool and enter the `mount` command.
	Confirm on the command line whether the UID and GID are 0, and if yes, the file system has been mounted with root permissions and can be used normally; if the UID and GID are -2 or other values, data may not be written normally, and you should repeat the previous steps to ensure that the file system is mounted with root permissions.
	<img src="https://main.qcloudimg.com/raw/3ccc26279bb8d73c16eae43f89fea8c7.png" width="80%">
  
	d. Verify reads/writes
  After confirmation, the page goes directly to the file system that has been mounted. You can right-click to create a file for verifying the correctness of read/write.
	<img src="https://main.qcloudimg.com/raw/598f69f5f327c1acc663b4a3eed5ba03.png" width="80%">
- Mount through CMD
  Enter the following command on the Windows command line to mount the file system. The default subdirectory is `FSID`.
```bash
mount <mount target IP>:/<FSID> <shared directory name>:
```
Sample:
```bash
mount 10.10.0.12:/z3r6k95r X:
```
> You can go to the **CFS Console** > **File System Details** > **Mount Target Info** to get the `FSID` mount command.

### Mounting a CIFS/SMB file system

A CIFS/SMB file system can be mounted through graphical interface or command line.

#### Mounting a file system through graphical interface

>CIFS/SMB file systems are in beta test. For more information, please see [Notes on CIFS/SMB Beta Test](https://intl.cloud.tencent.com/document/product/582/9553).

1. Open "Map Network Drive"
   Log in to Windows where you need to mount the file system, find "Computer" in the "Start" menu, right-click it, and then click "Map Network Drive" in the menu that appears. 
   
   ![](https://main.qcloudimg.com/raw/759b315c65db82db3feacd811aa93bdd.png)
2. Enter the access path
   In the pop-up window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the CIFS/SMB file system).
   ![](https://main.qcloudimg.com/raw/1527f4e7e72b465abc374c2ccb954830.png)
3. Verify read/write
   After confirmation, the page goes directly to the file system that has been mounted. You can right-click to create a file for verifying the correctness of read/write.
	 <img src="https://main.qcloudimg.com/raw/598f69f5f327c1acc663b4a3eed5ba03.png" width="80%">

#### Mounting a file system through command line
Use FSID to mount the file system. The mount command is as follows:
```bash
net use <shared directory name>: \\10.10.11.12\FSID 
```

Sample:
```bash
net use X: \\10.10.11.12\fjie120
```

> You can go to the **[CFS Console](https://console.cloud.tencent.com/cfs)** > **File System Details** > **Mount Target Info** to get the `FSID`.



## Step 4. Unmount the file system
#### Unmounting a shared directory through graphical interface

To disconnect a mounted file system, simply right-click the disk and click **Disconnect** in the menu that appears.
 <img src="https://main.qcloudimg.com/raw/3c6c6649a6df3513ea2d7436c0ab7cf3.png" width="80%">

#### Unmounting an NFS shared directory through CMD 

In case you need to unmount a shared directory, please open the Windows Command Prompt and run the following command, where "directory name" is the root directory or the full path of the file system.
```bash
umount <directory name>:
```

Sample:
```bash
umount X:
```

## Step 5. Terminate a resource

You can terminate a file system in the console. Specifically, go to the [CFS Console](https://console.cloud.tencent.com/cfs), select the file system to be terminated, and click **Delete** > **OK**.
