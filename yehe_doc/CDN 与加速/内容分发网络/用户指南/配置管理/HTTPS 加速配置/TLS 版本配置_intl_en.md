## Feature Overview

Tencent Cloud CDN enables TLS 1.0/1.1/1.2 and disables TLS 1.3 by default. You can enable and disable TLS versions as needed.

>!
>- Make sure the HTTPS certificate is properly configured.
>- TLS version configuration is now only available in the Chinese mainland regions. If the acceleration region of a domain name is "Global", then the configuration changes will take effect only in the Chinese mainland.
>- This feature may be unavailable in some platforms. We will complete server upgrade as soon as possible.



## Configuration Guide

### Viewing configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **HTTPS Configuration** tab to find the **TLS Version Configuration** section.

By default, TLS 1.0/1.1/1.2 are enabled and TLS 1.3 is disabled.

![](https://main.qcloudimg.com/raw/7445026074dc473c366db6e65b807a17.png)


### Modifying configuration

Open **Modify Configuration** to enable and disable TLS versions as needed.
![](https://main.qcloudimg.com/raw/0cd09ce66a94d6886d68c60f22844310.png)


**Configuration limitations**

- You can enable a single version or multiple consecutive ones. For example, you can enable version 1.0, 1.1 and 1.2, but not version 1.0 and 1.2.
- At least one version must be enabled.
