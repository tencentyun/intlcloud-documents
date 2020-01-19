To help you control access to your business resources, CDN offers referer-based hotlink protection. By configuring an access control policy for the referer value in the HTTP request header, you can restrict access sources to prevent hotlinking by malicious users.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/2ce3d1f1c8de224de57af4098beb41d8.png)
2. Click the **Access Control** tab and configure the **Hotlink Protection** module.
 ![](https://main.qcloudimg.com/raw/9fd20fc22df01301995b50825c9275d8.png)
Hotlink protection is disabled by default with no blacklist or whitelist. Referer-based blacklist and whitelist are incompatible with each other and cannot coexist. You can enter up to 400 entries, separated by line breaks and one entry per row.
>
> - Hotlink protection supports domain name/IP rules (if an IP rule is used, prefix matching is available; if a domain name rule is used, prefix matching is not supported). For example, if `www.abc.com` is configured, then `www.abc.com/123` will be matched, but `www.abc.com.cn` will not; if 127.0.0.1 is configured, then 127.0.0.1/123 will be matched.
> - Hotlink protection supports wildcard matching, i.e., if `*.qq.com` is configured, then both `www.qq.com` and `a.qq.com` will be matched.

### Referer Whitelist
1. Click the **Edit** icon in the hotlink protection configuration section and select **Referer Whitelist** to configure the whitelist.
If you configure a referer whitelist for the domain name `www.test.com` with content as `www.abc.com` and do not check **Allow blank referer**, you only allow requests where the referer value is `www.abc.com` to access, and a 403 error will be returned for other requests. 
2. **Configuration Notes:** 
 - If the referer field of a request matches the string configured in the whitelist, the CDN node will return the requested information.
 - If the referer field of a request does not match the string configured in the whitelist, the CDN node will not return the requested information and a 403 status code will be returned.
 - Once the whitelist is configured, the CDN node can only return requests that match the string configured in the whitelist.
 - If **Allow blank referer** is checked, the CDN node will return the requested information if the referer field is empty or does not exist in a request (such as a browser request).
![](https://main.qcloudimg.com/raw/8bb57f6f192f204d08e209f00d2c52a7.png)

### Referer Blacklist
1. Click the **Edit** icon in the hotlink protection configuration section and select **Referer Blacklist** to configure the blacklist.
If you configure a referer blacklist for the domain name `www.abc.com` with content as `www.test.com` and do not check **Allow blank referer**, a 403 error will be returned for all requests where the referer value is `www.test.com`, and all other requests will return the requested information.
2. **Configuration Notes:** 
 - If the referer field of a request matches the string configured in the blacklist, the CDN node will not return the requested information and a 403 status code will be returned.
 - If the referer field of a request does not match the string configured in the blacklist, the CDN node will return the requested information.
 - If **Allow blank referer** is checked, the CDN node will not return the requested information and a 403 status code will be returned if the referer field is empty or does not exist in a request (such as a browser request).
![](https://main.qcloudimg.com/raw/82a111ebd792082b5614917ef9116177.png)

## Sample Case
If the domain name referer is configured as follows:
![](https://main.qcloudimg.com/raw/429f14c59e95b118cf0ef484c443819b.png)
- If a user requests a resource with URL `http://www.test.com/1.jpg?version=1.1` from a browser and the request referer field is empty, then the requested information will be returned.
- If a user requests a resource with URL `http://www.test.com/1.jpg?version=1.1` and the request referer `www.abcd.com` is not in the whitelist, then a 403 error will be returned.
