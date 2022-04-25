## Overview
HTTP/3 (QUIC) requests are supported. QUIC is used to accelerate site requests and improve the data transfer efficiency and security.

#### What is QUIC?
Quick UDP Internet Connections (QUIC) is a general-purpose network protocol. It not only provides a reliability comparable to that of TCP connections, but also greatly reduces the latency in transfer and connections to prevent network congestion while guaranteeing the network security.

EdgeOne currently supports the following QUIC versions: h3-29, h3-Q050, h3-Q046, h3-Q043, Q046, and Q043.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Network optimization** on the left sidebar.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

3. On the network optimization page, select the target site and toggle the HTTP/3 (QUIC) feature on or off.
![](https://qcloudimg.tencent-cloud.cn/raw/9c8d306e5291439d6587f6a3cc677817.png)

**Parameter description:**
 - Disabled status (default): HTTP/3 (QUIC) requests are not supported.
 - Enabled status: HTTP/3 (QUIC) requests are supported, and HTTP/3 (QUIC) is used to accelerate site requests.
>!
>- This feature takes effect only after an HTTPS certificate is configured.
>- HTTP/3 (QUIC) requests in excess of the package quota will be billed in pay-as-you-go mode separately.

## Notes
1. If both HTTP/2 and HTTP/3 (QUIC) are enabled, HTTP/2 or HTTP/3 (QUIC) will be used based on the actual client request conditions.
2. Only HTTP/3 (QUIC) access requests rather than origin-pull requests are supported here.
