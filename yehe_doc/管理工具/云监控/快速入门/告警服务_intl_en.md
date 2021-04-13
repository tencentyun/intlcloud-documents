This document describes the features and operation processes of the alarm management module.

## Feature Overview

Alarms are provided for monitoring metrics. You can create alarms to stay informed on status changes of certain metrics. The specific metrics will be monitored during a certain period of time, and alarms will be sent through channels such as WeChat and SMS at specified intervals based on the specified threshold.

## Use Cases

To prevent the normal operation of your system from being affected when a monitoring metric of your CVM instance reaches a certain value, you can configure alarm rules for these metrics, The alarm system can then automatically check the monitoring data and send alarm notifications to the admin when the monitoring data meets the configured conditions, which will help you stay informed of business exceptions and quickly solve them.

## Directions

### Creating an alarm

#### Step 1. Create an alarm contact

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. On the left sidebar, select **Users** > **User List** > **Create User** to access the sub-user creation page.
3. Select **Custom Create** > **Receive messages only**.
4. Enter the user information and click **Done**.
> For more information on how to manage users, please see [User Group Management](https://intl.cloud.tencent.com/document/product/598/10599).


#### Step 2. Create an Alarm Recipient Group

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam).
2. On the left sidebar, select **User Groups** > **Create User Group** to access the user group creation page.
3. Enter the user group name and click **Next**.
4. Select the associated policy. You can also choose to leave the associated policy empty. Once you are done, select **Next** > **Done** to create the user group.
5. In the user group list, find the user group you just created. In the "Operation" column on the right, click **Add User** and select the target users.
6. After adding the users, click **OK**.
> 
> - For more information on how to create user groups, please see [Creating User Groups](https://intl.cloud.tencent.com/document/product/598/33380).
> - Basic cloud resource monitoring and custom monitoring have different sub-account permissions. A sub-account has no permission to query information about other sub-accounts by default. You can grant the relevant query permission if needed.
>  - If a sub-account needs permission to view user groups for basic Tencent Cloud services monitoring, you need to log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) with the root account and grant the `QcloudMonitorFullAccess` permission to the sub-account (if only this permission is granted, the alarm recipients for services monitoring will not be synced with that for custom monitoring).
>  - If a sub-account needs permission to view user groups for custom monitoring, you need to log in to the [CAM module](https://console.cloud.tencent.com/cam/policy) with the root account and grant the `QcloudCamReadOnlyAccess` permission to the sub-account.


#### Step 3. Create an alarm policy
1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor).
2. On the left sidebar, select **Alarm Configuration** > **Alarm Policy** to access the alarm policy configuration page.
3. Click **Add** to configure an alarm policy.
   - Configure basic settings such as policy name, remarks, policy type, and project.
   - Set alarm objects.
   - Set alarm trigger conditions.
   - Set alarm channels.
4. After the above configurations, click **Complete**.
>For more information on alarm settings, please see [Creating Alarms](https://intl.cloud.tencent.com/document/product/248/38908).

### Viewing an alarm

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor).
2. On the left sidebar, click **Monitor Overview** to access the monitoring overview page and view alarms.
