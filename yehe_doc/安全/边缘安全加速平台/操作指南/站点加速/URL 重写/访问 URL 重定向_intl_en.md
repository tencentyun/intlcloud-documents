
## Overview
The access URL redirection feature redirects the access URL in the request actually initiated by the client to the destination URL, i.e., URL of the cached resource on the node.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the **Rule Engine** page, select the target site and click ![](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure access URL redirection rules as needed.
>!Currently, you can configure access URL redirection only if the condition is **URL path** or **Host and URL path**.

Parameters:
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Destination URL</td>
<td>Destination URL after redirection, such as <code>www.example.com/images/foo.jpg</code> or <code>www.example.com/foo/bar</code>.</td>
</tr>
</tbody></table>

