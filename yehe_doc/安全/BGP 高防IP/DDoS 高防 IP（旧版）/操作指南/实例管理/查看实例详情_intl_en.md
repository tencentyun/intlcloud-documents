## Operation Scenarios
You can view the basic information (such as the base protection bandwidth and running status) and configure elastic protection of all purchased Anti-DDoS Advanced instances in the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview).
## Directions
This document uses the Anti-DDoS Advanced instance "bgpip-0000020n" in Guangzhou as an example to describe how to view instance details.
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Advanced** > **Asset List** on the left sidebar, and click **South China (Guangzhou)** in the region selection box. In the list below, click the Anti-DDoS Advanced instance whose ID is "bgpip-0000020n" to view its information.
2. On the pop-up page, you can view the following information:
**Parameter description:**
- **Basic information:**
		- **Name**
	This is the name of the Anti-DDoS Advanced instance for easier instance identification and management. You can set a custom instance name containing 1–20 character of any type as desired. For detailed directions, please see [Setting Resource Name](https://intl.cloud.tencent.com/document/product/297/34087).
	- **IP**
	This is the protective IP provided by the Anti-DDoS Advanced instance, which is used as the frontend IP of the real server to provide services.
	- **Region**
	This is the **region** selected when the Anti-DDoS Advanced instance is purchased.
	- **Forwarding target**
	This is the location of the real business server protected by the Anti-DDoS Advanced instance.
	- **Base DDoS protection bandwidth**
	This is the base protection bandwidth of the Anti-DDoS Advanced instance, i.e., the **base protection bandwidth** selected when the instance is purchased. If elastic protection is not enabled, this will be the maximum protection bandwidth of the instance.
	- **CC protection bandwidth**
	This is the capability of the Anti-DDoS Advanced instance to defend against sudden CC attacks.
	- **Current status**
	This is the current status of the Anti-DDoS Advanced instance, such as **Running**, **Cleansing**, and **Blocked**.
	- **Expiration time**
	This is calculated based on the **purchase duration** selected when the instance is purchased and the order is paid, which is accurate to second. Tencent Cloud will send expiration and renewal reminders to the account creator and all collaborators through internal message, SMS, and email 7 days before the instance expires.
	- **Intermediate IP range**
	This is the information of the intermediate IP range in the region of the current Anti-DDoS Advanced instance.
- **Elastic protection information**
		- **Current status**
	This indicates whether elastic protection is enabled. If it is not enabled when you purchase the Anti-DDoS Advanced instance, you can enable it in a self-service manner when using the instance. For detailed directions, please see [Configuring Elastic Protection](https://intl.cloud.tencent.com/document/product/297/34088).
	- **Elastic bandwidth**
	This is the maximum elastic protection bandwidth of the Anti-DDoS Advanced instance. You can [adjust it](https://intl.cloud.tencent.com/document/product/297/34088) as needed at any time.
>This parameter is visible only after elastic protection is enabled.

