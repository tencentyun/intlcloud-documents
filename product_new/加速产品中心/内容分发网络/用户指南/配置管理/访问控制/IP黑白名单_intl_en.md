CDN supports IP blacklist/whitelist configuration, allowing you to create filtering policies for source IPs of user requests based on business needs and preventing hotlinking or attacks from malicious IPs.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/99e0c24b4530c30b9abe27325bb1b317.png)
2. Click the **Access Control** tab and then **IP Blacklist & Whitelist Configuration** . The IP blacklist/whitelist feature is disabled by default.
![img](https://main.qcloudimg.com/raw/0ad78b7f997c766758807eb92340efcd.png)
	- IP blacklist and whitelist are incompatible with each other and cannot coexist. You can enter up to 100 entries in the blacklist or up to 50 entries in the whitelist, separated by line breaks and one entry per row.
	- Currently, only IP ranges in the following formats are supported: /8, /16, and /24. If both IP blacklist and whitelist are empty, blacklist/whitelist feature is disabled.

### Whitelist Configuration
1. Click **Edit** and **IP Whitelist** will be selected by default. You can now configure the whitelist.
   Enter IPs in the input box and submit them to enable the IP whitelist. The requested content will be returned only if the source IP matches an IP address or IP range in the whitelist; otherwise, a 403 error will be returned.
![img](https://main.qcloudimg.com/raw/d96fc3efbf3e8d22492f2abef5009ec3.jpg)
2. After the configuration is completed, the feature is on and effective IP whitelist configuration information will be displayed below. You can click **Edit** to change the configuration information.
![img](https://main.qcloudimg.com/raw/b75819f595495f27117a5f0947bc6c26.png)
3. After the **IP Blacklist/Whitelist** feature is off, the configuration information below will become invalid, i.e., the IP blacklist/whitelist feature is disabled. It can be enabled again manually.
![img](https://main.qcloudimg.com/raw/852bd47704f7a8dff83af4aa74956161.png)

### Blacklist Configuration

1. Click **Edit** and select **IP Blacklist** to configure the blacklist.
   Enter IPs in the input box and submit them to enable the IP blacklist. If the source IP matches an IP address or IP range in the blacklist, a 403 error will be returned; otherwise, the requested content will be returned.
![img](https://main.qcloudimg.com/raw/e15849cc11a69221e281a4f8c9e15624.jpg)
2. After the configuration is completed, the feature is on and effective IP blacklist configuration information will be displayed below. You can click **Edit** to change the configuration information.
![img](https://main.qcloudimg.com/raw/cd2fa0e9923cb6c88a49ed95b1398af9.png)
3. After the **IP Blacklist/Whitelist** feature is off, the configuration information below will become invalid, i.e., the IP blacklist/whitelist feature is disabled. It can be enabled again manually.
![img](https://main.qcloudimg.com/raw/0e1cd5c478cddb2890736be60e8ab55e.png)

## Sample Case
If the IP blacklist/whitelist configuration of the domain name `www.test.com` is as follows:
![img](https://main.qcloudimg.com/raw/03d21c419dce2dae111333d5e8b64025.jpg)
Then:
- When a user with IP `1.1.1.1` accesses the resource `http://www.test.com/1.jpg`, the IP matches an IP in the whitelist, the requested content will be returned.
- When a user with IP `2.2.2.2` accesses the resource `http://www.test.com/1.jpg`, as the IP does not match any IP in the whitelist, a 403 error will be returned.
