## Configuration Overview
To control the source of access to your business resources, you can use the referer hotlink protection feature in Tencent Cloud CDN.

By configuring an access control policy on the value of the referer field in the HTTP request header, you can control the access source to prevent hotlinking by malicious users.


## Configuration Guide
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Access Control** tab to see the **Hotlink Protection Configuration** section. It is disabled by default.
![](https://main.qcloudimg.com/raw/53cfa056e5574aae9c912db36fcbf67b.png)

### Enabling the configuration

Toggle on the switch, select a hotlink protection type, tick **Allow blank referer** as needed, enter an IP or domain name in the input box, and click **OK**.
![](https://main.qcloudimg.com/raw/951eb25d77110a01fcd91ab9bfcd1cad.png)
**Referer blocklist**:

- If the referer field of a request matches the string configured in the blocklist, CDN node will not return the requested information and a 403 status code will be returned.
- If the referer field of a request does not match the string configured in the blocklist, CDN node will return the requested information.
- If **Allow blank referer** is ticked, CDN node will not return the requested information and a 403 status code will be returned if the referer field is empty or does not exist in a request (such as a browser request).

**Referer allowlist**:
- If the referer field of a request matches the string configured in the allowlist, CDN node will return the requested information.
- If the referer field of a request does not match the string configured in the allowlist, CDN node will not return the requested information and a 403 status code will be returned.
- Once the allowlist is configured, CDN node can only return requests that match the string configured in the allowlist.
- If **Allow blank referer** is ticked, CDN node will return the requested information if the referer field is empty or does not exist in a request (such as a browser request).

**Configuration limitations**:
+ Hotlink protection supports domain name/IP rules (if an IP rule is used, prefix matching is available; if a domain name rule is used, prefix matching is not supported). For example, if `www.abc.com` is configured, then `www.abc.com/123` will be matched, but `www.abc.com.cn` will not; if `127.0.0.1` is configured, then `127.0.0.1/123` will be matched.
+ Hotlink protection supports wildcard matching, e.g., if `*.qq.com` is configured, then both `www.qq.com` and `a.qq.com` will be matched.

### Disabling the configuration
You can toggle off the switch to disable this feature. When the switch is off, this feature does not take effect in the production environment even if there is an existing configuration. If you toggle the switch on, the configuration will take effect across the entire network after the action is confirmed.
![](https://main.qcloudimg.com/raw/0eff7fac96363892b1b95f53fbadf47d.png)

### Region-specific configuration
If your acceleration domain name is configured for global acceleration and you want to configure acceleration in and outside the Chinese mainland with different referer hotlink protection settings, you can click **Add Special Configuration**.
![](https://main.qcloudimg.com/raw/31d414d5adf37f8a2deadce688962645.png)

> !Currently, region-specific configuration items cannot be deleted once added but can be disabled.

## Configuration Sample

If the hotlink protection configuration of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/027832bf7f5df50370257cce662105d8.png)
Then the actual access will be as follows:

1. If a user in the Chinese mainland initiates a request with the referer field being `1.1.1.1`, which matches the allowlist configured for the Chinese mainland, then the requested content will be directly returned.
2. If a user outside the Chinese mainland initiates a request with a blank referer, which matches the blocklist configured for regions outside the Chinese mainland, then a 403 status code will be returned.

