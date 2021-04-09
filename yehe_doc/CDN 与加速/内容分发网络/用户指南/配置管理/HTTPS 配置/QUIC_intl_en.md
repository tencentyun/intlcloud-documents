## Feature Overview

Quick UDP Internet Connections (QUIC) is a common network protocol, which guarantees network security and reduces the latency in transfer and connections to prevent network congestion. You can enable QUIC protocol for clients to access CDN nodes with enhanced data transfer security and access efficiency.

Tencent Cloud CDN QUIC beta has been released. You can [submit an application](https://intl.cloud.tencent.com/apply/p/g0lwu71z0i7). We will review your application within 15 business days.



## Beta Guide

When your application is approved, you can go to the CDN console to enable QUIC for your new domain names for testing.
>!
>- QUIC is only available for newly added domain names but not the existing ones.
>- During the beta, we recommend only enabling QUIC for your testing domain names instead of production domain names.
>- Switching service types involves resource scheduling between platforms. We recommend not switching service types for domain names after enabling QUIC.
>- QUIC origin-pull is currently not supported.

Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and tick the box to enable QUIC when connecting a new domain name:
![](https://main.qcloudimg.com/raw/cb7d9ab0a9026574363f7308047c04c6.png)
**Configuration limitations**:

- QUIC currently cannot be enabled for any domain names of the service type of streaming VOD acceleration.
- QUIC cannot be enabled for any domain names with IPv6 enabled.


After successfully connecting the domain name, you can click **Domain Management** on the left sidebar, enter the domain name details page, and open the **HTTPS Configuration** tab to find the QUIC configuration section. It is disabled by default, and you can enable it directly.
**Note:** You need to configure an HTTPS certificate before enabling QUIC.
![](https://main.qcloudimg.com/raw/b90da5a37968a594ed9c81768fb72ab5.png)







