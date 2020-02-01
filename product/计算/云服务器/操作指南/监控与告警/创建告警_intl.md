## Scenario

You can create an alarm to get notified for status change of Tencent Cloud services. The created alarm determines whether to trigger a notification according to the comparison results between a monitored metric and a specific threshold at regular interval.
You can take precautionary or remedial measures in a timely manner when an alarm is set off by status changes. Therefore, creating a valid alarm can help you improve your application's robustness and reliability.
Each alarm policy is a set of triggering conditions with the logic relationship "or", that is, an alarm is triggered when any of the conditions is met. The alarm is sent to all users associated with the alarm policy. Upon receiving the alarm, the user can view the alarm and take appropriate actions in time.

## Prerequiste
Log in to [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview)


## Directions
### Create Alarm
1. On the left, choose **Alarm Configuration** > **Alarm Policy**
2. Click **Add** button.
3. On the new page, enter a policy name and select alarm triggering conditions. The triggering condition is a semantic condition consisting of **metric**, **comparison relation**, **threshold**, **measurement period**, **number of continuous periods** and **repeated notification policy**.
4. Click **Complete**

### Associating an Object
1. On the left, choose **Alarm Configuration** > **Alarm Policy**
2. On the alarm policy list page, click the newly created alarm policy. On the details page, click **Add Object** button and select the cloud server you want to associate, and then click **Apply** to submit.

### Set an Object to Receive Alarms
1. On the left, choose **Alarm Configuration** > **Alarm Policy**
2. Click the created alarm policy to enter its details page, in **Alarm Recipient Object** part, select the recipient groups that need to be edited.




