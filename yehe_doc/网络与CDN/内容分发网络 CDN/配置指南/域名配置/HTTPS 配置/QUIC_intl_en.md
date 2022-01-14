Announcement:

Tencent Cloud CDN will officially launch QUIC support on January 5, 2022.
QUIC support is billed based on the number of QUIC requests. For more details, see [Billing Overview](https://intl.cloud.tencent.com/zh/document/product/228/2949).
We will notify you in advance of your subscription being billed. Please pay attention to our announcements in the console and documentation.

## Feature Overview

Quick UDP Internet Connections (QUIC) is a common network protocol, which guarantees network security and reduces the latency in transfer and connections to prevent network congestion. You can enable QUIC protocol for clients to access CDN nodes with enhanced data transfer security and access efficiency.

For now, the supported QUIC versions include draft h3-28, h3-Q050, h3-Q046, h3-Q043, Q046, and Q043.

## Directions

1. Enable QUIC:

After adding a domain name, you can click **Domain Management** on the left sidebar, in the domain name details page, select **HTTPS Configuration** -> **QUIC configuration**. QUIC is disabled by default, and you can enable it manually.
**Note:** An HTTPS certificate is required to enable QUIC.
![img](https://tva1.sinaimg.cn/large/008i3skNgy1gy2n1viwjjj30pf034t8t.jpg)

> Note:
>
>- Switching service types concerns resource scheduling between platforms. We recommend not switching service types for domain names after enabling QUIC.
>- QUIC requests cannot be forwarded to the origin.
> - QUIC is only partially supported for now.

**Use Limits:**

- QUIC is now not available for on-demand video streaming acceleration.
- QUIC cannot be enabled for any domain names with IPv6 enabled.

2. Disable QUIC:

You can go to **Domain Management** > **HTTPS Configuration** > **QUIC**, and disable QUIC.

## Billing

QUIC support is a value-added service, which is billed based on the number of QUIC requests and supports pay-as-you-go. For details, see [Billing Overview](https://intl.cloud.tencent.com/zh/document/product/228/2949).
