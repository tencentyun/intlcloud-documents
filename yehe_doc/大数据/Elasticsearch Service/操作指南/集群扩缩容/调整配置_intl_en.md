## Use Cases

As your business grows, the amounts of data and access requests in a cluster are ever-changing and may increase significantly. When the size of the cluster fails to meet your actual business needs, you can dynamically adjust the cluster configuration to scale it out. You can also temporarily scale it in if the amounts of data and access requests get smaller. ES supports adjusting configuration items such as number of nodes, node types, and storage capacity of individual data nodes. In addition, it also supports adjusting dedicated master nodes as detailed below.

>! Scale-in is currently restricted and you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## Directions

1. Log in to the [ES Console](https://console.cloud.tencent.com/es) and enter the cluster list page.
2. You can **adjust the cluster configuration** on either the cluster list page or cluster details page. 
 - On the cluster list page, select the cluster to be scaled out and select **More** > **Adjust Configuration** in the "Operation" column.
 - Click the cluster name to enter the cluster details page and select **More** > **Adjust Configuration** in the top-right corner.
3. In the **Adjust Configuration** dialog box that pops up, adjust the cluster node model or quantity according to your business needs and click **OK**.
> ?Either node type (node model and storage capacity) or node quantity can be adjusted at a time.
>
>4. After the configuration adjustment starts, the cluster status will change to **processing**. After the status changes to **normal**, the cluster can be used normally.  
5. You can view the progress of cluster adjustment on the cluster details page.


- Adjust the data node configuration.
![](https://main.qcloudimg.com/raw/3baaac98def0637e053788623c5245e0.png)
- Adjust the master node configuration.
![](https://main.qcloudimg.com/raw/a624c1570541ff57b3b2f310125606d3.png)
- View the progress of cluster adjustment.
![](https://main.qcloudimg.com/raw/7745487c55eafc38a1b462ef23ec485d.png)

## Configuration Adjustment Fees

- For postpaid pay-as-you-go clusters, fees are charged by the minute. After the configuration adjustment is completed, fees for the next minute will be calculated based on the price of the new configuration.

