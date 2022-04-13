
## Overview
The access URL rewrite feature rewrites the access URL in the request actually initiated by the client to the target URL, i.e., URL of the cached resource on the node.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure access URL rewrite rules as needed.
>!Currently, you can configure access URL rewrite only if the match condition is **URL path** or **Host and URL path**.

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

