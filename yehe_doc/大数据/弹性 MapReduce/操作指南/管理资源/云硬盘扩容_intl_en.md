## Overview
If the data storage space of a node becomes insufficient as your business grows, you need to expand the disk. This document describes how to expand a cloud disk and mount a cloud disk in the EMR console.
>! 
>- You can expand only cloud data disks but not system disks and local disks.
>- You cannot batch expand cloud data disks on multiple nodes.
>- We recommend you create snapshots for your cloud disks before expanding them, so as to avoid damaging the file system due to maloperations.
>- To prevent data loss, the capacity of disks can only be expanded but not reduced.

## Expanding Cloud Disk
### Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. 	Go to the **Resource Management** page and click **Expand Cloud Data Disk** in the **Operation** column of the target node to enter the expansion configuration page.

3. 	If multiple cloud data disks are mounted to the current node, you can batch expand them to the same capacity.

4. 	An expanded disk will be initialized automatically, and you don't need to manually update the disk information.

## Mounting a Cloud Disk
### Prerequisites
1. Cloud disks cannot be mounted to local disk models.
2. Up to 15 cloud disks can be mounted to a node.
3. You need to purchase a cloud disk in the same billing mode and the same AZ as the EMR node in CBS in advance.

### Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Resource** > **Resource Management** and click **Mount Cloud Data Disk** in the **Operation** column of the target node in the node list.

>! If no cloud data disk is available for mounting, purchase one in CBS.

3. If the expiration time of the mounted disk is earlier than that of the node, you have two options:
	1. Extend the expiration time of the mounted disk to that of the instance in the format of `yyyy-mm-dd xx:xx:xx`.
	2. Auto-renew the disk monthly upon expiration.

4. If multiple disks are mounted, you can only auto-renew them monthly upon expiration.
