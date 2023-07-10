## Overview

This document describes how to use CFS file systems on Windows clients. The example below shows how to do so on Windows Server 2012 R2. The operations are the same on other Windows editions such as Windows Server 2008 and Windows Server 2016.


## Step 1. Create a File System and Mount Target

For detailed directions, see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


## Step 2. Connect to an Instance

1. Log in to a Windows instance using the standard method.
For other login methods, see [Logging in to Windows instance](https://intl.cloud.tencent.com/document/product/213/32495).
2. Verify the network communication.
Before mounting, you need to check the network connectivity between the client and the file system (the Telnet service needs to be enabled on Windows clients). You can use the `telnet` command for verification, such as `telnet 192.168.1.1 445`. The specific protocols and ports as follows:
<table>
	<tr><th>File System Protocol</th><th>Open Port for Client</th><th>Check Network Connectivity</th></tr>
	<tr><td>NFS 3.0</td><td>111, 892, and 2049</td><td>telnet 111, 892, or 2049</td></tr>
	<tr><td>NFS 4.0</td><td>2049</td><td>telnet 2049</td></tr>
	<tr><td>CIFS/SMB</td><td>445</td><td>telnet 445</td></tr>
</table>


## Step 3. Mount a File System

>? We recommend you use SMB to mount CFS.
>

### Mounting a CIFS/SMB file system

A CIFS/SMB file system can be mounted via a command line or graphical interface.

#### Mounting a file system via command line

Use FSID to mount the file system. The mount command is as follows:
```bash
net use <shared directory name>: \\<mount target IP>\FSID 
```
Sample:
```bash
net use X: \\10.10.11.12\fjie120
```
>! You can go to the [CFS console](https://console.cloud.tencent.com/cfs), click the file system ID, and choose the **Mount Target Info** tab to obtain the `FSID` mount command.
>

#### Mounting a file system via a graphical interface

1. Click ![](https://qcloudimg.tencent-cloud.cn/raw/87424b64a5a4e1eccc091598bc74dd80.png) to enter the Start menu page.
2. Right-Click **This PC** and select **Map network drive**. 
![](https://main.qcloudimg.com/raw/759b315c65db82db3feacd811aa93bdd.png)
3. In the pop-up window, set the drive letter for **Drive** and folder (i.e., the mount directory you see in the CIFS/SMB file system) and click **Finish**.
![](https://main.qcloudimg.com/raw/1527f4e7e72b465abc374c2ccb954830.png)
4. You will be redirected to the file system that has been mounted. You can right-click to create a file and verify read/write correctness.
![](https://main.qcloudimg.com/raw/598f69f5f327c1acc663b4a3eed5ba03.png)


### Mounting an NFS file system

#### 1. Enable the NFS service
>? Before mounting, please make sure that the NFS service has been enabled.
>

1. Click ![](https://qcloudimg.tencent-cloud.cn/raw/87424b64a5a4e1eccc091598bc74dd80.png) and select **Control Panel** > **Programs** > **Turn Windows Features on or off**.
2. In the **Add Roles and Features Wizard** window that pops up, keep the default configuration and click **Next** 5 consecutive times.
3. On the **Features** page, select **Client for NFS** and click **Next**.
![](https://mc.qcloudimg.com/static/img/4f9d7ac7b877ceffc5bc2b1d7c050a24/image.png)
4. Click **Install**.
5. Restart the CVM instance.


#### 2. Verify whether the NFS service is enabled

1. Open the command line tool and run the following command:
```bash
mount -h
```
If NFS-related information is returned, the NFS client is running properly.
![](https://mc.qcloudimg.com/static/img/4e4f9db217874ccec91ac1f888c8e451/image.png)


#### 3. Add an anonymous user and user group

1. Right-Click ![](https://qcloudimg.tencent-cloud.cn/raw/87424b64a5a4e1eccc091598bc74dd80.png) and select **Run**.
2. In the **Run** window, enter the `regedit` command and click **OK** to open the **Registry Editor** window.
![](https://mc.qcloudimg.com/static/img/c9fca9a1b123a5b2dbc69b0ce66d539f/image.png)
3. Find the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default` path in the registry and select it. 
4. Right-Click in the blank space on the right and select **New** > **DWORD (32-bit) Value** or **QWORD (64-bit) Value** (subject to the number of bits of your operating system).
5. In the new record that appears in the list, set its name to **AnonymousUid** and use the default data value of 0.
6. Repeat **step 4** to add another record, set its name to **AnonymousUid**, and use the default data value of 0.
![](https://mc.qcloudimg.com/static/img/381cdc3b68fb35be5dcceb2a4c962e33/image.png)
7. Close the Registry Editor and then run the commands below on the command line tool in sequence to restart the NFS client service so that the modified Registry can take effect. You can also restart the Windows OS for the modified Registry to take effect.
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

#### 4. Mount an NFS file system

A file system can be mounted via a command line or graphical interface.

#### Mounting a file system via command line

Enter the following command on the command line tool to mount the file system. The default subdirectory is `FSID`.
```bash
mount <mount target IP>:/<FSID> <shared directory name>:
```
Sample:
```bash
mount 10.10.0.12:/z3r6k95r X:
```
>! You can go to the CFS console, click the file system ID, and choose the **Mount Target Info** tab to obtain the `FSID` mount command.
>


#### Mounting a file system via a graphical interface

1. Click ![](https://qcloudimg.tencent-cloud.cn/raw/87424b64a5a4e1eccc091598bc74dd80.png) to enter the Start menu page.
2. Right-Click **This PC** and select **Map network drive**. 
![](https://main.qcloudimg.com/raw/759b315c65db82db3feacd811aa93bdd.png)
3. In the pop-up window, set the drive letter for **Drive** and folder (i.e., the mount directory you see in the NFS file system) and click **Finish**.
![](https://main.qcloudimg.com/raw/1527f4e7e72b465abc374c2ccb954830.png)
4. Open the command line tool and enter the `mount` command to check whether the above file system is mounted with root permissions in the following way.
![](https://main.qcloudimg.com/raw/3ccc26279bb8d73c16eae43f89fea8c7.png)
Check whether the UID and GID values are 0. If so, the file system has been mounted with root permissions and can be used. If the UID and GID are -2 or other values, data may not be written properly, and you should repeat the previous steps to ensure that the file system is mounted with root permissions.

 If the Windows command-line tool displays "Locking=yes", to avoid read/write exception (NFS v3 does not support locking), you can modify the Registry by performing the following steps:
 1. Find the following registry path: **HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > ClientForNFS > CurrentVersion > User > Default > Mount**.
 2. Move the mouse to the right pane and right-click there. Click **New** and choose **DWORD (32-bit) Value** from the drop-down menu. Then, change the name to **Locking** and set the value to `0`.
5. You will be redirected to the file system that has been mounted. You can right-click to create a file and verify read/write correctness.



## Step 4. Unmount the File System

#### Unmounting a shared directory via command 

If you need to unmount a shared directory, please open the Windows Command Prompt and run the following command, where "directory name" is the root directory or the full path of the file system.

Sample for NFS:
```bash
umount X:
```

Sample for SMB:
```net use x: /del

```

#### Unmounting a shared directory via a graphical interface

To disconnect a mounted file system, simply right-click the disk and click **Disconnect** in the menu that appears.
 <img src="https://main.qcloudimg.com/raw/3c6c6649a6df3513ea2d7436c0ab7cf3.png" width="80%">


## Step 5. Terminate a Resource

>! Resources cannot be recovered from a deleted file system. Therefore, you are advised to back up all resources before deleting the file system.
>

You can terminate a file system in the console. Specifically, go to the [CFS console](https://console.cloud.tencent.com/cfs/fs), locate the file system to be terminated, and click **Delete** > **Confirm**.


