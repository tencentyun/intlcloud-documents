You can configure alarm rules for the connection, dedicated tunnel and direct connect gateway on the Cloud Monitor console. When an alarm rule is triggered, you will receive notifications via the channel you specified, helping you take appropriate measures.

## Directions
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and choose **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. Click **Create** on the **Alarm Policy** page.
3. Configure a new alarm policy as instructed below.
 1. Fill in **Policy Name** and **Remarks**. Select **Physical Dedicated Line**, **Dedicated Line Channel** or **Direct Connect Gateway** for **Policy Type** as needed.
    
 2. Choose a project to which the alarm policy belongs. Each project supports creating a maximum of 300 alarm policies.
 3. Select the alarm object.
     - If you select**All Objects**, the alarm policy will be associated with all instances under the current account.
     - If you select **Instance ID** and select instances in the pop-up window, the alarm policy will be associated with the selected instances.
    - If you select **Instance Group**, the alarm policy will be associated with the selected instance group. If there is no available instance group, you can click **Create instance group** to configure one.
 4. Configure the trigger condition using either of:
    - Template
     Click **Select template** and select a configured template in the drop-down list.
 >? You can click **Add Trigger Condition Template** to configure a new trigger condition template. For more information about the configurations, please see [Configuring Trigger Condition Template](https://intl.cloud.tencent.com/document/product/248/38911). If the new template is not displayed in the list, click the refresh icon.
    - Manual configuration
  Select **Configure manually** and configure **Metric Alarm** and **Event Alarm** as needed.
       - Set the trigger condition. You can click **Add Metric** to configure a new metric. For more information about metric alarms, see [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403).
 For example, if you choose **BandwidthIn** metric and configure as follows: **statistical period: 1 minute**, **>**, **100 Mbps**, **at 2 consecutive data points**, and **Alarm once a day**, then the inbound bandwidth data will be collected once every minute. An alarm will be triggered once a day if the inbound bandwidth of a connection, dedicated tunnel or direct connect gateway exceeds 100 Mbps for two consecutive minutes.
 >? Click **Add Metric** to configure a new trigger condition. You can choose to trigger an alarm when any or all conditions are met.
 >
       - Select a specific event such as DirectConnectDown for the event alarm. You can click **Add Event** to configure a new event alarm. For more information about event alarms, see [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403).
 >? Click **Add Event** to configure a new event alarm.
4. Configure alarm notification.
The notification template allows you to configure alarm recipients. You can click **Select template** and select an existing template, or click **Create Template** to configure a new template as prompted.
5. (Optional) Configure the API callback.
   1. Click **Create Template**. In the pop-up window, click **For more configurations, please go to notification template page**.
   2. On the **New Notification Template** page, complete the notification template configurations, enter a URL accessible over public networks as the API callback address (domain name or IP[:port][/path]), and click **Complete**.
   3. Go to the **Alarm Policy** page and select the alarm notification template you’ve just created.
   Then Cloud Monitor will push the alarm information to this address in time.
6. After the configuration is complete, click **Complete**.

## Manage Alarm Policies
Once an alarm policy is created, you can enable, disable, copy, or delete it on the console.
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm Configuration** > **Alarm Policy** to access the **Alarm Policy** page.
2. Perform the following steps as needed.
   - To enable or disable an alarm policy, locate it in the list, and toggle the switch in the **Alarm On-Off** column.
   - To copy an alarm policy, locate it in the list, click **Copy** in the **Operation** column, modify the policy as needed in the pop-up window, and click **Complete**.
   - To view historical alarm data, locate the alarm policy and click **Alarm Records** in the **Operation** column.
   - To delete an alarm policy, locate it in the list, click **Delete** in the **Operation** column, and click **Confirm** in the pop-up dialog box.

