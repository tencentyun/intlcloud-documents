CDN supports configuring IP blacklist/whitelist that enables you to create filtering policies for source IPs of user requests based on your business needs, helping prevent hotlinking and attacks from malicious IPs.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. Find the domain name you want to edit and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/f8219fdac6748d8a3130998f5a1f0104.jpg)
3. Click the **Access Control** tab and configure the **IP Blacklist & Whitelist** module.
 - IP blacklist/whitelist feature is disabled by default. IP blacklist and whitelist are incompatible with each other and cannot coexist. You can enter up to 100 entries in the blacklist or up to 50 entries in the whitelist separated by line breaks (one entry per row).
 - Currently, only IP ranges in the following formats are supported: /8, /16, /24, and /32. When both the IP blacklist and whitelist are empty, the blacklist/whitelist feature is disabled.
![](https://main.qcloudimg.com/raw/cb95783e5920e3d217fcb3afe1925169.jpg)

### Whitelist Configuration
1. In the **IP Blacklist & Whitelist** module, click **Edit** and select **IP Whitelist** to configure the whitelist.
 ![](https://main.qcloudimg.com/raw/410f67d73f07fd759f73b1a5d8339b0a.jpg)
2. Enter the IPs in the input box and submit to enable the IP whitelist. The requested content will be returned only if the source IP matches an IP address or IP range in the whitelist; otherwise, a 403 error will be returned. 

### Blacklist Configuration
1. In the **IP Blacklist & Whitelist** module, click **Edit** and select **IP Blacklist** to configure the blacklist.
 ![](https://main.qcloudimg.com/raw/7775b9983383e2e42755ff36ca464e55.jpg)
2. Enter the IPs in the input box and submit to enable the IP blacklist. If the source IP matches an IP address or IP range in the blacklist, a 403 error will be returned; otherwise, the requested content will be returned. 

## Sample Case
If the IP blacklist/whitelist configuration of the domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/410f67d73f07fd759f73b1a5d8339b0a.jpg)
Then:
- When a user with IP `1.1.1.1` requests the resource `http://www.test.com/1.jpg`, as the IP matches an IP in the whitelist, the requested content will be returned.
- When a user with IP `2.2.2.2` requests the resource `http://www.test.com/1.jpg`, as the IP does not match any IP in the whitelist, a 403 error will be returned.
