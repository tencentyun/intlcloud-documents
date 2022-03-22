
TDSQL-C can [roll back databases/tables] to an original cluster (https://intl.cloud.tencent.com/document/product/1098/40634) and roll back an entire cluster (clone) to a new cluster. You can choose different rollback methods according to your business needs. This document describes how to clone a cluster in the TDSQL-C console to quickly roll back an instance into a new cluster.

TDSQL-C provides the clone feature, which can restore a cluster to any time point in the log backup retention period or to the backup set of the specified backup file through clone.
The clone will create a new cluster based on your choice. After the new cluster is verified, you can [migrate the data back to the source cluster through DTS](https://cloud.tencent.com/document/product/571/45488) or directly use the cloned new cluster.

>?Billing will start for the cloned new cluster after the clone succeeds. For more information on billing and pricing, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1098/40620).

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Backup Management** tab and click **Clone** in the **Operation** column in the clone list.
3. On the purchase page that pops up, select the backup file and cluster specification for restoration by time point, confirm that everything is correct, and click **Buy Now**.
 - Billing Mode: pay-as-you-go and serverless billing modes are supported.
 - Rollback Mode: clone by backup file and clone by time point are supported.
    - By backup file: a new cluster can be created from the specified backup set for restoration, and the selection range is based on the time when the backup is completed and the retention period.
    - By time point: a new cluster can be created from the specific time point for restoration, and the time point selection range is based on the backup retention period.
![](https://main.qcloudimg.com/raw/ddf2b6523bea104cef180a935c64e12a.png)
4. Return to the cluster list and you can see the new cluster created through backup file rollback. After its status changes to "Running", it can be used normally.
>?After confirming that the data in the new cluster created through clone is correct, you can modify the cluster VIP or click **Delete** in the **Operation** column to delete the old cluster on the cluster details page as needed.
