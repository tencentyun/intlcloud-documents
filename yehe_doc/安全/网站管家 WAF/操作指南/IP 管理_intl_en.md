## Feature Overview
The IP management feature of WAF allows you to query access source IPs that pass WAF-protected domain names and add them to the blacklist/whitelist. The core features include IP query, IP blacklist/whitelist setting, and IP blocking status query.
- IP query: you can query the status of an entered IP in the protected domain name, such as whether it is in the blacklist/whitelist or is blocked.
- IP blacklist/whitelist setting: you can set domain name-specific or global IP blacklist/whitelist rules.
- IP blocking status: you can view the blocking status information of source IPs blocked due to CC attacks and CAPTCHA verification based on custom policies.

## Configuration Steps
- #### **Sample 1. Querying IP**
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview), select **IP Management** > **IP Query**, and enter the IP address to be queried to view its status.
![](https://main.qcloudimg.com/raw/21cb18626590f9463c60a73bbabdeebf.png)
2. You can manually add the queried IP address to the blacklist/whitelist.
![](https://main.qcloudimg.com/raw/20dcb9a1f8779f0541a903081d700880.png)
- #### **Sample 2. Blacklisting IP**
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **IP Management** > **IP Blacklist/Whitelist** to enter the configuration page.
>In the IP blacklist module, you can add a domain name-specific or global blacklist/whitelist which will take effect in the following priority order:
>- The priority of the blacklist/whitelist is only lower than that of the custom pass policy of WAF but higher than that of other detection logics.
>- Priority of IP blacklist/whitelist from high to low: global whitelist > domain name-specific whitelist > domain name-specific blacklist > global blacklist.

![](https://main.qcloudimg.com/raw/dad2779730036766a6ce098f635731d2.png)
**Configuration item description:**
Category: blacklist, whitelist.
Source: CC protection, custom rule.
Advanced Filter: you can use the creation time and expiration time to filter IP information.
2. To add the blacklist/whitelist, select the domain name to be protected in the top-left corner, click **Blacklist/Whitelist**, and select the IP address to be blacklisted/whitelisted.
![](https://main.qcloudimg.com/raw/61dbd125fcd2dd8803e7f7ac7a72779d.png)
>If you select `ALL` for domain name, the added IP blacklist/whitelist will be global.

3. You can import blacklist/whitelist and export their filtered results. When importing IP information, please use the export format.
![](https://main.qcloudimg.com/raw/3786459fe465cda4a68126f575f8522f.png)
4. After the source IP is added, you can enter it in the IP query module to query its status.
- #### **Sample 3. Querying IP blocking status**
Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **IP Management** > **IP Blocking Status** to enter the query page. You can query the information of IPs blocked by the custom rules and CC protection module. You can also export the query results or blacklist/whitelist a single IP.
![](https://main.qcloudimg.com/raw/ae0c778891b8fb748345458709ca6300.png)


