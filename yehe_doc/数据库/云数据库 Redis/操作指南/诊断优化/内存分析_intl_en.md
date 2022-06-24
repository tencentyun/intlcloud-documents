## Feature Description

If slots are sharded unevenly in the cluster mode of TencentDB for Redis, a data or query skew may occur. In this case, some Redis nodes with big keys may use more memory and ENI resources, causing Redis blockage.
The memory analysis feature mainly analyzes big keys stored in the database. It dynamically displays the change trend of the instance's memory utilization and collects the statistics of memory utilization, element quantity and length, and expiration time of top 100 big keys in real time. This helps you quickly identify big keys for splitting or clearing after expiration, so you can promptly optimize the database performance and avoid business blockage caused by high memory usage of big keys.

## Big Key Analysis Data Interpretation

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Performance Optimization**.
3. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/949f57e9a37830d95cd55836b0f6dc33.png)
4. Select the **Memory Analysis** tab to view the analysis data of big keys.
![](https://qcloudimg.tencent-cloud.cn/raw/0e4ec17b4cc9193373265eb2506eda02.png)
 - **Memory utilization**
   On the **Big Key Analysis** page, the change trend of the instance's memory utilization in the last 30 days is displayed by default. You can select a time period on the timeline to view the specific change trend of memory utilization.
 - **Top 100 big keys**
   Select a data type in the **Data Type** drop-down list to view the information of the top 100 big keys by memory usage, element quantity, max element length, average element length, and expiration time.
    - **Top 100 Big Keys (by MEM Usage)**: Top 100 big keys by memory usage from high to low.
    - **Top 100 Big Keys (by Element Quantity)**: Top 100 big keys by element quantity from high to low.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/5bcc95222edcbe371b9fdf5b21786c7e.png)
 - **Quickly find big keys**
   In the monitoring view of memory utilization, the change trend of the instance's memory utilization in the last 30 days is displayed by default. If you find that the memory utilization on a certain date is high, you can click the date on the date axis, then the time column will be fixed, and the information of big keys of that date will be displayed in the list of the top 100 big keys at the bottom, so you can quickly identify big keys with a high memory utilization.

## Creating Ad Hoc Analysis of Big Key

1. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list. Then, select the **Memory Analysis** > **Ad Hoc Analysis of Big Key** tab.
![img](https://qcloudimg.tencent-cloud.cn/raw/a0054deb489676437828c90008589281.png)
2. Click **Create Task**, and DBbrain will fetch the last backup of the database for automatic analysis. You can view the analysis progress on the progress bar in the task list.
3. After the analysis is completed, click **View** in the **Operation** column to view the result of big key analysis. If the big key needs to be deleted, click **Delete** in the **Operation** column in the task list.
4. View the analysis result in the **Analysis Result** panel.


