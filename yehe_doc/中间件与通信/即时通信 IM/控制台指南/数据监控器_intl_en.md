
The IM console provides you with data statistics and analysis features. You can log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Statistics** in the left sidebar to view app data such as the user base, message activity, group size, and real-time monitoring data.
>? Normally, data is updated at 10:00 a.m. every day. If the data is 0 or not updated, check whether the SDKAppID produced relevant data (for example, whether there are new registered users) in the specified period. If data was produced but not updated, wait a while for it to be updated.

## Daily Data Statistics
### User base
1. On the **Daily Statistics** page, select the **User Base** tab.
2. In the overview area, you can view the following data:
 - Peak DAU in the current month: The peak DAU for the current month as of yesterday. This metric is 0 on the first day of every month.
 - Cumulative number of users as of yesterday: The cumulative number of UserIDs registered with the SDKAppID as of yesterday.
 - Number of new registered users yesterday: The number of new UserIDs registered with the SDKAppID yesterday.
3. Select 7 days, 14 days, or 30 days, or specify a period.
4. In the data trend area, you can view the **DAU and New Users** or **Total Registered Users** chart for the selected period. 
6. In the data details area, you can view the data of each day for the selected period, including DAU, DAU (day-over-day), total users, total users (day-over-day), new registered users, and new registered users (day-over-day). You can also export these data by clicking **Export as CSV**.

![](https://qcloudimg.tencent-cloud.cn/raw/8955bab2cd460bda09e5e63b95c459a8.png)

![](https://qcloudimg.tencent-cloud.cn/raw/155b38a067353e875d5456d2827df548.png)

### Message activity

1. On the **Daily Statistics** page, select the **Message Activity** tab.
2. In the overview area, you can view the following data:
 - Number of one-to-one messages yesterday: The total number of C2C chat upstream messages under the SDKAppID yesterday.
 - Number of group messages yesterday: The total number of upstream messages in private groups, public groups, and chat rooms under the SDKAppID yesterday.
3. Select 7 days, 14 days, or 30 days, or specify a period.
4. In the data trend area, you can view the **C2C** or **Ordinary Group** message count charts for the selected period.
5. In the data details area, you can view the data for each day for the selected period, including the message count, message count (day-over-day), message senders, message senders (day-over-day), offline pushes, and offline pushes (day-over-day). You can also export these data by clicking **Export as CSV**.

![](https://qcloudimg.tencent-cloud.cn/raw/ec4654a69a3a28d49e7bcec279c2b0cd.png)
![](https://qcloudimg.tencent-cloud.cn/raw/648156a183114f2bdcf8ca30909ad6ec.png)

### Group size

1. On the **Daily Statistics** page, select the **Group Size** tab.
2. In the overview area, you can view **Current Month's Peak Groups**, which is the peak group count in the current month as of yesterday under the SDKAppID. This is 0 on the first day of every month.
3. Select 7 days, 14 days, or 30 days, or specify a period.
4. In the data trend area, select data items to view the **New**, **Total**, or **Active** group count charts for the selected period.
5. In the data details area, you can view data of each day for the selected period, including new groups, new groups (day-over-day), active groups, active groups (day-over-day), peak group count, and peak group count (day-over-day). You can also export these data by clicking **Export as CSV**.
![](https://qcloudimg.tencent-cloud.cn/raw/60e2a0f17181b9a16d883a9fb78da993.png)
![](https://qcloudimg.tencent-cloud.cn/raw/40071e2bac38b621658e459956d850dc.png)

## Real-Time Monitoring
>? The real-time monitoring feature is currently in the beta test phase. We are iterating and updating the feature. If you have any comments or suggestions, contact us through our QQ group (468195767) or [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E5%8D%B3%E6%97%B6%E9%80%9A%E4%BF%A1%20IM&level3_id=237&radio_title=%E7%99%BB%E5%BD%95%E5%8F%8A%E5%A4%9A%E7%AB%AF%E5%9C%A8%E7%BA%BF%E9%97%AE%E9%A2%98&queue=3235&scene_code=27293&step=2).

1. In the left sidebar, select **Statistics** > **Real-Time**.
2. In the overview area, you can view **One-to-One Messages Today**, **Group Messages Today**, and **Web/Mini Program Messages**.
3. In the monitoring data details area, the time axis displays 24-hour data by calendar day by default. When you hover the cursor over the data chart area, you can scroll the scroll bar to magnify the time axis to view details, drag the time axis leftwards or rightwards to view data at different time points, and click the legend below the time axis to hide or display values in the chart.
 - In the login monitoring area, you can view the number of logins and login success rate on different clients.
  >? Currently, only login data reported by iOS, Android, Windows, and Mac devices with SDK version 4.8.10 or later can be displayed. We recommend that you use the [latest SDK](https://intl.cloud.tencent.com/document/product/1047/33996).
  >

![](https://qcloudimg.tencent-cloud.cn/raw/44981d16aeec09991b8147e9d3ebaad2.png)
 - In the message monitoring area, you can view the number and success rate of one-to-one messages and group messages on different clients.
 - 
   >? Currently, only message data reported by iOS, Android, Windows, and Mac devices with SDK version 4.8.10 or later can be displayed. We recommend that you use the [latest SDK](https://intl.cloud.tencent.com/document/product/1047/33996). Web clients and Mini Program do not support message count statistics by chat type.
   >
 - In the callback monitoring area, you can view the number of callbacks and callback success rate.
 - In the RESTful API call monitoring area, you can view the number of RESTful API requests and the request success rate.
 - In the offline push monitoring area, you can view the number of offline pushes and the push success rate.

![](https://qcloudimg.tencent-cloud.cn/raw/c57d688deafc6dd8049b05dd3480ee06.png)
