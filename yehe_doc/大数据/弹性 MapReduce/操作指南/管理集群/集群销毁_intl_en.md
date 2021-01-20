## Feature Overview
When you no longer need an EMR cluster, you can terminate it in the [EMR console](https://console.cloud.tencent.com/emr).
## Prerequisites
- Pay-as-you-go cluster: once terminated, the cluster will not be retained in the recycle bin but will be completely terminated and cannot be recovered. Please do so with caution.
- Before terminating a cluster, please make sure that your data has been backed up as it cannot be recovered after termination.
- If there is an EIP (an IP with a secondary ENI), the instance will be retained once returned, and the idle IP will continue to incur fees. If you don't need to retain it, please release it on the corresponding resource management page.

## Directions
>!If MetaDB in the cluster to be terminated is associated with an external cluster as a Hive metadatabase, it will be retained when the cluster is terminated; if you no longer need it, please go to the TencentDB console to terminate it. Hive metadatabases cannot be recovered once terminated. Please do so with caution.

Log in to the [EMR console](https://console.cloud.tencent.com/emr), select **Action** > **More** > **Terminate** to enter the cluster termination page. Confirm the information of the cluster that needs to be terminated. After confirming that everything is correct, check **I have read and agree to** and click **Next**.
![](https://main.qcloudimg.com/raw/50398d8c5468d4b4bb809785ca9de2de.png)
After confirming that everything is correct on the **Confirm Termination** tab, click **Start Termination** to terminate the cluster.
![](https://main.qcloudimg.com/raw/a8f60aac8339c6edbd510ae0deeb5d5d.png)
