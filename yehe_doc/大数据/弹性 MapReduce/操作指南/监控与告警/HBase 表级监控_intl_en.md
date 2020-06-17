## Feature Description
HBase table-level monitoring enables you to monitor the number of read/write requests and storage of each table in HBase.

### Viewing table monitoring overview
Log in to the [EMR Console](https://console.cloud.tencent.com/emr), click **Component Management** on the left sidebar, select a cluster, and select **HBase** for the component name. You can also click "Role Management" on the right of HBase to enter **Table-level Monitoring**.
The overview page displays information of HBase tables in four dimensions: number of real-time read requests, number of real-time write requests, size of MemStore, and size of storeFile. You can click the table header ![](https://main.qcloudimg.com/raw/c79ddb001c767d587be626c036a00db5.png) to sort tables by corresponding dimension. In addition, you can enter a table name in the search box in the top-left corner and click **Query** to search for the table.
![](https://main.qcloudimg.com/raw/3d0b2e2912854b8b777c5fba2559fc77.png)
### Viewing table details
To enter a table's details page, on the table-level monitoring overview page, click **Details** in the **Operation** column of the desired table. 
The details page can display the number of read/write requests and size of store (including MemStore and storeFile) of the selected table in the dimension of the entire table or node. You can switch between nodes by using the drop-down list in the top-left corner.

