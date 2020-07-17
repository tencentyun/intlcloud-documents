## Overview

Here's an example to show how you can configure an alarm. Assume that you want to send an SMS alarm to the number `12345678888` when the CPU utilization of CVM instance `ins-12345678` (in Guangzhou) `exceeds 80%` in `2` consecutive five-minute periods.

## Procedure

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Alarm Configuration** -> **Alarm Policy** to access the management page.
3. Click **Add** and configure the following options.
4. Configure the policy name and other basic options.
	- Policy Name: CPU alarm
	- Policy Type: CVM-basic monitoring
5. Configure the alarm object. In the “Alarm Object” module, select “Select certain objects” and select the CVM instance.
   ![](https://main.qcloudimg.com/raw/02c60b7f7f8ed7f618a2a7eae9e77f61.jpg)
6. Configure trigger conditions. In the “Trigger Conditions” module, configure the following conditions.
	- Select “Configure trigger conditions”.
	- Select “Metric alarm”: `CPU utilization` `->` `80%` `5 minutes` `2 periods`
	- Alarm repetition period: `15 minutes`
  ![](https://main.qcloudimg.com/raw/cd5792a1cc2563815814f4d17b064ebb.jpg)
7. Configure alarm channels. Add an alarm recipient group (if you have not created one yet, click **Add Recipient Group** to create one).
![](https://main.qcloudimg.com/raw/8542ff5caae88f5e508efa8d34d83a37.jpg)
8. Click **Finish** to complete the alarm configuration.
9. At this point, if the CPU utilization of the instance exceeds 80% in 2 consecutive five-minute periods, the number `12345678888` will receive the alarm SMS sent from Tencent Cloud.
