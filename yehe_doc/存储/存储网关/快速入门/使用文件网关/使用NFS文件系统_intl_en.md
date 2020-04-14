After creating a file system, configure a server or client as follows and then mount the file system to it for use. NFS file gateway supports the NFS v3.0 and NFS v4.0 protocols.

>If you are using a gateway on CVM, you are recommended to deploy the gateway under the VPC of each visiting client; if the clients are on different VPCs, please use [Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000) to achieve network interconnection.

You can view the mount command on the file system details page.



## Using NFS File System on Linux

### Starting NFS client

Before mounting, please make sure that nfs-utils or nfs-common has been installed on the system. The installation method is as follows:

- CentOS: sudo yum install nfs-utils
- Ubuntu or Debian: sudo apt-get install nfs-common


### NFS v4.0 mounting

Run the following command to achieve NFS v4.0 mounting: 

```
sudo mount -t nfs -o vers=4 <mount target IP>:/share/nfs/<file system name, i.e. bucket name> <destination directory to be mounted>
```
>
>- There is a space between "<file system name, i.e. bucket name>" and "<destination directory to be mounted>".
>- Mount target IP: this refers to the IP address of the gateway. 
>- By default, the file system is mounted under the file system directory (i.e., the file system name). If a subdirectory is created in the file system, it can be mounted to.
>- Target mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.

#### Sample
- Mount the root directory of the file system: sudo mount -t nfs -o vers=4 10.0.0.1:/share/nfs/bucketname /local/test
- Mount the subdirectory "subfolder" of the file system: sudo mount -t nfs -o vers=4 10.10.19.12:/share/nfs/bucketname/subfolder /local/test


### NFS v3.0 mounting

Run the following command to achieve NFS v3.0 mounting: 
```
sudo mount -t nfs -o vers=3,nolock,proto=tcp <mount target IP>:/share/nfs/<file system name, i.e. bucket name> <destination directory to be mounted>
```

>
>- There is a space between "<file system name, i.e. bucket name>" and "<destination directory to be mounted>".
>- Mount target IP: this refers to the IP address of the gateway. 
>- By default, the file system is mounted under the file system directory (i.e., the file system name). If a subdirectory is created in the file system, it can be mounted to.
>- Target mount directory: this refers to the target directory to be mounted to on the current server and needs to be created in advance.


#### Sample
- Mount the root directory of the file system: mount -t nfs -o vers=3,nolock,proto=tcp 10.10.19.12:/share/nfs/bucketname /local/test
- Mount the subdirectory "subfolder" of the file system: mount -t nfs -o vers=3,nolock,proto=tcp 10.10.19.12:/share/nfs/bucketname/subfolder /local/test


### Viewing mount target information 

After the mount is completed, run the following command to view the mounted file system.
```
mount -l
```

You can also run the following command to view the capacity information of the file system.
```
df -h
```


### Unmounting shared directory 

In case you need to unmount a shared directory, run the following command where "directory name" is the root directory or the full path of the file system.
```
umount <directory name>
// For example, umount /local/test
```

## Using NFS File System on Windows

### Enabling NFS service

Before mounting, please make sure that the NFS service has been enabled. Taking Windows Server 2012 R2 as an example, you can enable the service in the following way:

Open Control Panel -> Programs -> Turn Windows features on or off -> select "Server for NFS" in **Server Roles** -> select "Client for NFS" in **Features** to enable the Windows NFS client service.

The following figure uses Windows Server 2012 R2 as an example.
![](https://mc.qcloudimg.com/static/img/eaeed922e9d1f673e47137d80a88fa70/image.png)
![](https://mc.qcloudimg.com/static/img/4f9d7ac7b877ceffc5bc2b1d7c050a24/image.png)

### Checking NFS service status

Open the command line tool on Windows and type the following command. If NFS-related information is returned, the NFS client is running properly.
```
mount -l
```

![](https://mc.qcloudimg.com/static/img/4e4f9db217874ccec91ac1f888c8e451/image.png)

### Adding anonymous visiting user and user group

#### Opening the registry
Enter the `regedit` command in the command line window and press Enter to open the "Registry" window.
![](https://mc.qcloudimg.com/static/img/c9fca9a1b123a5b2dbc69b0ce66d539f/image.png)

#### Adding configuration items `AnonymousUid` and `AnonymousGid`
Find the following path in the Registry and select it: 

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default
```

Right-click the blank space on the right, click **New**, and select **DWORD (32-bit) Value**. At this point, a new record will appear in the list. Change the name field to `AnonymousUid` and use the default value of 0. Add a record named `AnonymousGid` with the default value of 0 too in this method.

![](https://mc.qcloudimg.com/static/img/381cdc3b68fb35be5dcceb2a4c962e33/image.png)

![](https://mc.qcloudimg.com/static/img/80bb0cfbffbed939522459a830df3eac/image.png)

#### Restarting for the configuration to take effect

Close the Registry and restart Windows to complete the Registry modification.


#### Opening "Map Network Drive"
Log in to Windows where you need to mount the file system, find "Computer" in the "Start" menu, right-click it, and then click "Map Network Drive" in the menu that appears. 


#### Entering access path
In the pop-up settings window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the NFS file system).



#### Verifying read/write
After confirmation is completed, you will be redirected to the file system that has been mounted. You can right-click to create a file and verify read/write correctness.


#### Disconnecting the file system
To disconnect a mounted file system, simply right-click the disk and click **Disconnect** in the menu that appears.

