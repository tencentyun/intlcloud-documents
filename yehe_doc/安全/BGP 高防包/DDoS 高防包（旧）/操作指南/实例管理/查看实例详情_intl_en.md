## Operation Scenarios
You can view the basic information (such as the base protection bandwidth and running status) and configure elastic protection of all purchased Anti-DDoS Pro instances in the Anti-DDoS Console.
## Directions
This example shows you how to view the details of the single IP instance `bgp-000006ee` in the Guangzhou region.
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Pro** > **Resource List** on the left sidebar, click **Single IP Instance**, select **South China (Guangzhou)** in the region selection box, find the single IP instance named "bgp-000006ee", and click **ID/Single IP Instance Name** to view the instance information.
3. On the pop-up page, you can view the following information
**Parameter description:**
  - **Basic Information:**
		- **Instance name**
This is the name of the Anti-DDoS Pro instance for easier instance identification and management. You can set a custom instance name containing 1–20 character of any type as desired. For detailed directions, please see [Setting Resource Name](https://intl.cloud.tencent.com/document/product/1029/31755).
		- **Region**
 This is the **region** selected when the Anti-DDoS Pro instance is purchased.
		- **Bound IP**
This is the actual IP of the business protected by the Anti-DDoS Pro instance.
		- **Base protection bandwidth**
This is the base protection bandwidth of the Anti-DDoS Pro instance, i.e., the **base protection bandwidth** selected when the instance is purchased. If elastic protection is not enabled, this will be the maximum protection bandwidth of the instance.
		- **Current status**
This is the current status of the Anti-DDoS Pro instance, such as **Running**, **Cleansing**, and **Blocked**.
		- **Expiration time**
This is calculated based on the **purchase duration** selected when the instance is purchased and the order is paid, which is accurate to second. Tencent Cloud will send expiration and renewal reminders to the account creator and all collaborators through internal message, SMS, and email within 7 days before the instance expires.
		- **Tag**
This is the tag name of the Anti-DDoS Pro instance, which can be edited and deleted.
 - **Elastic protection information**
		- **Current status**
This indicates whether elastic protection is enabled. If it is not enabled when you purchase the Anti-DDoS Pro instance, you can **enable** it in a self-service manner when using the instance. For detailed directions, please see [Configuring Elastic Protection](https://intl.cloud.tencent.com/document/product/1029/31756).
		- **Elastic bandwidth**
This parameter is visible only if elastic protection is enabled, which is the maximum elastic protection bandwidth of the Anti-DDoS Pro instance. You can adjust it as instructed in [Configuring Elastic Protection](https://intl.cloud.tencent.com/document/product/1029/31756) as needed at any time.


