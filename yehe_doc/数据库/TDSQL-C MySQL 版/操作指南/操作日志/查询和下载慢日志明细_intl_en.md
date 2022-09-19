The slow log is used to record query statements that take more time than the specified value to execute in TDSQL-C for MySQL read-write and read-only instances. You can find out inefficient query statements to optimize by slow log details. TDSQL-C for MySQL allows you to download such details for easier analysis and optimization.

This document describes how to query and download slow log details.

## Querying a slow log
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Instance List** tab and click the ID of the target read-write or read-only instance to enter the instance details page.
4. On the instance details page, select **Operation Log** > **Slow Log Details**.
![](https://qcloudimg.tencent-cloud.cn/raw/7202fe1b441b538b8a70489ba665de14.png)
 - You can filter slow log details by time (all, today, yesterday, last 7 or 30 days, or custom time period).
 - You can query slow log details by field (client address, username, or database name) and export them into a list file.
 - You can query and sort the following details: execution time, SQL statement, client address, username, database, execution duration (s), lock duration (s), parsed rows, and returned rows.
 ![](https://qcloudimg.tencent-cloud.cn/raw/61ab4c7c3d983bc40357cc9d9fed7970.png)


## Downloading slow log details
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Instance List** tab and click the ID of the target read-write or read-only instance to enter the instance details page.
4. On the instance details page, select **Operation Log** > **Slow Log Details**.
5. Query the target slow log details by time or keyword and click **Export**.
![](https://qcloudimg.tencent-cloud.cn/raw/adfbe9b254ae09e30c7bc91e9aab1fb9.png)
6. In the pop-up window, select the file format and click **OK** for download.
![](https://qcloudimg.tencent-cloud.cn/raw/59416c33ca79c20138dac0d4f9c419cf.png)
 - You can export the filtered or retrieved results in CSV or native format (supported by open-source analysis tools).
    - CSV format: You can perform quick check and optimization. Below is the sample exported information:
    ![](https://qcloudimg.tencent-cloud.cn/raw/9b1e7f340335b349bc0be1598e7cbaed.png)
	- Native format: The exported file can be recognized by open-source analysis tools. Below is the sample exported information:
		![](https://qcloudimg.tencent-cloud.cn/raw/228aeb980008a577db2cec47832cea20.png)    
 - You can export up to 2,000 records at a time. To download more than 2,000 records, select a shorter time range and export a part of the records you need. Repeat the steps until all of the records are exported.
