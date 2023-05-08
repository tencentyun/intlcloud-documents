## Overview
If the data storage space of a node becomes insufficient as your business grows, you need to expand the space. This document describes how to scale up cloud disks in the EMR console.
>! 
>- You can scale up only cloud data disks but not system disks and local disks.
>- You cannot batch scale up cloud data disks on multiple nodes.
>- For your data security, we recommend you create snapshots of your cloud disks before scale-up.
>- To prevent data loss, a disk can be scaled up only but not scaled down.

## Scaling up Cloud Disks
### Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of a target cluster in the cluster list to go to the cluster details page.
2. Click the **Resource Management** tab and then click **Scale up cloud data disk** in the **Operation** column of the target node to enter the settings page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Zpwa251_%E5%9B%BD%E9%99%8519.png)
3. If multiple cloud data disks are mounted to the current node, you can batch scale them up to the same capacity.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Zfb7538_%E5%9B%BD%E9%99%85%E7%AB%9920.png)
4. Disks will be initialized automatically after scale-up, and you don't need to manually update the disk information.

