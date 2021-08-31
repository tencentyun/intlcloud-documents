## Configuration Scenario

To control the source of access to your business resources, you can use the IP blocklist/allowlist feature in Tencent Cloud ECDN.

By configuring an access control policy on IPs of user requests, you can effectively control the source of access to prevent hotlinking by malicious IPs, attacks, etc.

## Configuration Guide

### Viewing configuration

Log in to the [ECDN Console](https://console.cloud.tencent.com/ecdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. You will find the IP blocklist/allowlist configuration in **Access Configuration**.
![](https://main.qcloudimg.com/raw/a90696de3c9633b19350c42ce7969a22.png)

### Modifying configuration

#### 1. Modify the configuration

Click **Edit** to select "IP Blocklist" or "IP Allowlist", enter the list of IPs or IP ranges, and click **OK** to enable IP blocklist/allowlist configuration:
![](https://main.qcloudimg.com/raw/fb9c0a6d836c850c0483d2a7f1b7a84d.png)
**IP blocklist**
If a client IP matches an IP or IP range in the blocklist, the accessed ECDN node will directly return a 403 status code.
**IP allowlist**
If a client IP does not match any IP or IP range in the allowlist, the accessed ECDN node will directly return a 403 status code.
**Blocklist/Allowlist rules**

- The IP blocklist and allowlist are mutually exclusive and cannot be configured at the same time.
- Only IP ranges `/8`, `/16`, `\24`, and `/32` are supported.
- The blocklist/allowlist does not support entries in `IP:port` format and can contain up to 50 entries.

## Configuration Sample

Suppose the IP blocklist/allowlist of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/92cbda13c61935970d8a57d73ee1884c.png)
The actual access status will be as follows:

1. When a user with client IP `1.1.1.1` accesses the resource `http://www.test.com/test.txt`, as the IP matches an IP in the allowlist, the requested content will be returned.
2. When a user with client IP `2.1.1.1` accesses the resource `http://www.test.com/test.txt`, as the IP does not match any IP in the allowlist, a 403 status code will be returned.

