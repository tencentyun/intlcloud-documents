If you want to control the access to your business resources, you can use the referer-based hotlink protection feature in CDN. By setting an access control policy on the value of the referer field in the HTTP request header, the access source can be restricted to prevent hotlinking by malicious access.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. Find the domain name you want to edit and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/f5bc41a4fe8fd20dd8b2c098da3878a7.jpg)
3. Click the **Access Control** tab and configure the **Hotlink Protection** module.
 ![](https://main.qcloudimg.com/raw/10ea38c8f5ac219e8b0d7faf455871ba.jpg)
Hotlink protection is disabled by default with no blacklist or whitelist enabled. Referer blacklist and whitelist are incompatible with each other and cannot coexist. You can enter up to 400 entries separated by line breaks (one entry per row).
>- Hotlink protection supports domain name/IP rules (if an IP rule is used, prefix matching is available; if a domain name rule is used, prefix matching is not supported). For example, if `www.abc.com` is configured, then `www.abc.com/123` will be matched, but `www.abc.com.cn` will not; if 127.0.0.1 is configured, then 127.0.0.1/123 will be matched.
> - Hotlink protection supports wildcard matching, i.e., if `*.qq.com` is configured, then both `www.qq.com` and `a.qq.com` will be matched.

### Referer Whitelist
1. Click the **Edit** icon in the hotlink protection configuration section and select **Referer Whitelist** to configure the whitelist.
If you configure a referer whitelist for the domain name `www.test.com` with content as `www.abc.com` and do not check **Allow blank referer**, you are only allowing access requests where the referer value is `www.abc.com`, and a 403 error will be returned for other requests. 
2. **Configuration notes:** 
 - If the referer field of a request matches the string set in the whitelist, the CDN node will return the requested information.
 - If the referer field of a request does not match the string set in the whitelist, the CDN node will reject returning the requested information and return a 403 status code.
 - Once the whitelist is configured, the CDN node can only return the requested information for requests that match the string set in the whitelist.
 - If **Allow blank referer** is checked, the CDN node will return the requested information if the referer field is empty or does not exist in a request (such as a browser request).
![](https://main.qcloudimg.com/raw/33fc1792ebd204bc97f8b7d34ea4b4f5.jpg)

### Referer Blacklist
1. Click the **Edit** icon in the hotlink protection configuration section and select **Referer Blacklist** to configure the blacklist.
If you configure a referer blacklist for the domain name `www.abc.com` with content as `www.test.com` and do not check **Allow blank referer**, a 403 error will be returned for all requests where the referer value is `www.test.com`, and the requested content will be returned for other requests.
2. **Configuration notes:** 
 - If the referer field of a request matches the string set in the blacklist, the CDN node will reject returning the requested information and return a 403 status code.
 - If the referer field of a request does not match the string set in the blacklist, the CDN node will return the requested information.
 - If **Allow blank referer** is checked, the CDN node will reject returning the requested information and return a 403 status code if the referer field is empty or does not exist in a request (such as a browser request).
![](https://main.qcloudimg.com/raw/9e84057459903a7b24f1aa35d1880d28.jpg)

## Sample Case
If the domain name referer is configured as follows:
![](https://main.qcloudimg.com/raw/f88b6d6e3654b50e04ffd578290f1478.png)
- If a user requests a resource with URL `http://www.test.com/1.jpg?version=1.1` from a browser and the request referer is empty, then the requested content will be returned.
- If a user requests a resource with URL `http://www.test.com/1.jpg?version=1.1` and the request referer is `www.abcd.com` which is not in the whitelist, then a 403 error will be returned.
