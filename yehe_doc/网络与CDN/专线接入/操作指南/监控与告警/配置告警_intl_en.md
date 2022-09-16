You can configure alarm rules for the connection, dedicated tunnel and direct connect gateway on the Cloud Monitor console. When an alarm rule is triggered, you will receive notifications via the channel you specified, helping you take appropriate measures.

## Directions
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and choose **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. Click **Create** on the **Alarm Policy** page.
![]()
3. Configure a new alarm policy as instructed below.
 1. Edit **Policy name** and **Remarks**. Select **Connection**, **Dedicated tunnel** or **Direct connect gateway** for **Policy type** as needed.
<dx-alert infotype="explain" title="">
If **Direct connect gateway** is selected, the policy is VPC-based.
</dx-alert>
 <img src="" style="zoom:80%;" />
 2. Choose a project to which the alarm policy belongs. Each project supports creating a maximum of 300 alarm policies.
 3. Select the alarm object.
     - If you select **All objects**, the alarm policy will be associated with all instances under the current account.
     - If you select **Instance ID** and select instances in the pop-up window, the alarm policy will be associated with the selected instances.
     - If you select **Instance group**, the alarm policy will be associated with the selected instance group. If there is no available instance group, you can click **Create instance group** to configure one.
      ![]()
 4. Configure the trigger condition using either of:
    - Template
	 Click **Select template** and select a configured template in the drop-down list.
	  <dx-alert infotype="explain" title="">
	 You can click **Add trigger condition template** to configure a new trigger condition template. For more information about the configurations, please see [Configuring Trigger Condition Template](https://intl.cloud.tencent.com/document/product/248/38911). If the new template is not displayed in the list, click **Refresh**.
	 </dx-alert>
    - Manual configuration
    Set the trigger condition as needed after selecting **Manual configuration**. You can click **Add metric** to configure a new metric. For more information about metric alarms, see [Alarm Overview](https://intl.cloud.tencent.com/document/product/216/38403).
	  For example, if you choose **Inbound bandwidth** metric and configure as follows: **statistical period: 1 minute**, **>**, **100 Mbps**, **at 2 consecutive data points**, and **Alarm once a day**, then the inbound bandwidth data will be collected once every minute. An alarm will be triggered once a day if the inbound bandwidth of a connection, dedicated tunnel or direct connect gateway exceeds 100 Mbps for two consecutive minutes.
>?Click **Add metric** to configure a new trigger condition. You can choose to trigger an alarm when any or all conditions are met.
>
 ![]()
>?If you need to configure event alarms, see [Quickly Configuring Cloud Monitor Event Alarm Push](https://intl.cloud.tencent.com/document/product/1108/45202).
4. Configure alarm notification.
The notification template allows you to configure alarm recipients. You can click **Select template** and select an existing template, or click **Create template** to configure a new template as prompted.
![]()
5. (Optional) Configure the API callback.
   i. Click **Create template**. In the pop-up window, click **For more configurations, please go to notification template page**.
   ii. On the **New notification template** page, complete the notification template configurations, enter a URL accessible over public networks as the API callback address (domain name or IP[:port][/path]), and click **Complete**.
   iii. Go to the **Alarm policy** page and select the alarm notification template you’ve just created.
   Then Cloud Monitor will push the alarm information to this address in time.
6. Click **OK**.

## Managing Alarm Policies
Once an alarm policy is created, you can enable, disable, copy, or delete it on the console.
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm Configuration** > **Alarm Policy** on the left sidebar to access the **Alarm policy** page.
2. Perform the following steps as needed.
   - To enable or disable an alarm policy, toggle the switch in its **Alarm On-Off** column.
   - To copy an alarm policy, click **Copy** in its **Operation** column, modify the policy as needed in the pop-up window, and click **Complete**.
   - To view historical alarm data, locate the alarm policy and click **Alarm records** in the **Operation** column.
   - To delete an alarm policy, click **Delete** in its **Operation** column, and click **Confirm** in the pop-up dialog box.

