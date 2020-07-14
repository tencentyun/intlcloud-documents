## Introduction
After you create an alarm policy, you need to bind certain alarm objects to the policy to specify which instance objects will trigger alarms when the alarm conditions are met.


## Directions

### Binding objects
1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to access the **Alarm Policy** page.
3. Find the policy with which you want to bind objects and click the alarm policy name to access its details page.
4. In the **Alarm Object** section, click **Add Object** after selecting the desired region and then select a corresponding product instance to bind an object to the policy.
![](https://main.qcloudimg.com/raw/2fc8bcdd282ccdbc5f238b7fe11f1f84.png)


### Unbinding objects

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to access the **Alarm Policy** page.
3. Find the policy with which you want to bind objects and click the alarm policy name to access its details page.
4. In the **Alarm Object** section, select the instance for which you want to remove a bound object. At the top of the **Alarm Object** section, click **Disassociate** to unbind the object from the alarm policy.
![](https://main.qcloudimg.com/raw/ac13a88715c947e67360066051fbdd36.png)
5. You can also click **Disassociate All** to unbind all objects from the alarm policy.