You can configure alarm rules for the connection and dedicated tunnel on the Cloud Monitor console. When an alarm rule is triggered, you will receive notifications, which will allow you to take appropriate measures.

## Creating an Alarm Policy
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm Configuration** -> **Alarm Policy** to access the alarm policy configuration page.
2. Click **Create**.
3. Perform the following steps to configure a new alarm policy.
  4. Fill in **Policy Name** and **Remarks**. Select **Physical Dedicated Line** or **Dedicated Line Channel** for **Policy Type** as needed.
 2. Choose a project based on your needs. Each project supports creating a maximum of 300 alarm policies.
 3. Select the alarm object.
    - If you check **All Objects**, the alarm policy will be associated with all instances under the current account.
    - If you check **Select some objects**, the alarm policy will be associated with the selected instances.
    - If you check **Select instance group**, the alarm policy will be associated with the selected instance groups. You can click **Create instance group** to add instance groups.
 4. Use one of the following methods to configure the trigger condition.
- Trigger condition template
    This method allows you to select a configured template from the drop-down list.
>? You can click **Add Trigger Condition Template** to configure a new trigger condition template. For more information, see [Configuring Trigger Condition Templates](https://intl.cloud.tencent.com/document/product/248/32817). If the new template is not displayed in the list, click **Refresh**.

- Configure trigger condition
   This method requires configuring **metric alarm** and **event alarm** as needed.
 - Configure the trigger conditions for metric alarm. For more information about the metrics, see [Metric Alarms](https://intl.cloud.tencent.com/document/product/216/38403).
 For example, if you choose **BandwidthIn** metric and configure the following parameters: **Statistical Period 1 minutes**, **>**, **100 Mbps**, **Last for 2 periods**, and **Alarm once every 1 day**, then the inbound bandwidth data will be collected once every minute, and an alarm will be triggered once a day if the inbound bandwidth of a connection or dedicated tunnel exceeds 100 Mpbs for 2 consecutive minutes.
>? Click **Add** to configure a new trigger condition. You can select to trigger an alarm when any or all conditions are met.


 - Configure the event such as DirectConnectDown for the event alarm. For more information about the events, see [Event Alarms](https://cloud.tencent.com/document/product/216/48582).

 >? Click **Add** to configure a new event alarm.

4. Configure the alarm channel, including the recipient group, valid period, and receipt channel (email, object, and WeChat) as needed.
 >? Click **Add Recipient Group** to configure a new receipt group. For more information about the configuration, see [Creating Alarm Recipient Groups](https://intl.cloud.tencent.com/document/product/248/6217).


5. (Optional) Configure the API callback. Input the URL that is accessible over the public network as the callback API address (domain name or IP[:port][/path]), and the Cloud Monitor will push the alarm information to this address in time.
6. After the configuration is complete, click **Complete**.

## Managing an Alarm Policy

Once the alarm policy is created, you can enable, disable, copy, or delete it on the console.
1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm Configuration** -> **Alarm Policy** to access the alarm policy configuration page.
2. Perform the following steps as needed.
   - Locate the alarm policy that you want to enable or disable, toggle switch in the **Alarm On-Off** column.
   - Locate the alarm policy that you want to copy, click **Replication** in the **Operation** column, modify the policy as needed in the pop-up window, and click **Complete**.
   - Locate the alarm policy that you want to delete, click **Delete** in the **Operation** column, and click **OK** in the pop-up window to confirm the deletion.

