## Configuration Scenario
To control the source of access to your business resources, you can use the IP blocklist/allowlist feature in Tencent Cloud CDN.

By configuring an access control policy on IPs of user requests, you can effectively control the source of access, preventing hotlinking by malicious IPs, attacks, etc.

## Configuration Guide

### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Access Control** tab, find the IP blocklist/allowlist configuration, which is disabled by default:
![](https://main.qcloudimg.com/raw/f151317bd14f053a125bf0c3841da033.png)

### Modifying configuration
#### 1. Modify the configuration
Switch to select "IP Blocklist" or "IP Allowlist", enter the list of IPs or IP ranges, and click **OK** to enable IP blocklist/allowlist configuration:
![](https://main.qcloudimg.com/raw/0b278589542a7022b3525f80ecadd2e3.png)
**IP blocklist**
If a client IP matches an IP or IP range in the blocklist, the accessed CDN node will directly return a 403 status code.
**IP allowlist**
If a client IP does not match any IP or IP range in the allowlist, the accessed CDN node will directly return a 403 status code.
**Blocklist/Allowlist rules**

+ The IP blocklist and allowlist are mutually exclusive and cannot be configured at the same time.
+ Only IP ranges `/8`, `\/16`, and `\/24` are supported.
+ The blocklist/allowlist does not support entries in `IP:port` format and can contain up to 50 entries.

#### 2. Disable the configuration
You can switch to disable the IP blocklist/allowlist feature. When the switch is off, this feature will not take effect in the production environment even if there is an existing configuration. When the switch is on, a message will be displayed to confirm whether to enable this feature before the configuration takes effect across the entire network.
![](https://main.qcloudimg.com/raw/24a3de16131fd945c05307493eb768f0.png)

>If your acceleration domain name is configured for global acceleration, the IP blocklist/allowlist will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.

## Configuration Sample

Suppose the IP blocklist/allowlist configuration of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/29a9307902d03f686345eef2964c5ec2.png)
The actual access status will be as follows:
1. A user with client IP `1.1.1.1` accesses the resource `http://www.test.com/test.txt`. As the IP matches an IP in the allowlist, the requested content will be returned.
2. A user with client IP `2.1.1.1` accesses the resource `http://www.test.com/test.txt`. As the IP does not match any IP in the allowlist, a 403 status code will be returned.

