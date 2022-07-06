## Overview

You can configure a Linux or Windows client to which a CFS file system is mounted, so that the file system can be automatically mounted after the client is restarted.

## Directions
### Automatically mounting an NFS file system on Linux
1. Connect to the CVM instance that needs to automatically mount the file system by logging in to the CVM Console or performing remote login. Then, open the "/etc/fstab" file (make sure that the account you logged in to has the root privileges).
```
// Run the following command to open the `fstab` file
vi /etc/fstab
```

2. Then, enter "i" (insert) and add the following command to `/etc/fstab`. The mounting methods are as follows:
```shell
Mount the file system with NFS v4.0
<mount point IP>:/ <target mount directory> nfs vers=4,minorversion=0,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
Example: 10.10.19.12:/ /local/test nfs vers=4,minorversion=0,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
```
```shell
Mount the file system with NFS v3.0
<mount point IP>:/<fsid> <target mount directory> nfs vers=3,nolock,proto=tcp,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
Example: 10.10.19.12:/djoajeo4 /local/test nfs vers=3,nolock,proto=tcp,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
```
```shell
Mount the file system with Turbo
<mount point IP>@tcp0:/<fsid>/cfs <target mount directory> lustre defaults,_netdev 0 0 
Example: 172.16.0.7@tcp0:/01184207/cfs /root/turbo lustre defaults,_netdev 0 0

```
3. Press Esc and enter ":wq" to save the change. Restart the client, and the file system will be automatically mounted.

>! When the command of automatic mounting is added but the shared file system is exceptional, Linux may not be started normally, because the automatic start command in `fstab` is not executed. To solve this problem, enter "Single User Mode" upon startup, delete the automatic mounting command in `fastb`, and then restart the server.


### Automatically mounting a file system on Windows
When mounting a file system, select "Reconnect at logon" as shown below. For more information, please see [Using CFS File Systems on Windows Clients](https://intl.cloud.tencent.com/document/product/582/11524).
