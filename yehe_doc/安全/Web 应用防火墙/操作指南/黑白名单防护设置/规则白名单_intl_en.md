## Scenarios
If normal access traffic is blocked by the WAF rule engine, you can create rules to allow the access traffic using the blocklist/allowlist feature.

## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-iplist) and select **Configuration Center** > **IP Blocklist/Allowlist** on the left sidebar to enter the IP blocklist/allowlist page.
2. On the blocklist/allowlist page, select the target domain name in the top-left corner and click **Rule allowlist**.
3. On the page that appears, click **Add rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/d8914811a4f566005fc0877340b3d04c.png)
4. In the pop-up window, configure the required parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/1966d4f6f09301328f303802d8f61885.png)

**Field description:**
 - Rule ID: ID of the rule to be allowed. You can add up to 10 rule IDs for each policy.
 - Match method: Match method of the URL to be allowed. You can select "Exact match" (default value), "Prefix match", or "Suffix match".
 - URL: URI path to be allowed. The URI must be unique under one domain name.
 - Enable allowlist: It specifies whether to enable allowlist. The switch is enabled by default.
