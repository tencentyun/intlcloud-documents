## Overview
HTTP/2 (HTTP 2.0) requests are supported to accelerate sites and improve the web performance.

#### What is HTTP/2?
Hypertext Transfer Protocol Version 2 (HTTP/2 or HTTP 2.0) is the second major version of the HTTP protocol. It can effectively reduce the network latency and accelerate site page loading.


## Prerequisites
- This feature takes effect only after an HTTPS certificate is configured.
- Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.



## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Network optimization** on the left sidebar.
2. On the network optimization page, select the target site and toggle the HTTP/2 feature on or off.
![](https://qcloudimg.tencent-cloud.cn/raw/b419e71ee31f9f1f3cb15a4a7d1e12c3.png)
**Parameter description:**
 - Enabled status (default): HTTP/2 is used to accelerate sites.
>! This feature takes effect only after an HTTPS certificate is configured.
>
 - Disabled status: HTTP/2 is not used to accelerate sites.

## Notes
1. If a client doesn't support HTTP/2, HTTP 1.x will be used.
2. Only HTTP/2 access requests rather than origin-pull requests are supported here. You can configure HTTP/2 origin-pull on the [rule engine](https://intl.cloud.tencent.com/document/product/1145/46151) page.
