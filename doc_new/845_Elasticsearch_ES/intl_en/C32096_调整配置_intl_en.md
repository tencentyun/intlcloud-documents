## Use Cases

As your business grows, the amounts of data and access requests in a cluster are ever-changing and may increase significantly. When the size of the cluster fails to meet your actual business needs, you can dynamically adjust the cluster configuration to scale up the cluster. You can also temporarily scale down the cluster if the amounts of data and access requests get smaller. ES supports adjusting configuration items such as number of nodes, node types, and storage capacity of individual data nodes. In addition, it also supports adjusting the dedicated master nodes of the cluster as detailed below.

> Scale-down is currently restricted and you can apply for it by submitting a [ticket](https://console.cloud.tencent.com/workorder/category).

## Directions

1. Log in to the [ES Console](https://console.cloud.tencent.com/es) and enter the cluster list page.
2. You can **adjust the cluster configuration** on either the cluster list page or the cluster details page. 
 - On the cluster list page, select the cluster to be scaled and select **More** > **Adjust Configuration** in the "Action" column.
 - Click the cluster name to enter the cluster details page and select **More** > **Adjust Configuration** in the top-right corner.
3. In the **Adjust Configuration** dialog box that pops up, adjust the cluster node model or quantity according to your business needs and click **OK**.

> Either node type (node model and storage capacity) or node quantity can be adjusted at a time, and simultaneous adjustment of both is not supported.

4. After the configuration adjustment starts, the cluster status changes to **processing**. After the status changes to **normal**, the cluster can be used normally.  
5. You can view the progress of cluster adjustment on the cluster details page.


- Adjust the data node configuration.
  ![Adjust configuration](https://main.qcloudimg.com/raw/ea8d73de889458f1b2ad29bbe7bca0cf.png)
- Adjust the master node configuration.
  ![Dedicated master node](https://main.qcloudimg.com/raw/d46e45aab5e1599711489244d5b186a4.png)
- View the progress of cluster adjustment.
  ![Dedicated master node](https://main.qcloudimg.com/raw/3cea7e6bb34b7c8930173dd8f0946c24.png)

## Note on Configuration Adjustment Fees

- For pay-as-you-go clusters, the billing cycle is per minute. After the configuration adjustment is completed, fees for the next minute will be calculated based on the price of the new configuration.
