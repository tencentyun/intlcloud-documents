## Overview
A node redirects the URL requested by the client to the destination URL based on the response status code.

## Use cases
The URL redirect used to be generated and returned by the origin server, which can now be constructed and returned by EdgeOne nodes. This reduces the network latency and load consumed to generate the URL redirect, thereby improving the client access performance.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and configure the URL redirect rule as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Configuration item description:
<table>
<thead>
<tr>
<th align="left">Configuration Item</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Destination URL</td>
<td align="left">Destination URL after redirection, such as <code>https://www.example.com/images/foo.jpg</code> and <code>https://www.example.com/foo/bar</code>.</td>
</tr>
<tr>
<td align="left">Carry query parameters</td>
<td align="left">Whether to carry the original query parameters to the destination URL. By default, they are carried.</td>
</tr>
<tr>
<td align="left">Status code</td>
<td align="left">Select the response status code of the redirect. Valid values:<ul><li>302 (default)</li><li>301</li><li>303</li><li>307</li></ul></td>
</tr>
</tbody></table>

## Sample Configuration

If the request URL `https://www.example.com/path/foo.html` is configured with the access URL redirect as follows:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/M9AY760_QQ20221116-120548.png)

Then, when the client requests `https://www.example.com/path/foo.html?key1=value1`, the node will return the 301 status code and redirect it to `https://www.example.com/newpath/bar.html`.
