CDN supports configuring IP blacklist/whitelist that enables you to create filtering policies for source IPs of user requests based on your business needs, helping prevent hotlinking and attacks from malicious IPs.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the row of the domain to be edited and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/18a3dd6931e3fe4ea109f971e5afe410.png)
3. Click the **Access Control** tab and configure the **IP Blacklist & Whitelist** module.
 - IP blacklist/whitelist are disabled by default. IP blacklist and whitelist are incompatible with each other and cannot coexist. You can enter up to 100 entries in the blacklist or up to 50 entries in the whitelist separated by line breaks (one entry per row).
 - Currently, only IP ranges in the following formats are supported: /8, /16, /24, and /32. When both the IP blacklist and whitelist are empty, the blacklist/whitelist feature is disabled.
![](https://main.qcloudimg.com/raw/dc424728310985a97ae8e582aa43f67b.png)

### Whitelist Configuration
1. In the **IP Blacklist & Whitelist** module, click **Edit** and select **IP Whitelist** to configure the whitelist.
 ![](https://main.qcloudimg.com/raw/1375163314eb66c9e1bb1e0c9e15901b.png)
2. Enter the IPs in the input box and submit to enable the IP whitelist. The requested content will be returned only if the source IP matches an IP address or IP range in the whitelist; otherwise, a 403 error will be returned. 

### Blacklist Configuration
1. In the **IP Blacklist & Whitelist** module, click **Edit** and select **IP Blacklist** to configure the blacklist.
 ![](https://main.qcloudimg.com/raw/9832bc5859983c28f53f4d8726e293c2.png)
2. Enter the IPs in the input box and submit to enable the IP blacklist. If the source IP matches an IP address or IP range in the blacklist, a 403 error will be returned; otherwise, the requested content will be returned normally. 

## Configuration Case
If the IP blacklist/whitelist configuration of the domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/344800306be3282caf6f79a0bfbd5d52.png)
Then:
- When a user with IP `1.1.1.1` requests the resource `http://www.test.com/1.jpg`, as the IP is matched in the whitelist, the requested content will be returned.
- When a user with IP `2.2.2.2` requests the resource `http://www.test.com/1.jpg`, as the IP is not matched in the whitelist, a 403 error will be returned.
