## Overview
You can view the created file systems and manipulate them in the CFS console, such as viewing the file system status and usage, file system details, and mount point information.

>!If a file system is in the **Creating** status, you cannot view its details or delete it.

## Prerequisites

Log in to the [CFS console](https://console.cloud.tencent.com/cfs) and click **File System** on the left sidebar to enter the file system list page.

## Viewing File System Status and Usage
You can view the current file system usage and status on the file system list page. CFS also allows you to search for items by file system name, ID, VPCID, and IP.


## Viewing a File System
Click a file system name on the file system list page to enter the file system details page, where you can view the basic information of the file system as well as information of its mount point and mounted clients.

### Basic information of a file system
The basic information of a file system includes its region, file system ID, name, file service protocol, file system status, and creation time. You can set the file system name on this page.

### Mount point information
The mount point information of an NFS file system includes the network information, permission group, and recommended mount command. You can modify the file system permission group on this page.

### Mounted client information
You can select the **Mounted Clients** tab to view the information of the clients where the file system is mounted.
>!Client information display may have a delay of 1–3 minutes.


## Renaming a File System
Click the file system to be renamed in the file system list to enter the file system details page, where you can click <img src="https://main.qcloudimg.com/raw/a779dd9fce8c531f8ca36cf19c7d4d42.png"  style="margin:0;"> to the right of the instance name to rename the file system.


## Deleting a File System
If you no longer need a file system, you can find it in the file system list and select **Delete** in the "Operation" column to delete it.
>!To avoid system exceptions on clients, please disconnect the file system from all clients before deleting it.


