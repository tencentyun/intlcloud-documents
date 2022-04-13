## Overview

The origin-pull URL rewrite feature rewrites the URL in the origin-pull request initiated by a node to an origin server to the target URL, which doesn't affect the node cache key.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure origin-pull URL rewrite rules as needed.
>!Currently, you can configure origin-pull URL rewrite only if the match condition is **URL path** or **Host and URL path**.

Parameter description:
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Target URL</td>
<td>Target URL after rewrite, such as <code>www.example.com/images/foo.jpg</code> or <code>www.example.com/foo/bar</code>.</td>
</tr>
</tbody></table>

