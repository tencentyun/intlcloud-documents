## Overview

Request origin-pull over the HTTP/2 protocol is supported.

#### What is HTTP/2?
Hypertext Transfer Protocol Version 2 (HTTP/2 or HTTP 2.0) is the second major version of the HTTP protocol. It can effectively reduce the network latency and accelerate site page loading.

## Directions

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and Select **Origin Configuration** > **Rule engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure HTTP/2 origin-pull rules as needed.
>!Currently, you can configure HTTP/2 origin-pull rules only if the match condition is **Host**.

Parameter description:
<table>
<thead>
<tr>
<th>Switch Status</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Enabled</td>
<td>Request origin-pull over the HTTP/2 protocol is enabled.<br>Note: It can take effect only if the origin server supports origin-pull over the HTTPS protocol.</td>
</tr>
<tr>
<td>Disabled</td>
<td>Request origin-pull over the HTTP/2 protocol is disabled.</td>
</tr>
</tbody></table>
