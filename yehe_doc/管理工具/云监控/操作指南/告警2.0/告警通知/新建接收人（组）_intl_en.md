## Overview

Alarm recipients/groups determine who can receive alarm notifications. You can put people related to the same alarm in the same group. When the alarm is triggered, people in the group will receive the corresponding alarm notification. The following describes how to add an alarm recipient group for an alarm policy.

## Directions

### Adding alarm recipient

1. Log in to the CM console and go to [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Click the name of the policy for which to add users to enter the alarm policy modification page.
3. In the alarm notification module, click **Create Template** to pop up the notification template creation window.
4. In the **Recipient Object** drop-down list, select the **User Group** type and click **Add Recipients** on the right of the text box to enter the user list page.
5. You can create either a sub-account or a message recipient as needed.
	- **Create a sub-account**: the created user can have programming access, log in to the Tencent Cloud console, and receive message notifications. For more information on how to create a sub-account, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
	- **Create a message recipient**: the created user can receive messages only but cannot have programming access or log in to the Tencent Cloud console. For more information on how to create a message recipient, please see [Creating a Message Recipient](https://intl.cloud.tencent.com/document/product/598/13667).
6. After creating the user, go back to the notification template creation pop-up window, refresh it, and select the newly created user in the recipient object list.
7. You can name the template and select the notification method as needed.
8. After completing the configuration, click **Save** to add the user to the alarm policy. The user can then receive alarm notifications sent by the alarm policy.
   ![](https://main.qcloudimg.com/raw/0a7a5fa7773b1d29eecf268e973c8103.png)

### Adding alarm recipient group

1. Log in to the CM console and go to [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Click the name of the policy for which to add users to enter the alarm policy modification page.
3. In the **Recipient Object** drop-down list, select the **User Group** type and click **Add Recipient Group** on the right of the text box to enter the user group list page.
4. Click **Create** to enter the user group creation page. Create a user group as instructed in [User Management](https://intl.cloud.tencent.com/document/product/598/10599), complete other configurations of the notification template, and save the template.
5. After creating the user group, go back to the notification template creation pop-up window, refresh it, and select the newly created user group in the recipient object list.
6. You can name the template and select the receiving channel as needed.
7. After completing the configuration, click **Save** to add the user group to the alarm policy. The user group can then receive alarm notifications sent by the alarm policy.
   ![](https://main.qcloudimg.com/raw/38004047ade05096fc74769e1e762176.png)
> ?If the sub-account cannot access Cloud Monitor or other Tencent Cloud service resources after the recipient or recipient group is created, please grant the sub-account permissions as instructed in [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/248/36744).

### Unsubscribing from alarm

If you do not want a user to receive alarm notifications of a policy, you can cancel the user's alarm subscription in the following ways:

- In [Cloud Monitor console > Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy), remove the alarm notification template associated with the user from the corresponding policy. 
  ![](https://main.qcloudimg.com/raw/4f6184d53dffbf7a583f24955b71ea8a.png)
- In the [CAM console](https://console.cloud.tencent.com/cam), delete the target user group or user.
