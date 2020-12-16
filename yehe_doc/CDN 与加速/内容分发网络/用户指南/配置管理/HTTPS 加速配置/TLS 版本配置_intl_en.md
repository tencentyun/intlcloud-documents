## Feature Overview

Tencent Cloud CDN enables TLS 1.0/1.1/1.2 and disables TLS 1.3 by default. You can enable and disable TLS versions as needed.

>!
>- HTTPS certificate must be successfully configured before the TLS configuration.
>- Some platforms are being upgraded and the configuration is currently not supported.



## Configuration Guide

### Viewing configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **HTTPS Configuration** tab to find the **TLS Version Configuration** section.

TLS 1.0/1.1/1.2 are enabled and TLS 1.3 is disabled by default.




### Modifying configuration

You can click **Modify Configuration** to enable and disable TLS versions as needed.


**Configuration limitations**

- Only a single version or multiple consecutive ones can be enabled, i.e., skipping version 1.1 to enable 1.0 and 1.2 is not allowed.
- At least one version must be enabled.

