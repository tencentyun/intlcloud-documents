## Feature description

The performance trends feature provides the following real-time monitoring information of your MongoDB database to help you locate time-consuming commands and their execution time and overall latency distribution.
- Resource Monitoring: **CPU**, **MEM**, **Storage Space**, and **Traffic**.
- Request Statistics: **Request Latency Distribution**, **Request Type Distribution**, **Request Type with 10-50 ms Latency**, **Request Type with 50-100 ms Latency**, **Request Type with over 100 ms Latency**, **TTL Request Statistics**, **Active Sessions**, and **Request Latency**.
- MongoDB Primary-Secondary Replication: **Secondary Node Replication Delay** and **Oplog Retention Period**.
- Storage Engine: **Cache**, **qr/qw**, and **ar/aw**.

## Viewing performance trends

1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Performance Trends** tab.
2. Set the monitoring dimension and metrics of performance trends.  
   - Monitoring dimension: You can select instance monitoring or node monitoring.
![](https://qcloudimg.tencent-cloud.cn/raw/f3ca724dfe9f42a98f210445902b8ec8.png)
      - Instance dimension: It displays the monitoring view of instances.
      - Node dimension: It displays the comparison trend views of relevant metrics on each MongoDB node.
   - Metric categories: Include **CPU**, **MEM**, **Disk**, **Connection**, **Traffic**, and **Request Statistics**.
   - Select performance metrics: You can select all metrics, custom metrics, and various views.
     - Filter global metrics
       ![](https://qcloudimg.tencent-cloud.cn/raw/c73bd25a48ff2ded73da46b541716777.png)
     - Filter one single metric
       ![](https://qcloudimg.tencent-cloud.cn/raw/7a4a58d54c5e8a9a948b4315f2ea5b25.png)
     - Switch between chart views
      ![](https://qcloudimg.tencent-cloud.cn/raw/ac31c930d5e9d030e0e940573fe1e52a.png)
3. Switch between the **Real-Time** and **Historical** views.
   DBbrain allows you to switch between real-time and historical data. Based on the selected time view, different granularities are provided. Single metric view and comparison view are also available.
   Customize the multi-node comparison chart.
    ![](https://qcloudimg.tencent-cloud.cn/raw/0741af9306a6324fdc78230ee24fbad5.png)
4. Enable chart interaction.
   For one single instance, node, or proxy, you can view relevant metric trend comparison, add custom metrics, and view the performance metric trend comparison by time.
   After you enable chart interaction, when you hover over a data point in any monitoring view, the data at the same time point will be displayed in other monitoring views. Click the data point to pin it for display. To unpin it, click **Deselect the Time Point**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c548dde8155b9dde7c3ed9eed2ebb40b.png)
5. Switch between the one-column and two-column modes, drag a monitoring view, or zoom in a monitoring view.
   - **Switching between the one-column and two-column modes**: Click the button on the right of **Chart Interaction** in the top-right corner to switch.
   - **Dragging a monitoring view**: Click the border of a monitoring view to drag it to the desired position.
   - **Zooming in a monitoring view**: Drag the icon in the bottom-right corner of a monitoring view to zoom it in for fine-grained display of the trend of one single performance metric.
6. Check the status of the MongoDB node. For more information, see [MongoStatus](https://intl.cloud.tencent.com/document/product/1035/48617) and [MongoTop](https://intl.cloud.tencent.com/document/product/1035/48616).
7. View the data of latency analysis.
    Below is a sample performance trends query result. Click a data point in the chart to display the metric details.
   
   - Sample request latency distribution:
     ![](https://qcloudimg.tencent-cloud.cn/raw/4636f59f739bf4bcf05737135e478e28.png)
   - Sample distribution of the request type with over 100 ms latency:
     ![](https://qcloudimg.tencent-cloud.cn/raw/a0e7481925609b55dd7bb0aa4a74331a.png)
   - Sample request latency:
     ![](https://qcloudimg.tencent-cloud.cn/raw/99b790fa508daafa72e0e88d4ee61bb8.png)
     
     
