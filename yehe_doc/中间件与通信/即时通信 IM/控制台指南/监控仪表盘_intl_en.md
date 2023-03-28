
The Chat console provides you with data statistics and analysis features. You can log in to the [Chat console](https://console.cloud.tencent.com/im), click the target app card, and choose **Monitoring Dashboard** in the left sidebar to view app data such as user base, message activity, group size, and real-time monitoring data.
>?Normally, the data is updated at 10:00 every morning. In the event that the data is 0 or not updated, check whether the SDKAppID produced relevant data (for example, whether there are new registered users) in the specified period. If data was produced but not updated, just wait a while for it to be updated.

## Daily Statistics
### User base
1. On the **Daily Statistics** page, click the **User Base** tab.
2. In the overview area, you can view the following data:
 - Peak DAU of the current month: the peak DAU of the current month as of yesterday. This data is 0 on the first day of every month.
 - Cumulative number of users as of yesterday: the cumulative number of UserIDs registered with the SDKAppID as of yesterday.
 - Number of new registered users yesterday: the number of new UserIDs registered with the SDKAppID yesterday.
3. Select 7 days, 14 days, or 30 days, or specify a period.
4. In the data trend area, you can view the **DAU and New Users** or **Total Registered Users** chart for the selected period. 
5. In the data details area, you can view the data of each day for the selected period, including DAU, DAU (day-over-day), total users, total users (day-over-day), new registered users, and new registered users (day-over-day). You can also export these data by clicking **Export as CSV**.

![](https://qcloudimg.tencent-cloud.cn/raw/8955bab2cd460bda09e5e63b95c459a8.png)

### Message activity
1. On the **Daily Statistics** page, click the **Message Activity** tab.
2. In the overview area, you can view the following data:
 - Number of one-to-one messages yesterday: the total number of C2C chat upstream messages under the SDKAppID yesterday.
 - Number of group messages yesterday: the total number of upstream messages in private group, public group, and chat room chats under the SDKAppID yesterday.
3. Select 7 days, 14 days, or 30 days, or specify a period.
4. In the data trend area, you can view the **C2C** or **Ordinary Group** message count charts for the selected period.
5. In the data details area, you can view the data of each day for the selected period, including message count, message count (day-over-day), message senders, message senders (day-over-day), offline pushes, and offline pushes (day-over-day). You can also export these data by clicking **Export as CSV**.

![](https://qcloudimg.tencent-cloud.cn/raw/ec4654a69a3a28d49e7bcec279c2b0cd.png)

### Group size
1. On the **Daily Statistics** page, click the **Group Scale** tab.
2. In the overview area, you can view the **Current Month's Peak Groups** data, which is the peak group count of the current month as of yesterday under the SDKAppID. This is 0 on the first day of every month.
3. Select 7 days, 14 days, or 30 days, or specify a period.
4. In the data trend area, you can select a data item to view the trends of **New**, **Total**, or **Active** groups within the selected time range.
5. In the data details area, you can view the data in each day for the selected period, including new groups, new groups (day-on-day), active groups, active groups (day-on-day), peak group count, and peak group count (day-on-day). You can also export these data by clicking **Export as CSV**.

![](https://qcloudimg.tencent-cloud.cn/raw/60e2a0f17181b9a16d883a9fb78da993.png)

## Real-Time Monitoring
>?The real-time monitoring feature is in beta testing and is still being updated in iteration mode. If you have any feedback or suggestions, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E5%8D%B3%E6%97%B6%E9%80%9A%E4%BF%A1%20IM&level3_id=237&radio_title=%E7%99%BB%E5%BD%95%E5%8F%8A%E5%A4%9A%E7%AB%AF%E5%9C%A8%E7%BA%BF%E9%97%AE%E9%A2%98&queue=3235&scene_code=27293&step=2).

1. In the left sidebar, choose **Monitoring Dashboard** > **Real-Time**.
2. In the overview area, you can view **Current Online Users**, **One-to-One Messages Today**, **Ordinary Group Messages Today**, and **Audio-Video Group Messages Today**.
3. In the detailed monitoring data area, data of the 24 hours of the natural day is displayed on the timestamp by default. When the mouse cursor points to the data chart area, you can use the scroll wheel to zoom in the timestamp to view details, drag the timestamp left and right to view the data before and after the time, and click the legend below the timestamp to hide or show the corresponding value in the chart.
 - In the login monitoring area, you can view the login times and login success rate of each client.
>?Currently, only the login data reported by 4.8.10 or later Chat SDKs for iOS, Android, Windows, and macOS will be displayed. You are advised to upgrade to the [latest version of SDK](https://intl.cloud.tencent.com/document/product/1047/33996).
>
![](https://qcloudimg.tencent-cloud.cn/raw/44981d16aeec09991b8147e9d3ebaad2.png)
 - In the message monitoring area, you can view the number of one-to-one or group messages sent by each client and the message sending success rate.
>?Currently, only the login data reported by 4.8.10 or later Chat SDKs for iOS, Android, Windows, and macOS will be displayed. You are advised to upgrade to the [latest version of SDK](https://intl.cloud.tencent.com/document/product/1047/33996). Currently, the web SDK does not support collecting message statistics by chat type.
>
 - In the callback monitoring area, you can view the number of callbacks and the callback success rate.
 - In the RESTful API monitoring area, you can view the number of RESTful API requests and the request success rate.
 - In the offline push monitoring area, you can view the number of offline push times and the push success rate.
    ![](https://qcloudimg.tencent-cloud.cn/raw/c57d688deafc6dd8049b05dd3480ee06.png)



