## Overview

This document describes how to use CFS file systems on Windows clients. The example below shows how to do so on Windows Server 2012 R2. The operations are the same on other Windows editions such as Windows Server 2008 and Windows Server 2016.

## Directions

The steps to use a CFS file system are as follows: [create a file system and mount point](#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.8F.8A.E6.8C.82.E8.BD.BD.E7.82.B9) > [connect to a CVM instance](#.E8.BF.9E.E6.8E.A5.E5.AE.9E.E4.BE.8B) > [mount the file system](#.E6.8C.82.E8.BD.BD.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F) > [unmount a shared file system](#.E5.8D.B8.E8.BD.BD.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F) > [terminate resources](#.E7.BB.88.E6.AD.A2.E8.B5.84.E6.BA.90). For specific directions, please see the sections below.

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
    <p>VPC or basic network. Please create and mount the file system according to the network type in which your CVM instance resides; otherwise, access may fail as network interconnection is unavailable.</p>
    <li>To allow a file system to be shared by CVM instances in the same VPC, you need to select VPC when creating the file system. If a file system resides in a VPC, only CVM instances in the same VPC can be mounted if no specific network settings are made.</p>
    <li>To allow a file system to be shared by CVM instances in the basic network, you need to select basic network when creating the file system. If a file system resides in the basic network, only CVM instances in the basic network can be mounted if no specific network settings are made.</p>
    <li>If a file system needs to be shared across multiple networks, please see <a href="https://intl.cloud.tencent.com/document/product/582/9764">Cross-network Access to File System</a>.</p>
    </td>
  </tr>  
  <tr>
    <td>Permission group</td>
    <td>Each file system must be bound to a permission group, which specifies the access whitelist and read/write permissions.
    </td>
  </tr>
</table>

#### 3. Get the mount point information

Get the mount point information. After the file system and mount point are created, click the instance ID to enter the file system details page and click **Mount Point Info** to get the mount command for the file system on a Window client. Please use the recommended mount command to perform the mount operation.
**Quantity** refers to the number of mounted sources, i.e., the number of ways of mounting. Currently, only mounting via IP is supported, so this value is 1.


### Connecting to an instance

This section describes how to log in to a Windows-based CVM instance. Login method varies by scenario. This section shows how to log in to the instance through the console. For more information on other login methods, please see [Logging in to a Windows-based Instance](/doc/product/213/5435).

#### Prerequisites

You need to use an admin account ID and the corresponding password to log in to the CVM instance.

- Admin account ID: it is `Administrator` for all Windows-based instances.
- Password: the password is the one you specified when purchasing the CVM instance.

#### Logging in to a CVM instance in the console

1. In the "Operation" column of the CVM instance list, click **Log in** to connect to the Windows-based CVM instance via VNC.
2. Select **Ctrl-Alt-Delete** in the top-left corner to go to the login page.
3. Enter the account ID `Administrator` and its password to log in.

>This instance is exclusive, i.e., only one user can log in through the console at a time.

#### Verifying network communication

Before mounting, you need to confirm the network connectivity between the client and the file system (the Telnet service needs to be enabled on Windows clients). You can use the `telnet` command for verification. The specific protocols and open ports for clients are as follows:

| File System Protocol | Open Port for Client | Check Network Connectivity |
| ------------ | -------------- | ------------------------- |
| NFS v3.0 | 111, 892, 2049 | telnet 111 or 892 or 2049 |
| NFS v4.0 | 2049 | telnet 2049 |
| CIFS/SMB | 445 | telnet 445 |

>CFS does not support `ping` currently.

### Mounting a file system

#### Mounting an NFS file system

#### 1. Enable the NFS service

Before mounting, please make sure that the NFS service has been turned on.
1.1. Select **Control Panel** > **Programs** > **Turn Windows Features on or off** > **Server Roles** and check **Server for NFS**.
![](https://mc.qcloudimg.com/static/img/eaeed922e9d1f673e47137d80a88fa70/image.png)
1.2. Select **Control Panel** > **Programs** > **Turn Windows Features on or off** > **Features** and check **Client for NFS** to enable the NFS client service for Windows.
![](https://mc.qcloudimg.com/static/img/4f9d7ac7b877ceffc5bc2b1d7c050a24/image.png)

#### 2. Verify whether the NFS service is enabled

Open the command line tool on Windows and run the following command. If NFS-related information is returned, the NFS client is running properly.
```bash
mount -h
```
![](https://mc.qcloudimg.com/static/img/4e4f9db217874ccec91ac1f888c8e451/image.png)

#### 3. Add an anonymous user and user group

3.1. Open the Registry
Enter the `regedit` command in the command line window and press Enter to open the Registry.
![](https://mc.qcloudimg.com/static/img/c9fca9a1b123a5b2dbc69b0ce66d539f/image.png)

3.2. Add configuration items `AnonymousUid` and `AnonymousGid.`
Find the following path in the registry and select it. 
```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default
```

Right-click the blank space on the right, click **New**, and select **DWORD (32-bit) Value** or **QWORD (64-bit) Value** (depending on the bit count of your OS) in the menu. At this point, a new record will appear in the list. Change the name field to `AnonymousUid` and use the default value of 0. Add a record named `AnonymousGid` with the default value of 0 too by using this method.
![](https://mc.qcloudimg.com/static/img/381cdc3b68fb35be5dcceb2a4c962e33/image.png)

Then, the configuration items are successfully added as shown below:
![](https://main.qcloudimg.com/raw/9af3f35d4b78a2e17cf2ef44fa6863d7.png)

3.3. Restart the system to make the configuration take effect
Close the Registry and restart Windows to complete the Registry modification.

#### 4. Mount the file system

A file system can be mounted via graphical interface or command line (CMD).

- Mount via graphical interface
  a. Open "Map Network Drive"
  Log in to Windows where you need to mount the file system, find "Computer" in the "Start" menu, right-click it, and then click "Map Network Drive" in the menu that appears. 
  ![](https://main.qcloudimg.com/raw/759b315c65db82db3feacd811aa93bdd.png)
  b. Enter the access path
  In the pop-up window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the NFS file system).
  ![](https://main.qcloudimg.com/raw/1527f4e7e72b465abc374c2ccb954830.png)
  ![](https://main.qcloudimg.com/raw/3de493b63f5687253caf9cf99322b17b.png)
  c. Verify read/write
  After confirmation, the page goes directly to the file system that has been mounted. You can right-click to create a file for verifying the correctness of read/write.
  ![](https://main.qcloudimg.com/raw/598f69f5f327c1acc663b4a3eed5ba03.png)
- Mount via CMD
  Enter the following command on the Windows command line to mount the file system. The default subdirectory is `FSID`.
```bash
mount <mount point IP>:/<FSID> <shared directory name>:
```
Example:
```bash
mount 10.10.0.12:/z3r6k95r X:
```
> You can go to the **CFS Console** > **File System Details** > **Mount Point Info** to get the `FSID` mount command.

#### Mounting a CIFS/SMB file system

A CIFS/SMB file system can be mounted via graphical interface or command line.

#### Mounting a file system via graphical interface

>CIFS/SMB file systems are in beta test. For more information, please see [Notes on CIFS/SMB Beta Test](https://intl.cloud.tencent.com/document/product/582/9553).

1. Open "Map Network Drive"
   Log in to Windows where you need to mount the file system, find "Computer" in the "Start" menu, right-click it, and then click "Map Network Drive" in the menu that appears. 
2. Enter the access path
   In the pop-up window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the CIFS/SMB file system).
3. Verify read/write
   After confirmation, the page goes directly to the file system that has been mounted. You can right-click to create a file for verifying the correctness of read/write.

#### Mounting a file system via command line
Use FSID to mount the file system. The mount command is as follows:
```bash
net use <shared directory name>: \\10.10.11.12\FSID 
```

Example:
```bash
net use X: \\10.10.11.12\fjie120
```

> You can go to the **CFS Console** > **File System Details** > **Mount Point Info** to get the `FSID` mount command.



### Unmounting a file system
#### Unmounting a shared directory via graphical interface

To disconnect a mounted file system, simply right-click the disk and click **Disconnect** in the menu that appears.
![](https://main.qcloudimg.com/raw/3c6c6649a6df3513ea2d7436c0ab7cf3.png)

#### Unmounting an NFS shared directory via CMD 

In case you need to unmount a shared directory, please open the Windows Command Prompt and run the following command, where "directory name" is the root directory or the full path of the file system.
```bash
umount <directory name>:
```

Example:
```bash
umount X:
```

### Terminating a resource

You can terminate a file system in the console. Specifically, go to the [CFS Console](https://console.cloud.tencent.com/cfs), select the file system to be terminated, and click **Delete** > **OK**.
