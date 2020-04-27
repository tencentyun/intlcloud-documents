## Operation Scenarios

Alarm recipient groups determine who can receive alarm notifications. You can put people related to the same alarm in the same group. When the alarm is triggered, people in the group will receive the corresponding alarm notification. The following describes how to add an alarm recipient group for an alarm policy.

## Directions

### Adding an alarm recipient group

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor).

2. In the left sidebar, choose **Alarm Configuration** > **Alarm Policy** to access the alarm policy management page.

3. Find the policy to which you want to add a recipient group and click on its name to access the details page.

4. Scroll down, find the **Alarm Recipient Object** configuration item, and click **Edit**. The alarm recipient configuration box will pop up.
   
   ![](https://main.qcloudimg.com/raw/7463c810ee3ba0bd8cfbabdcbc187cb6.png)
   
5. Click **Add Recipient Group** and the user group module in the CAM Console will be displayed on a new page. For more information on how to create a user group, please see [User Group Management](https://intl.cloud.tencent.com/document/product/598/10599). For more information on how to create a new user, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

6. After creating the user and user group, return to and refresh the alarm policy page of Cloud Monitoring. In the alarm recipient group module, select the user group you just created.

7. You can select receipt channels as needed.

8. After completing the configuration, click **Save** to add the user group to the alarm policy. The user group can then receive alarm notifications sent by the alarm policy.

> Basic cloud resource monitoring and custom monitoring have different sub-account permissions. A sub-account has no permission to query information about other sub-accounts by default. You can grant the relevant query permission if needed.
>  - If a sub-account needs permission to view user groups for basic Tencent Cloud services monitoring, you need to log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) with the root account and grant the `QcloudMonitorFullAccess` permission to the sub-account (if only this permission is granted, the alarm recipients for services monitoring will not be synced with that for custom monitoring).
> - If a sub-account needs permission to view user groups for custom monitoring, you need to log in to the [CAM module](https://console.cloud.tencent.com/cam/policy) with the root account and grant the `QcloudCamReadOnlyAccess` permission to the sub-account.

### Managing alarm receipt methods

- Currently, alarm notifications can be sent via email, SMS, and WeChat. You can modify users' phone numbers, email addresses, and WeChat accounts in the [CAM Console](https://console.cloud.tencent.com/cam) and decide how they will receive alarm notifications. For more information on how to modify user information, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
You can set alarm notifications to be received via WeChat.

### Unsubscribing from an alarm

If you do not want a user to receive alarm notifications for a particular policy, you can cancel the user's alarm subscription by the two following ways:

- In the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor), disassociate the alarm recipient group of the target user from the corresponding policy. 
- In the [CAM Console](https://console.cloud.tencent.com/cam), delete the corresponding user group or user.
