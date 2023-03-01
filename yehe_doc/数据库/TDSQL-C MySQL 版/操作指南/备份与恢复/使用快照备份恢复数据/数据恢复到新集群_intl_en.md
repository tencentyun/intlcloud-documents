TDSQL-C for MySQL can roll back databases/tables to the original cluster as instructed in [Restoring Data to Original Cluster](https://www.tencentcloud.com/document/product/1098/48393) and roll back an entire cluster (clone) to a new cluster. You can choose different rollback methods based on your business needs. This document describes how to clone a cluster in the console to quickly roll back an instance into a new cluster.

TDSQL-C for MySQL provides the clone feature to restore a cluster to any time point in the log backup retention period or to the backup set of the specified backup file.
The clone will create a new cluster based on your choice. After the new cluster is verified, you can either use the new cluster directly or migrate the data back to the original cluster through DTS as instructed in [Migration from MySQL/MariaDB/Percona to TDSQL-C for MySQL](https://intl.cloud.tencent.com/document/product/571/47364).

>?Billing will start for the new cluster after the clone succeeds. For more information on billing and pricing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1098/40620).

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Backup Management** tab and click **Clone** in the **Operation** column in the backup list.
3. On the purchase page that pops up, select the backup file for restoration by time point, cluster specification, and period, and then click **Next**.
   - Billing Mode: Monthly subscription, pay-as-you-go, and serverless billing modes are supported.
   - Rollback Mode: Clone by backup file and clone by time point are supported.
     - By backup file: A new cluster can be created from the specified backup set for restoration, and the selection range is based on the time when the backup is completed and the retention period.
     - By time point: A new cluster can be created from the specific time point for restoration, and the time point selection range is based on the backup retention period.
  - Region: Same as that of the cloned cluster.
  - AZ: Same as that of the cloned cluster.
  - Network: Select VPC.
  - Compatible Database: Same as that of the cloned cluster.
  - Compute Instance Quantity: Select the numbers of read-write nodes and read-only nodes.
  - Instance Specification: Select the CPU and memory of the instance.
  - Storage Billing Mode: Monthly subscription and pay-as-you-go billing modes are supported. Monthly subscription can be selected here only if the compute billing mode is monthly subscription.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NSwt135_17.png)
4. Configure the **Basic Info** and **Advanced Configuration** settings on the page redirected to, such as cluster name, default character set, security group, parameter template, and project. Then, click **Buy Now**.
5. Return to the cluster list, and you can see the new cluster created through clone. After its status changes from **Cloning** to **Running**, it can be used normally.
>?After confirming that the data in the new cluster created through clone is correct, you can modify the cluster VIP or click **Delete** in the **Operation** column to delete the old cluster on the cluster details page as needed.
