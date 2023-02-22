## Overview

You can redirect requests to a custom error page for specific error status codes returned by the origin. The redirection is performed when a 302 is returned.
>?Only status codes returned for origin-pull requests are supported.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create rules for configuring a custom error page as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Parameters:
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Status code</td>
<td>Specifies the error status code returned by the origin:<ul><li>4XX: 400, 403, 404, 405, 414, 416, 451</li><li>5XX: 500, 501, 502, 503, 504</li></td>
</tr>
<tr>
<td>Page address</td>
<td>Specifies the error page address, such as <code>http://www.example.com/custom-page.html</code></td>
</tr>
</tbody></table>

## Configuration Sample
The following configuration sample shows how to redirect requests to a custom error page for the 404 Not Found error:
![](https://qcloudimg.tencent-cloud.cn/raw/ef5eb08e2ae402cd5cd9ab782817dc56.png)