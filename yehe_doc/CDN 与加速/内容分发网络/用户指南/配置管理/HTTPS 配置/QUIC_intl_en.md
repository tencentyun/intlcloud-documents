## Feature Overview

Quick UDP Internet Connections (QUIC) is a general network protocol, which guarantees network security and reduces the latency in transfer and connections to prevent network congestion.

Tencent Cloud CDN QUIC beta has been released. You can [submit an application](https://intl.cloud.tencent.com/apply/p/g0lwu71z0i7) to become a beta user. We will review your application within 15 business days.



## Beta Guide

When your application is approved, you can go to the CDN console to enable QUIC for your testing domain names.
>!QUIC is currently in beta on the CDN console, therefore, we recommend only enabling QUIC for your new testing domain names instead of any business domain names.

Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and enable QUIC when connecting a new domain name:
![](https://main.qcloudimg.com/raw/a8dd2d19c8c6c31612317d39dda70266.png)
**Configuration limitations:**

- QUIC is not available for domain names with the service type of **Streaming VOD acceleration**.
- QUIC is not available for domain names with IPv6 enabled.

After adding the domain name, you can click **Domain Management** on the left sidebar, enter the domain name details page of the domain name, and open the **HTTPS Configuration** page to find the QUIC configuration section.
It is disabled by default. You need to configure an HTTPS certificate before enabling it.
![](https://main.qcloudimg.com/raw/cdeb046241bd674d27884feaf14eeeb3.png)



>!Switching service types involves resource scheduling between platforms. We recommend not switching service types for domain names after enabling QUIC.



