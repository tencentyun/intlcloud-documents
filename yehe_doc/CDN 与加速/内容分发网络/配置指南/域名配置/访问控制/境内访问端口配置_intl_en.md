
## Configuration Overview

By default, CDN supports port 80, 8080, and 443. You can disable any of them as needed.

>! 
>- Port configuration is now only available in the Chinese mainland. If a domain name is configured for global acceleration, then the configuration changes will take effect only in the Chinese mainland.
>- This feature may be unavailable in some platforms. We will complete server upgrade as soon as possible.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page. Open the **Access Control** tab to find the **Chinese Mainland Access Port Configuration** section.

Port 80, 8080, and 443 are enabled by default.
![](https://main.qcloudimg.com/raw/a9f3930bb87a720acd8a09fb07f333d2.png)

### Modifying the configuration

You can disable and enable the ports as needed.

**Modification limitations**

- If HTTPS access or forced HTTPS redirection is enabled for a domain name, Port 443 cannot be disabled.
- Either Port 80 or 8080 must be opened.



## Configuration Samples

If the **Chinese Mainland Access Port Configuration** of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/a420e4f25d322855ee04b41c408ea9ab.png)

Then the actual access will be as follows:

CDN nodes deny all access requests from the port 8080.
- If a domain name is configured for global acceleration, the configuration will only take effect in the Chinese mainland, which means that the CDN nodes will deny the access requests from the port 8080.

