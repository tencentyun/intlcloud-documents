Service monitoring provides detailed monitoring features for main services installed in the cluster, including HDFS, YARN, Hive, ZooKeeper, Spark, HBase, and Presto.
## Viewing Service Monitoring Information
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click **Cluster Monitoring** on the left sidebar to enter the cluster monitoring page.
2. Select **Service Monitoring** to view the monitoring information of important services in the cluster.
3. In the service monitoring section, you can view monitoring metric details of service components such as HDFS, YARN, HBase, Spark, Hive, Presto, and ZooKeeper in the current cluster.
4. The service monitoring page provides monitoring views of three service dimensions, namely, service overview, service summary, and role list. As different service components have different services, the dimensions of display vary.
 - **Service Overview** intuitively displays the metrics and their statistical rules of service components in the corresponding time period. The system displays a maximum of 6 metrics by default. You can click "Set Metric" on the right to customize the displayed metrics.
![](https://main.qcloudimg.com/raw/12c9e198bd534098a84e6b89ce9f1df8.png)
![](https://main.qcloudimg.com/raw/8955aa65869661cd2422b0195290844f.png)
 - **Service Summary** displays the current overall status of the service.
![](https://main.qcloudimg.com/raw/abb26f56e50555f3a7427c29cb658887.png)
 - **Role List** displays the service deployment status of each role of the current service component. Click **Node IP** to view the monitoring metrics and their statistical rules of the current node. 6 metrics are displayed by default, and up to 12 metrics can be displayed.
![](https://main.qcloudimg.com/raw/5502b61780676857e2a9a2ce941aa80f.png)
Enter a node page and click **Set Metric** to customize the displayed metrics.
![](https://main.qcloudimg.com/raw/fe70bda0007f64bbd3e36f6be48ffac7.png)
>
> 1. Service monitoring displays the HDFS service component by default. You can manually adjust to view other service components.
> 2. The service monitoring dimensions vary by service component due to different service types. For example, HBase supports table-level monitoring.


## HBase Table Load
### Feature description
HBase table load enables you to monitor the number of read/write requests and storage of each table in HBase.

### Viewing HBase table load
Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster Monitoring** > **Service Monitoring**, and then select the HBase service component to view **HBase Table Load**.

HBase table load displays information of HBase tables in four dimensions: number of real-time read requests, number of real-time write requests, size of MemStore, and size of storeFile. You can click the table header to sort tables by corresponding dimension. In addition, you can enter a table name in the search box in the top-left corner and click ![](https://main.qcloudimg.com/raw/4b7c4ff1fa301f618db0826d4fd6168a.png) to search for the table.
![](https://main.qcloudimg.com/raw/d3869744607345a3767186cdf11892da.png)
 
### Viewing table details
Click a table name to pop up the table details. The details page can display the number of read/write requests and size of store (including MemStore and storeFile) of the selected table in the dimension of entire table or node. You can switch between nodes by using the **Node Filter** in the top-right corner.
 
