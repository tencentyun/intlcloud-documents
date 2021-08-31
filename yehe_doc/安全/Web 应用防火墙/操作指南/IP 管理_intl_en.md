## Overview
The IP management feature of Tencent Cloud WAF allows you to query access source IPs that pass WAF-protected domain names and add them to the blocklist or allowlist. Key features include IP query, IP blocklist/allowlist setting, and IP blocking status query.
- IP query: you can query the status of an IP for the protected domain name, such as whether it is in the blocklist/allowlist or whether it is blocked.
- IP blocklist/allowlist setting: you can set domain name-specific, IP range-specific, or global IP blocklist/allowlist rules.
- IP blocking status query: you can view the blocking status information of source IPs blocked due to CC attacks, bot behaviors, and failed CAPTCHA verification based on custom policies.

## Directions
- #### **Example 1. Querying IP**
	1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview), select **IP Management** -> **IP Query** on the left sidebar, and enter an IP address to view its status.
![](https://main.qcloudimg.com/raw/21cb18626590f9463c60a73bbabdeebf.png)
	2. You can manually add the queried IP address to the blocklist/allowlist.
![](https://main.qcloudimg.com/raw/20dcb9a1f8779f0541a903081d700880.png)
- #### **Example 2. Adding IP to Blocklist**
	1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **IP Management** -> **IP Blocklist/Allowlist** on the left sidebar to enter the configuration page.
>?In the blocklist/allowlist module, you can add a domain name-specific or global blocklist/allowlist which will take effect in the following priority order:
>- The priority of the blocklist/allowlist is only lower than that of the custom pass policy of WAF, but higher than that of other detection logic.
>- Priorities of IP blocklist/allowlist settings in descending order: custom pass policy > global allowlist > domain name-specific allowlist > domain name-specific blocklist > global blocklist > other WAF module logic.
>
![](https://main.qcloudimg.com/raw/dad2779730036766a6ce098f635731d2.png)
#### **Configuration item description:**
		- Category: blocklist or allowlist.
		- Source: CC protection, BOT, or custom rule.
		- Advanced Filter: you can use the creation time and expiration time to filter IPs.
	
2. To add an IP to the blocklist/allowlist, select the target domain name at the top-left corner, click **Add Blocklist/Allowlist**, and select the IP address or range to be blocked/allowed.
>!
>- If you select **ALL** for the domain name, the added IP address or range will be blocked/allowed globally.
>- The quotas for domain name in each edition are as follows:
>Premium Edition: 1000 entries/domain name; Enterprise Edition: 5,000 entries/domain name; Ultimate Edition: 20,000 entries/domain name. Each IP address or range occupies one entry in the quota.

	![](https://main.qcloudimg.com/raw/61dbd125fcd2dd8803e7f7ac7a72779d.png)
3. You can import a blocklist or allowlist and export their filtered results. When you import IP information, please refer to the file format.
	![](https://main.qcloudimg.com/raw/3786459fe465cda4a68126f575f8522f.png)
	4. After the source IP is added, you can enter it in the IP query module to query its status.
- #### **Example 3. Querying IP blocking status**
	1. Log in to the [WAF console ](https://console.cloud.tencent.com/guanjia/waf/overview) and select **IP Management** -> **IP Blocking On/Off** to enter the query page.
	2. On the query page, you can query the information of IPs blocked by the custom policy, CAPTCHA, bot blocking, and CC protection modules. You can also export the query results and add IPs to the blocklist or allowlist.
![](https://main.qcloudimg.com/raw/ae0c778891b8fb748345458709ca6300.png)

