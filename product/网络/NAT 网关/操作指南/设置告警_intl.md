You can set an alarm for your NAT gateway to monitor its status.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), click **Products** -> **Monitor & Management** -> [**Cloud Monitoring**](https://console.cloud.tencent.com/monitor/overview) in the top navigation pane, click **My Alarms** -> [**Alarm Policy**](https://console.cloud.tencent.com/monitor/policylist) in the left pane, and then click **Add**.
2. Enter the alarm policy name, select **VPC** -> **NAT Gateway** for **Policy Type**, select an alarm object, set an alarm policy, select an Recipient Group and Alarm Channel, and then click **Complete**. At this point, you can view the alarm policy you set in the alarm policy list.
>**Note:**
>After an alarm policy is created, you must unbind all resources from it before you can delete it.

 ![1](https://main.qcloudimg.com/raw/4adfb60a91722bf4bf9b8c42310fe6ab.png)
3. **View alarm information**
After the alarm condition is triggered, you will receive the alarm via the selected alarm channel (SMS, Email, internal message, etc.). You also can click **My Alarms** -> **Alarm List** in the left navigation pane to view it. For more information about alarms, see [Alarm Configuration](/doc/product/248/1073).

