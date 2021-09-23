## Overview

Quick UDP Internet Connections (QUIC) is a common network protocol, which guarantees network security and reduces the latency in transfer and connections to prevent network congestion. You can enable QUIC protocol for clients to access CDN nodes with enhanced data transfer security and access efficiency.

For now, the supported QUIC versions include draft h3-28, h3-Q050, h3-Q046, h3-Q043, Q046, and Q043.


## Beta User Application
QUIC feature is in beta test now. Please contact your sales rep if you’d like to join the beta tesing. 


## Beta User Guide

Beta users can go to the CDN console to enable QUIC for your new domain names for testing.
>!
>- In the beta test, QUIC is only available for newly added domain names but not the existing ones.
>- To avoid affecting the normal running of your business, please enable QUIC only for staging domain names instead of production domain names.
>- Switching service types concerns resource scheduling between platforms. We recommend not switching service types for domain names after enabling QUIC.
>- QUIC is not available for origin pull.


Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and tick the box to enable QUIC when connecting a new domain name:
![](https://main.qcloudimg.com/raw/2098308cd8a8c1a0321c0164646b7700.png)
**Use Limits:**

- QUIC is now not available for on-demand video streaming acceleration.
- QUIC cannot be enabled for any domain names with IPv6 enabled.


After adding a domain name, you can click **Domain Management** on the left sidebar, in the domain name details page, select **HTTPS Configuration** -> **QUIC configuration**. QUIC is disabled by default, and you can enable it manually.
**Note:** An HTTPS certificate is required to enable QUIC.
![](https://main.qcloudimg.com/raw/e697e32b39948d56610285c80043f1de.png)



## Billing

QUIC is a value-added service. It’s now in free beta test. We will inform you in advance before it starts incurring charges. 

