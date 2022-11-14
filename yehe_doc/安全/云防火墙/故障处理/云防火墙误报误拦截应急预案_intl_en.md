
This topic describes how to deal with a large number of firewall false positives and an abnormal drop in traffic due to improper strategy changes.
## Problem
A large number of legitimate requests from certain IPs are blocked due to false positives of intrusion defense, or an abnormal drop in traffic is caused by improper strategy changes.
## Solution
If these requests are blocked by Cloud Firewall, you can disable the blocking feature, allow requests from the blocked IPs, or request support from the product security team.
## Steps
### [Step 1: disable the blocking feature](id:step1)

1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ips), and then click **Intrusion Protection System** in the left navigation pane.
2. Select **Observe** for the protection mode on the intrusion defense page.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8aefe20482d102a10ce06bfffe899f3c.png" style="zoom:67%;" />
3. Disable "Enable blocklist" above the blocklist.
![](https://qcloudimg.tencent-cloud.cn/raw/01276741e02f666c36e8cd4c17817c3a.png)

### Step 2: manual troubleshooting
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/warncenter), and then click **Alert Management** in the left navigation pane to enter the Alert Management page.
2. On the Alert Management page, select **Blocked statistics** -> **Inbound**.
3. On the Inbound tab, select **Sort by blocking statistics** to find the IP address that is falsely blocked.
![](https://qcloudimg.tencent-cloud.cn/raw/adbaf7841559056429298135b27b3150.png)
4. Add the IP address to the allowlist.
	- **Method 1**: Click **Allow** on the right side of the falsely blocked IP address to add it to the allowlist (ignore list) and allow access from the IP address.
	- **Method 2**: On the [Intrusion Defense](https://console.cloud.tencent.com/cfw/ips) page, select **Ignore list** -> **Add addresses** to add the falsely blocked IP addresses in batches.
	![](https://qcloudimg.tencent-cloud.cn/raw/ab8be2bcc5dc6bfb54401c616fdfc29e.png)
5. After the above procedures, restore the configuration in [Step 1](#id:step1) and observe if the traffic volume returns to normal.

### Step 3: submit a ticket to report false positives

1. If the traffic volume is still abnormal after manual troubleshooting, enter the [Submit ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=1290&source=0&data_title=T-Sec-%E4%BA%91%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=1323&queue=3233&scene_code=36970&step=2) page and provide your AppID and the falsely blocked IP addresses to the security team.
2. After the feedback is received, the security team will respond within the specified time period and adjust the detection rules.
