## Configuration Scenario
To control the source of access to your business resources, you can use the referer hotlink protection feature in Tencent Cloud CDN.

By configuring an access control policy on the value of the referer field in the HTTP request header, you can control the access source to prevent hotlinking by malicious users.

## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Access Control** tab, find the hotlink protection configuration, which is disabled by default:
![](https://main.qcloudimg.com/raw/edc5be9d4956054d85b315d9d4b2c487.png)

### Modifying configuration
#### 1. Modify the configuration
Switch to select the hotlink protection type, enter the corresponding information, select whether to allow blank referer, and click **OK** to enable hotlink protection.
![](https://main.qcloudimg.com/raw/4054e066457c91c7e581ed71dbb6412d.png)
**Referer blocklist:**

- If the referer field of a request matches the string configured in the blocklist, CDN node will not return the requested information and a 403 status code will be returned.
- If the referer field of a request does not match the string configured in the blocklist, CDN node will return the requested information.
- If **Allow blank referer** is selected, CDN node will not return the requested information and a 403 status code will be returned if the referer field is empty or does not exist in a request (such as a browser request).

**Referer allowlist:**
- If the referer field of a request matches the string configured in the allowlist, CDN node will return the requested information.
- If the referer field of a request does not match the string configured in the allowlist, CDN node will not return the requested information and a 403 status code will be returned.
- Once the allowlist is configured, CDN node can only return requests that match the string configured in the allowlist.
- If **Allow empty referer** is selected, CDN node will return the requested information if the referer field is empty or does not exist in a request (such as a browser request).

**Configuration rules:**
+ Hotlink protection supports domain name/IP rules (if an IP rule is used, prefix matching is available; if a domain name rule is used, prefix matching is not supported). For example, if `www.abc.com` is configured, then `www.abc.com/123` will be matched, but `www.abc.com.cn` will not; if `127.0.0.1` is configured, then `127.0.0.1/123` will be matched.
+ Hotlink protection supports wildcard matching, i.e., if `*.qq.com` is configured, then both `www.qq.com` and `a.qq.com` will be matched.

#### 2. Disable the configuration
You can switch to disable the hotlink protection feature. When the switch is off, this feature will not take effect in the production environment even if there is an existing configuration. If the switch is on, a message will be displayed to confirm whether to enable this feature before the configuration takes effect across the entire network.
![](https://main.qcloudimg.com/raw/80d3e5a457aabcc43427cbe4a5b3718b.png)

#### 3. Add region-specific configuration
If your acceleration domain name is configured for global acceleration and you want different referer hotlink protection configurations for acceleration in and outside of Mainland China, click **Add Special Configuration**.
![](https://main.qcloudimg.com/raw/11e2f8dcbba10df142183068d715d09f.png)

>After a region-specific configuration item is added, it cannot be directly deleted for the time being. You can only disable it.

## Configuration Sample

Suppose the hotlink protection configuration of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/f650be89fce5b7abb05e81ff66bf1343.png)
The actual access status will be as follows:

1. If a user in Mainland China whose referer is `1.1.1.1` initiates a request, the allowlist configured for Mainland China will be hit and the requested content will be directly returned.
2. If a user outside Mainland China whose referer is empty initiates a request, the blocklist configured for regions outside Mainland China will be hit and a 403 code will be returned.
