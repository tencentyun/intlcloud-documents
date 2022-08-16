
You can view the basic information (such as the base protection bandwidth and running status) and elastic protection configuration of your purchased Anti-DDoS Advanced instances in the console.

## Directions

The following takes the Anti-DDoS Advanced instance "bgpip-000002jf" as an example.
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package). Select **Anti-DDoS Advanced (New)** > **Instance List** on the left sidebar. Select a target instance and click the ID to view the instance details. If you have many instances, you can use the search box in the top right corner to filter results.
![](https://qcloudimg.tencent-cloud.cn/raw/c174ccf351d369aaa1e0470c97278bfa.png)
3. On the pop-up page, you can view the following information:
![](https://main.qcloudimg.com/raw/77f50dfce86cccc4dc24dd4d3b5cd331.png)
  - **Anti-DDoS Advanced Name**: Name of the Anti-DDos Advanced instance, which allows you to identify and manage instances. You can create a instance name containing 1–20 characters of any type as desired.
  - **Destination IP**: The IP address of Anti-DDoS Advanced instance. The IP address may change.
>! To avoid DNS resolution failure, you are recommended to change the DNS resolution address to the assigned CNAME.

   - **Region**: Select a region when purchasing an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/15483).
   - **CNAME**: CNAME of the Anti-DDoS Advanced instance. The CNAME will be resolved to an instance IP that can forward cleansed traffic to the origin server.
>! To avoid DNS resolution failure, you are recommended to change the DNS resolution address to the assigned CNAME.

  - **Base protection bandwidth**: Base protection bandwidth of the Anti-DDoS Advanced instance, that is, the **base protection bandwidth** you select when you [purchase](https://intl.cloud.tencent.com/document/product/297/15483) the instance. If the elastic protection is disabled, the base protection bandwidth is the maximum bandwidth of the instance.
  - **Current Status**: Current status of the Anti-DDoS Advanced instance, such as **Running**, **Cleansing**, and **Blocking**.
  - **Expiration Time**: It is calculated based on the purchase duration selected when the instance is [purchased](https://intl.cloud.tencent.com/document/product/297/37241) and the time when the order is paid, which is accurate to second. Tencent Cloud will send expiration and renewal reminders to the account creator and all collaborators through Message Center, SMS, and email within 7 days before the instance expires.
	 - **Tag**: Tag of the Anti-DDoS Advanced instance, which can be edited and deleted.
	 - **Intermediate IP Range**: IP that forwards cleansed traffic back to the origin server.


