## Overview
You can configure alarm policies for SCF through [Cloud Monitor](https://console.cloud.tencent.com/monitor/myalarm) to monitor the execution status of functions.
Currently, the monitoring metrics that can be configured for SCF include runtime, invoke count, and error count. For the full list of supported metrics, see [Descriptions of monitoring metrics](https://intl.cloud.tencent.com/document/product/583/32739). In addition, you can select user groups that will receive alarms through email, SMS, or WeChat.

## Directions

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Functions** on the left sidebar.
2. On the **Functions** page, click the target function name to enter the function details page.
3. Select **Monitoring information** on the left and click **Set alarm** on the details page as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mNL2280_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219161556.png)
4. On the **Create alarm policy** page, configure a new alarm policy as detailed below:
	- **Policy Name**: Custom.
	- **Monitoring Type**: Select **Tencent Cloud services**.
	- **Policy Type**: Select **Function/Version** or **Function/Alias**.
	- **Alarm Object**: Select the functions for which to apply the policy as needed. If **Instance ID** is selected, the region will be set to Guangzhou by default. You can view corresponding functions in different regions.
	For more information on detailed alarm policy configuration, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
5. Click **Complete**, and you can see the configured policy in **Alarm Management** > **[Policy Management](https://console.cloud.tencent.com/monitor/alarm2/policy)** and choose to enable/disable it at any time.

