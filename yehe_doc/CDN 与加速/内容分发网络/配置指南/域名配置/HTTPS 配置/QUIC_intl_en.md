## Feature Overview

Quick UDP Internet Connections (QUIC) is a common network protocol, which guarantees network security and reduces the latency in transfer and connections to prevent network congestion. You can enable QUIC protocol for clients to access CDN nodes with enhanced data transfer security and access efficiency.

Currently, these QUIC versions are supported by default: draft h3-28, h3-Q050, h3-Q046, h3-Q043, Q046, and Q043.

Tencent Cloud CDN QUIC beta has been released. You can [submit an application](https://intl.cloud.tencent.com/apply/p/g0lwu71z0i7), and after which we will review your application within 15 business days.



## Beta Guide

If your application is approved, you can go to the CDN console to enable QUIC for your new domain names for testing.
>!
>- After your application is approved, QUIC can only be enabled for new but not the existing domain names.
>- QUIC is currently in beta on the CDN console, therefore, we recommend only enabling QUIC for your testing domain names instead of any business domain names.
>- Switching service types concerns resource scheduling between platforms. We recommend not switching service types for domain names after enabling QUIC.
>- QUIC origin-pull is currently not supported.


Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and tick the box to enable QUIC when connecting a new domain name:
![](https://main.qcloudimg.com/raw/2098308cd8a8c1a0321c0164646b7700.png)
**Configuration limitations:**

- QUIC currently cannot be enabled for any domain names of the service type of streaming VOD acceleration.
- QUIC cannot be enabled for any domain names with IPv6 enabled.


After successfully connecting the domain name, you can click **Domain Management** on the left sidebar, enter the domain name details page, and open the **HTTPS Configuration** tab to find the QUIC configuration section. It is disabled by default, and you can enable it directly.
**Note:** Please first configure an HTTPS certificate to enable it.
![](https://main.qcloudimg.com/raw/e697e32b39948d56610285c80043f1de.png)



## Billing

QUIC is currently in beta on the CDN console. It is a value-added service and currently free of charge.

