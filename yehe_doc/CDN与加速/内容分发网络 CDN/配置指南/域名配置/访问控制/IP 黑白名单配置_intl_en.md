
## Overview
To control the source of access to your business resources, you can use the IP blocklist/allowlist feature in Tencent Cloud CDN.

By configuring an access control policy on IPs of user requests, you can effectively control the source of access, preventing hotlinking by malicious IPs, attacks, etc.

## Directions

### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Access Control** tab to find the **IP Blocklist/Allowlist Configuration** section. The **On/Off** switch is toggled off by default.

### Enabling the configuration

To enable the IP blocklist/allowlist configuration, toggle on the **On/Off** switch. If you enable the IP blocklist/allowlist configuration for the first time and no rule is available, the Add Rule page pops up. The IP blocklist/allowlist configuration takes effect based on the priorities of the rules that you add. The rule at the bottom of the rule list has the highest priority.
>! If your acceleration domain name is configured for global acceleration, the IP blocklist/allowlist configuration takes effect globally. This configuration does not distinguish between requests from regions in and outside the Chinese mainland.

#### Adding or modifying a rule
In the **IP Blocklist/Allowlist Configuration** section, click **Add Rule** to add an IP blocklist/allowlist rule.
**IP blocklist**
If a client IP matches an IP or IP range in the blocklist, the accessed CDN node will directly return a 514 status code.
**IP allowlist**
If a client IP does not match any IP or IP range in the allowlist, the accessed CDN node will directly return a 514 status code.
**Configuration limitations**

- When you add a rule, select **Allowlist** or **Blocklist** as **Rule type**. The IP blocklist and allowlist are mutually exclusive and cannot be configured at the same time.
- Up to 500 entries can be added to the blocklist and allowlist respectively.
- Do not add entries in the IP:Port format to the IP blocklist or allowlist.
- Do not add reserved IPv4/IPv6 addresses or address ranges to the IP blocklist or allowlist.
- The rule at the bottom of the rule list has the highest priority.
To modify a rule, click **Modify** on the right of the rule in the **Operation** column.

#### Adjusting the priority of a rule
To adjust the priority of a rule, click **Adjust priority** above the rule list. Then, click the upward or downward arrow on the right of the rule in the **Operation** column to adjust its priority, as shown in the following figure. If you click the upward arrow, the rule moves up one row. If you click the downward arrow, the rule moves down one row. After you adjust the priority of the rule, click **Save**.
>!The lower a rule is in the rule list, the higher its priority.
>

#### Deleting rules
To delete a rule, click **Delete** on the right of the rule in the **Operation** column. In the pop-up window, click **OK** to confirm the deletion. The rule is permanently deleted.

### Disabling the configuration
To disable the IP blocklist/allowlist configuration, toggle off the **On/Off** switch. After the IP blocklist/allowlist configuration is disabled, you can still modify IP blocklist/allowlist rules. However, the modified rules are not immediately published to the production environment. The rules take effect only when you enable the IP blocklist/allowlist configuration.

## Configuration Samples
If the IP blocklist/allowlist configuration of the domain name `www.test.com` is as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/z5ge560_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230310104738.png)
Then the actual access will be as follows:

1. If a user whose IP is 1.1.1.1 requests to access `https://www.test.com/test/vod.mp4`, the blocklist rule at the bottom of the rule list is matched. In this case, the access request is denied, and a 514 status code is returned.
2. If a user whose IP is 1.1.1.2 requests to access `https://www.test.com/test/vod.mp4`, the blocklist rule is not matched because the IP is not specified in the blocklist rule. The allowlist rule that is configured for the access resource allows access requests only from IP 1.1.1.1. In this case, the access request is denied due to an IP mismatch, and a 514 status code is returned.
3. If a user whose IP is 1.1.1.1 requests to access `https://www.test.com/vod.mp4`, the allowlist rule instead of the blocklist rule is matched. In this case, the access request is allowed, and the user can access the resource as expected.
