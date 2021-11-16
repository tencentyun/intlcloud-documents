
## Scenarios
To create a better user experience, alarm rules can be configured in Cloud Monitoring. An alarm is triggered immediately when the alarm condition configured for the acceleration connection is reached.

## Directions

Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) before taking the following procedures.

### Connection monitoring

1. Click **Alarm Policy** on the left sidebar. Click **Create** to enter the **Create Alarm Policy** page.
2. For **Policy Type**, select **GAAP** > **Channel**.
![](https://qcloudimg.tencent-cloud.cn/raw/f951241047178c919b8bfef1a3894133.png)
3. In the **Alarm Policy** section, add channels as needed for **Policy Object**.
   You can choose **Select template** or **Configure manually** for **Trigger Condition**.
   If you choose **Select template**, you can use the alarm policies that has been configured before. If there are no templates, you can create and configure a new template as follows. The template will be saved to the console for subsequent use.
	1. Click **Add Trigger Condition Template** to enter the template configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/121bf297151fd5d14463d2a9f39a5989.png)
	2. Click **Create**. In the pop-up window, configure the following trigger conditions:
		- **Template Name**: Enter a template name.
		- **Remarks**: Enter template remarks.
		- **Policy Type**: Select a monitoring service, such as **GAAP** > **Channel**.
		- Use preset trigger conditions: Select this option to enable preset trigger conditions for the corresponding monitored product.
		- Trigger condition: includes indicator alarm and event alarm. You can click **Add** to set multiple alarms.
	If you choose **Configure manually**, you can add multiple alarm trigger conditions as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/4ce5c2222f27a23a50e29b7d6e675a61.png)
4. In the **Configure Alarm Notification** section, click **Create Template**, create a template name and select a recipient object and channel.
>!The recipient object needs to be bound with a channel. Otherwise, you will not receive an alarm notification.
>
![](https://qcloudimg.tencent-cloud.cn/raw/96bc43097aed1a331162305ef08a6c61.png)
Click **Select template** to choose a template you need.
![](https://qcloudimg.tencent-cloud.cn/raw/4362a734429b1aadce77fd7b219358cb.png)

### Listener monitoring

1. Select **Alarm Policy** on the left sidebar. Click **Create** to enter the **Create Alarm Policy** page.
2. For **Policy Type**, select **GAAP** > **L4 Listener Origin Server Status**/**L7 Listener Origin Server Status**.
![](https://qcloudimg.tencent-cloud.cn/raw/31a0c004e5b18e3715f4b197791dc20f.png)
3. In the **Alarm Policy** section, select an object for **Policy Object**, and choose **Select template** or **Configure manually** for **Trigger Condition**. If you choose **Configure manually**, you can set a trigger condition to notify you that an origin server is found exceptional.
![](https://qcloudimg.tencent-cloud.cn/raw/d75fdfe6dc7394fb9bdcdcbd6672915f.png)
4. In the **Configure Alarm Notification** section, click **Create Template**, create a template name and select a recipient object and channel.
>!The recipient object needs to be bound with a channel. Otherwise, you will not receive an alarm notification.
>
![](https://qcloudimg.tencent-cloud.cn/raw/242dedea0ea3fb500e2c5cbf33ec449e.png)
Click **Select template** to choose a template you need.
![](https://qcloudimg.tencent-cloud.cn/raw/16a460eea88e69afbc2a3ca4e97f2d10.png)
