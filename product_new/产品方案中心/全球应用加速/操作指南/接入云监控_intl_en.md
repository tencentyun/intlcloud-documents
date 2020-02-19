## Scenario
Alarm rules can be configured in Cloud Monitoring. An alarm is triggered immediately when the alarm condition configured for the acceleration connection is reached.

## Directions
Log into the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/policylist/add), and follow the steps below:

### Monitoring acceleration connections
1. In the left sidebar, choose **Alarm Policy**. Click **Add** to enter the **Create Policy** page.
2. In **Policy Type**, select **GAAP**>**Channel**.
![](https://main.qcloudimg.com/raw/21a41c74d5282d4e55cc340824b79e37.png)
In **Trigger Condition**, click **Add**. You can add multiple trigger conditions, including **inpacket**, **outpacket**, **inbound bandwidth**, and other alarm conditions. You can configure specific policies as needed. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/3abe12f5d1702b4a1e581ccab98a7d00.png)

### Monitoring Listeners
1. In the left sidebar, choose **Alarm Policy**. Click **Add** to enter the **Create Policy** page.
2. In **Policy Type**, select **GAAP**>**Listener**.
![](https://main.qcloudimg.com/raw/442694974704ab4e980785107a5c63a5.png)
3. **Trigger Conditions** currently supports alarms for **Origin server status**. If the status of the origin server becomes abnormal, the Cloud Monitor triggers an alarm. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/0bef097363d0587dcdf3ad7eb22c272f.png)


