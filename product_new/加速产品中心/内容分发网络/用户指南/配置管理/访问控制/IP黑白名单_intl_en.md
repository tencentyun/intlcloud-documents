CDN supports IP blacklist/whitelist configuration, allowing you to create filtering policies for source IPs of user requests based on business needs and preventing hotlinking or attacks from malicious IPs.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/9c13a263df1ccc5cc15f2d19a5476e37.png)
2. Click the **Access Control** tab and then **IP Blacklist & Whitelist Configuration** . The IP blacklist/whitelist feature is disabled by default.
![img](https://main.qcloudimg.com/raw/daf36d387ba9b2e74ebf83214321f870.png)
	- IP blacklist and whitelist are incompatible with each other and cannot coexist. You can enter up to 100 entries in the blacklist or up to 50 entries in the whitelist, separated by line breaks and one entry per row.
	- Currently, only IP ranges in the following formats are supported: /8, /16, and /24. If both IP blacklist and whitelist are empty, blacklist/whitelist feature is disabled.

### Whitelist Configuration
1. Click **Edit** and **IP Whitelist** will be selected by default. You can now configure the whitelist.
   Enter IPs in the input box and submit them to enable the IP whitelist. The requested content will be returned only if the source IP matches an IP address or IP range in the whitelist; otherwise, a 403 error will be returned.
![img](https://main.qcloudimg.com/raw/be099978810fec15c883c8745d8a331b.png)
2. After the configuration is completed, the feature is on and effective IP whitelist configuration information will be displayed below. You can click **Edit** to change the configuration information.
![img](https://main.qcloudimg.com/raw/12e3102f0ab79650a41ada6e3a008648.png)
3. After the **IP Blacklist/Whitelist** feature is off, the configuration information below will become invalid, i.e., the IP blacklist/whitelist feature is disabled. It can be enabled again manually.
![img](https://main.qcloudimg.com/raw/9ee22e5632a51a8e5ad5a7030aec80b5.png)

### Blacklist Configuration

1. Click **Edit** and select **IP Blacklist** to configure the blacklist.
   Enter IPs in the input box and submit them to enable the IP blacklist. If the source IP matches an IP address or IP range in the blacklist, a 403 error will be returned; otherwise, the requested content will be returned.
![img](https://main.qcloudimg.com/raw/361066912bd61b86fcda7ba31596fda6.png)
2. After the configuration is completed, the feature is on and effective IP blacklist configuration information will be displayed below. You can click **Edit** to change the configuration information.
![img](https://main.qcloudimg.com/raw/b6a6763732006e229730865b4403c3f2.png)
3. After the **IP Blacklist/Whitelist** feature is off, the configuration information below will become invalid, i.e., the IP blacklist/whitelist feature is disabled. It can be enabled again manually.
![img](https://main.qcloudimg.com/raw/cb843154d275ee9c899bb125f33f5d0d.png)

## Sample Case
If the IP blacklist/whitelist configuration of the domain name `www.test.com` is as follows:
![img](https://main.qcloudimg.com/raw/4116aa2143c33c9bbbb7eba1a0897a7e.png)
Then:
- When a user with IP `1.1.1.1` accesses the resource `http://www.test.com/1.jpg`, the IP matches an IP in the whitelist, the requested content will be returned.
- When a user with IP `2.2.2.2` accesses the resource `http://www.test.com/1.jpg`, as the IP does not match any IP in the whitelist, a 403 error will be returned.
