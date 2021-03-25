## Scenario
You can create an alarm to trigger and send alarm notifications when Tencent Cloud services change statues. The created alarm can determine whether to trigger alarm notifications based on comparison between a monitoring metric and a specified threshold at every interval.
Each alarm policy is a set of trigger conditions with the logic relationship "or", that is, an alarm is triggered when any of the conditions is met. The alarm is sent to all users associated with the alarm policy. Upon receiving the alarm, you can view it and take appropriate actions in time. Creating an alarm can help you increase application reliability. For more information on alarms, see [Create Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38908).

## Prerequisites

1. Log in to [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).

## Directions
### Create alarms
1. On the left sidebar, click **Alarm Configuration** > **[Alarm Policy](https://console.cloud.tencent.com/monitor/policylist)** to enter the alarm policy management page.
2. Click **Add** to create a new policy.
3. On the “Create Policy” page, enter the policy name, select the policy type and alarm object, and configure the trigger condition.
The trigger condition is a semantic condition consisting of **metric**, **comparison**, **threshold**, **statistical period**, **continuous periods** and **repeat notification policy**.
4. Click **Complete**.

### Associate Objects
1. On the left sidebar, click **Alarm Configuration** > **[Alarm Policy](https://console.cloud.tencent.com/monitor/policylist)** to enter the alarm policy management page.
2. Click the newly created alarm policy to enter the alarm policy management page.
3. Click **Add Object** on the alarm policy management page.
4. In the pop-up “Associate Alarm Object” window, select the CVM you want to associate with, and then click **Apply**.

### Configure alarm recipient objects
1. On the left sidebar, click **Alarm Configuration** > **[Alarm Policy](https://console.cloud.tencent.com/monitor/policylist)** to enter the alarm policy management page.
2. Click the newly created alarm policy to enter the alarm policy management page.
3. Locate **Alarm Recipient Object* on the alarm policy management page, and click **Edit**.
4. In the pop-up “Alarm Recipient Object” window, select the user groups you want to notify and click **Save**.



