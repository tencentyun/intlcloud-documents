After creating a file system, configure a server or client as follows and then mount the file system to it for use. NFS file gateway supports the NFS v3.0 and NFS v4.0 protocols.

**Note: If you are using a gateway on CVM, it is recommended to deploy the gateway under the VPC of each visiting client; if the clients are on different VPCs, please use [Peering Connection](https://cloud.tencent.com/document/product/215/5000) to achieve network interconnection.**

You can view the mount command on the file system details page. See below:
![](https://mc.qcloudimg.com/static/img/427c850d61745f04d34e0e4f96f0a9b7/image.png)


## Using an NFS File System on Linux

### Starting the NFS Client

Before mounting, please make sure that nfs-utils or nfs-common is installed on the system. The installation method is as follows:

> CentOS: sudo yum install nfs-utils
> Ubuntu or Debian: sudo apt-get install nfs-common


### NFS v4.0 Mounting

Use the following command to achieve NFS v4.0 mounting: 

> sudo mount -t nfs -o vers=4 <mount point IP>:/share/nfs/<file system name, i.e. bucket name> <destination directory to be mounted>    
> //Note that there is a space between "<file system name, i.e. bucket name>" and "<destination directory to be mounted>".


*Note*
*		 Mount point IP: This refers to the IP address of the gateway. 
*		 Currently, the file system directory (i.e., the file system name) is mounted by default. If a subdirectory is created in the file system, it can be mounted too.
*		 Destination directory to be mounted: This refers to the destination directory to be mounted on the current server and needs to be created in advance.

*Example*
* 		Mount the root directory of the file system: sudo mount -t nfs -o vers=4 10.0.0.1:/share/nfs/bucketname /local/test
* 	Mount the subdirectory "subfolder" of the file system: sudo mount -t nfs -o vers=4 10.10.19.12:/share/nfs/bucketname/subfolder /local/test


### NFS v3.0 Mounting

Use the following command to achieve NFS v3.0 mounting: 

> sudo mount -t nfs -o vers=3,nolock,proto=tcp <mount point IP>:/share/nfs/<file system name, i.e. bucket name> <destination directory to be mounted>   
> //Note that there is a space between "<file system name, i.e. bucket name>" and "<destination directory to be mounted>".

*Note*
*		 Mount point IP: This refers to the IP address of the gateway. 
*		 Currently, the file system directory (i.e., the file system name) is mounted by default. If a subdirectory is created in the file system, it can be mounted too.
*		 Destination directory to be mounted: This refers to the destination directory to be mounted on the current server and needs to be created in advance.


*Example*
*	 Mount the root directory of the file system: mount -t nfs -o vers=3,nolock,proto=tcp 10.10.19.12:/share/nfs/bucketname /local/test
*	 Mount the subdirectory "subfolder" of the file system: mount -t nfs -o vers=3,nolock,proto=tcp 10.10.19.12:/share/nfs/bucketname/subfolder /local/test


### Viewing Mount Point Information 

After the mount is completed, use the following command to view the mounted file system.
> mount -l

You can also use the following command to view the capacity information of the file system.
> df -h

### Unmounting a Shared Directory 

In case you need to unmount a shared directory, use the following command where "directory name" is the root directory or the full path of the file system.
> umount <directory name>
> // For example, umount /local/test


## Using an NFS File System on Windows

### Turning on NFS Service

Before mounting, please make sure that the NFS service has been turned on. Take Windows Server 2012 R2 as an example. The following shows how to turn the service on:

> Open Control Panel -> Programs -> Turn Windows features on or off -> Select "Server for NFS" in **Server Roles** -> Select "Client for NFS" in **Features** to turn on Windows NFS client service.

The following figure uses Windows Server 2012 R2 as an example.
![](https://mc.qcloudimg.com/static/img/eaeed922e9d1f673e47137d80a88fa70/image.png)
![](https://mc.qcloudimg.com/static/img/4f9d7ac7b877ceffc5bc2b1d7c050a24/image.png)

### Verifying NFS Service Is Turned on

Open the command line tool on Windows and type the following command. If NFS-related information is returned, the NFS client is running properly.

> mount -l

![](https://mc.qcloudimg.com/static/img/4e4f9db217874ccec91ac1f888c8e451/image.png)

### Adding an Anonymous Visiting User and User Group

#### Opening the Registry
Enter the regedit command in the command line window and press Enter to open the Registry window.
![](https://mc.qcloudimg.com/static/img/c9fca9a1b123a5b2dbc69b0ce66d539f/image.png)

#### Adding Configuration Items AnonymousUid and AnonymousGid
Find the following path in the Registry and select it: 

> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default

Right click on the space to the right and "New" will pop up. Select "DWORD(32-bit) Value" from the menu. At this point, a new record will appear in the list. Modify the name field to AnonymousUid and use the default value of 0. Add a record named AnonymousGid with the default value of 0 too using this method.

![](https://mc.qcloudimg.com/static/img/381cdc3b68fb35be5dcceb2a4c962e33/image.png)

![](https://mc.qcloudimg.com/static/img/80bb0cfbffbed939522459a830df3eac/image.png)

#### Restarting to Make the Configuration Effective

Close the Registry and restart the Windows to complete the Registry modification.


#### Opening "Map Network Drive"
Log in to Windows where you need to mount the file system, find "Computer" in the "Start" menu, right-click it and then click "Map network drive" in the menu that appears. 
![](https://mc.qcloudimg.com/static/img/5696d66a83d4e9b35196274f89e07dfc/image.png)
![](https://mc.qcloudimg.com/static/img/6eeb1c0838e6aab185ed8b76dc736912/image.png)

#### Entering the Access Path
In the pop-up settings window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the NFS file system).
![](https://mc.qcloudimg.com/static/img/c7b07faf43812540d383b7767c52158b/image.png)


#### Verifying Read/write
After confirmation, the page goes directly to the file system that has been mounted. You can right click to create a file to verify the correctness of read/write.
![](https://mc.qcloudimg.com/static/img/60b9388885536ec7d81b1cf7f76c39d5/image.png)

#### Disconnecting the File System
To disconnect a mounted file system, simply right-click the disk and click **Disconnect** in the menu that appears.
![](https://mc.qcloudimg.com/static/img/376cd0547aa64f4d519e5444c5a58f93/image.png)

