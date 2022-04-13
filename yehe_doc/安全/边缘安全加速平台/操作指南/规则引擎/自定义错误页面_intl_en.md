## Overview

If an error status code is specified for origin server response, status code 302 will be returned, and the custom page will be redirected to.
>?
>- Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.
>- This feature is only for redirecting requests encountered status codes during origin-pull, but not applicable to requests with status codes returned by any access control features such as the IP blocklist/allowlist configuration and token authentication.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to create and configure custom error page rules as needed.
>!Currently, you can configure and customize error page rules only if the match condition is **All (any request)** or **Host**.

Parameter description:
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Status code</td>
<td>It specifies the error status code returned by the origin server:<ul><li>4XX: 400, 403, 404, 405, 414, 416, 451</li><li>5XX: 500, 501, 502, 503, 504</li></td>
</tr>
<tr>
<td>Page address</td>
<td>It specifies the error page address, such as <code>http://www.example.com/custom-page.html</code></td>
</tr>
</tbody></table>
