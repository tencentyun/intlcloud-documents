## 1. Console Login
Log in to the [GAAP console](https://console.cloud.tencent.com/gaap) and click **Platform Management** to enter the shared acceleration platform.

<img src="https://qcloudimg.tencent-cloud.cn/raw/d3113b122fd7ccccf5a46511eeadd139.png" width="530px">


## 2. Platform Management
### Creating platform
Go to the **Platform Management** page and click **Create**. In the pop-up window, enter the required information and click **OK**. By default, you can create up to 30 platforms. To create more, submit a ticket for assistance.
 -	Name: Enter a custom name, which can contain up to 30 characters.
 -	Region: Select **Chinese Mainland** and/or **Outside Chinese Mainland** (this configuration item cannot be modified after the creation information is submitted).
 -	Tag: You can classify and manage resources by setting tags, with up to 50 tags for each resource.
![](https://qcloudimg.tencent-cloud.cn/raw/83685e52fd213cda2a51044635152b31.png)
After submitting the creation information, you can view the relevant information of the platform.
 -	Platform ID/name: You can click the ID to view the **platform details** and configure listeners (forwarding rules) and attack defense.
 -	Status: **Enabled** or **Enabling** indicates that the platform is running normally or being enabled respectively.
	If the status is **Disabled**, you cannot modify the platform information and configuration. **Disabling** indicates that the configuration is being disabled.
	**Deploying** or **Deleting** indicates that the configuration is being deployed or being deleted respectively.
 - Chinese Mainland: Information of resource groups and CNAME records in the Chinese mainland. 
 - Outside Chinese mainland: Information of resource groups and CNAME records outside the Chinese mainland.
 -	Operation: You can change the platform status (enabling, disabling, or deleting the platform).
![](https://qcloudimg.tencent-cloud.cn/raw/1da2390af5e2c45eafa2a1f5b2545c7c.png)

### Enabling acceleration service
Go to the **Platform Management** page and click **Enable** in the **Operation** column of the target platform (in **Disabled** status). In the pop-up window, click **OK** to enable the acceleration service.
- Disabling acceleration service
Go to the **Platform Management** page and click **Disable** in the **Operation** column of the target platform (in **Running** status). In the pop-up window, click **OK** to disable the acceleration service.
- Deleting acceleration service
Go to the **Platform Management** page and click **Delete** in the **Operation** column of the target platform (in **Disabled** status). In the pop-up window, click **OK** to delete the acceleration service. If the platform status is **Running**, you need to disable the platform first before deleting it.
- Platform details
Go to the **Platform Management** page and click the ID of the target platform to enter the platform details and tags page. Here, you can view the **platform information**, click the **TCP/UDP Listener Management** tab to configure forwarding rules, and click the **Attack Defense** tab to set security access policies.

![](https://qcloudimg.tencent-cloud.cn/raw/ceacffe9ef7b27bfb9aa6fb86d3ac5f3.png)

### TCP/UDP listener management
1. Create a listener
Go to the **Platform Management** page and click the ID of the target platform to enter the platform details page. Select the **TCP/UDP Listener Management** tab, click **Create**, configure the listener information in the pop-up window, and click **OK** to create a forwarding rule.
![](https://qcloudimg.tencent-cloud.cn/raw/33b6eff9530c5133a11155d2cc3eb1b9.png)
>! Set **Protocol** and *Get client IP** based on your actual business protocol. If the secondary origin server is enabled, the protocol can be TCP only.

![](https://qcloudimg.tencent-cloud.cn/raw/6ac3b171bd051529c2c2644459d61d43.png)

 -	Listener name: Enter a custom listener name, which can contain up to 30 characters.
 -	Get client IP: You can select **TOA** or **Proxy Protocol**.
 -	Protocol: It uses the default configuration and does not need to be entered.
 -	Listening port: Access port of the acceleration line, which cannot be modified after the configuration is submitted.
Value range: 1-64999 (36000 and 56000 are unavailable). You can click **Add** to add multiple port records. Up to 20 ports can be added during each listener creation. The listening ports of each acceleration platform must be unique.
 -	Origin Type: Select **IP** or **Domain Name**.
 -	Origin-pull policy: If the origin type is **IP**, you can select **RR** or **Weighted RR**. If the origin type is **Domain Name**, you can select **RR** only.
 -	Origin-pull Address: Enter the origin server address, which can contain up to 80 characters. The value range of the origin server port is 1–65535.
	1. If the origin type is **IP**, you can click **Add** to add up to nine origin servers, and only IPv4 IPs are supported. If the origin type is **Domain Name**, you can add only one origin server.
	2. The origin server port refers to the port accessed during origin-pull.
	3. A weight ranges from 1 to 100, and the system calculates the origin-pull ratio of different origin servers based on their weights. For example, if you configure three origin server: A, B, and C, whose weights are 10, 20, and 30 respectively, then 10/(10+20+30) requests will be forwarded to origin server A, 20/(10+20+30) requests to B, and 30/(10+20+30) requests to C.
 -	Secondary origin: It is disabled by default. If you select **Enable**, you need to configure the secondary origin-pull policy and address.
 -	Origin-pull policy: Same as the primary origin server's **origin-pull policy**. 
 -	Origin-pull address: Its type can only be the same as that of the primary origin server's **origin-pull Address**.
2.	Modify a listener
Go to the **Platform Management** page and click the ID of the target platform to enter the platform details page. Select the **TCP/UDP Listener Management** tab, click **Modify** in the **Operation** column of the target listener, modify the listener information (the protocol and listening port cannot be modified) in the pop-up window, and click **OK**.
3.	Delete a listener
Go to the **Platform Management** page and click the ID of the target platform to enter the platform details page. Select the **TCP/UDP Listener Management** tab, click **Delete** in the **Operation** column of the target listener, and click **OK** in the pop-up window.

### 	Attack defense
1. Go to the **Platform Management** page and click the ID of the target platform to enter the platform details page. Select the **Attack Defense** tab and set security access policies to control the public network access permissions of the acceleration platform. After configuration, click **Save** to make the rules take effect.
![](https://qcloudimg.tencent-cloud.cn/raw/92f129027e84f4d1c16440affc73dd84.png)
2.	Control policy
If it is **enabled**, all traffic is allowed by default, which is the default rule.
If it is **disabled**, all traffic is denied by default.
3.	Access rule
Rule priority: Rules listed lower are with higher priority. You can drag and drop the rules to adjust their priorities. You can create up to 100 access rules. To create more, submit a ticket for assistance.
	1.	Add a rule
	Click **Add Rule**, enter the access rule information in the pop-up window, and click **OK**.
		-	Source IP: You can enter a single IP (such as 192.168.0.1) or a CIDR block (such as 192.168.0.1/24).
		-	Policy: If you select **Allow**, the source IP set by the rule will be allowed to access when attack defense is enabled.
		If you select **Reject**, the source IP will be denied access.
		-	Remarks: You can add custom remarks for this rule, which can contain up to 30 characters.
	![](https://qcloudimg.tencent-cloud.cn/raw/40f2b30236da813154907dbf3c3aa5f6.png)
	2.	Modify a rule
	Click **Modify** in the **Operation** column of the target rule. In the pop-up window, modify the information and click **OK**. Then, click **Save** to make the rule take effect.
	3.	Delete a rule
	Click **Delete** in the **Operation** column of the target rule. Then, click **Save** to make the configuration take effect.

## 3. Statistics
Click **Statistics** to enter the **Statistics** page, where you can view the resources and status of shared acceleration platforms and listeners.
![](https://qcloudimg.tencent-cloud.cn/raw/f618d0b13be73675f34bad2902a5f637.png)

-	Dimension: Select **Platform** or **Listener**.
	1. If you select **Platform**, the **Platform** field will be displayed, and you can select one or multiple platforms. 
	2. If you select **Listener**, the **Platform** and **Listener** fields will be displayed, and you can select one platform and one or multiple listeners.
-	Region: Select **Chinese Mainland** or **Outside Chinese mainland**.
-	Acceleration Type: **All** is selected by default, and you can select **Bandwidth**, **Traffic**, or **Current Connections**.
-	Time Period: Select **Today**, **Yesterday**, **Last 7 Days**, **Last 15 days**, **Last 30 Days** or a custom time period. 
-	Time Granularity: Select **1 minute**, **5 minutes**, **1 hour**, or **1 day**. Data can be retained for up to 186 days.

## 4. Shared Acceleration Connection
GAAP shared acceleration currently does not support access via IP connection, and the CNAME domain name cannot be accessed directly. You need to complete the CNAME configuration at your domain name service provider. After the configuration takes effect, GAAP shared acceleration can be used normally.
![](https://qcloudimg.tencent-cloud.cn/raw/8bc39905d8a944ffe0a26e699cf2bcdc.png)
1. Set a CNAME record for DNS

	-	If your DNS service provider is Tencent Cloud, configure the CNAME record as instructed in the official operation guide.
	-	If your DNS service provider is Wanwang, configure the CNAME record as instructed [here](https://help.aliyun.com/document_detail/29725.html).
	-	If you use another DNS service provider, see their particular operation guide.
2. Check whether the CNAME record takes effect
The time it takes for the CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also run `ping` on the command line to check whether the CNAME record is in effect. If a domain name suffixed with `ovscdns.com` can be pinged, the domain name's CNAME record has taken effect.

## 5. Get the real client IP
For detailed directions, see [Basic Principle](https://intl.cloud.tencent.com/document/product/608/14429).
