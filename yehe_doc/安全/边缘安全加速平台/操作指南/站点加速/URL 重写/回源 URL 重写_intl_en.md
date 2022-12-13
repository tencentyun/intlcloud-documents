## Overview
Based on specified rules, this feature rewrites the user request URL received by the node to the destination URL when the node sends the request to the origin server, which doesn't affect the node cache key.

## Use cases
In certain cases, the URL accessed by the client has been published and should not be modified, but the origin server has changed its URL for certain reasons; or the URL accessed by the client differs from that on the origin server for SEO. Then, you can set origin-pull URL rewrite rules, so that the node can rewrite the origin-pull URL to the actual resource URL on the origin server without changing the URL accessed by the client.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and configure the origin-pull URL rewrite rule as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Configuration item description:
<table>
<thead>
<tr>
<th width="20%">Configuration Item</th>
<th width="80%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Type</td>
<td align="left">Rewrite type:<ul><li>Add a prefix: Add the specified prefix to the request URL. For example, if the request URL is <code>http://www.example.com/path0/index.html</code> and the prefix to be added is `/prefix`, the rewritten URL will be <code>http://www.example.com/prefix/path0/index.html</code>.</li><li> Remove the prefix: Remove the specified prefix from the request URL. For example, if the request URL is <code>http://www.example.com/path0/path1/index.html</code> and the prefix to be removed is `/path0`, the rewritten URL will be <code>http://www.example.com/path1/index.html</code>.</li><li>Replace the complete path: Replace the complete request URL. For example, if the request URL is <code>http://www.example.com/path0/index.html</code> and the path to be replaced is `/new/page.html`, the rewritten URL will be <code>http://www.example.com/new/page.html</code>.</li></ul></td>
</tr>
<tr>
<td align="left">Carry query parameters</td>
<td align="left">Whether to carry the original query parameters to the destination URL. By default, they are carried.</td>
</tr>
</tbody></table>

## Sample Configuration

If the request URL `https://www.example.com/path0/path1/foo.html` is configured with the origin-pull URL rewrite as follows:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/QBFf806_QQ20221116-121138.png)

Then, when the client requests `https://www.example.com/path0/path1/foo.html?key1=value1`, the URL will be rewritten to `https://www.example.com/path1/foo.html` during origin-pull to get the requested resource.