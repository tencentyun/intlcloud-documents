## Overview
By adjusting the query string in the resource URL, configuring case ignoring, and concatenating the HTTP request header, you can customize resource cache keys to optimize node cache, respond to requests for resources based on the business scenario, and improve the loading speed of the requested resources.

#### Cache key
A cache key is the unique ID of a resource cached on a node. When a node responds to a resource request, it will use the complete request URL as the cache key to match the cached resource. For example, `https://www.example.com/images/example.jpg?key1=value1` and `https://www.example.com/images/example.jpg?key2=value2` correspond to different cache keys, as they have different query strings.

## Use Cases
A resource requested by a client is related to the query string in the URL, case sensitivity, HTTP header, or request protocol. You need to configure the cache key as needed so that the client can get the corresponding cache.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and configure the custom cache key as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
   Configuration item description:
<table>
<thead>
<tr>
<th width="20%">Configuration Item</th>
<th width="80%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Query string</td>
<td align="left">The query string in the URL can be adjusted to generate a cache key. By default, all query parameters of the original request are retained. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1145/46174">Query String</a>.</td>
</tr>
<tr>
<td align="left">Ignore case</td>
<td align="left">Whether to ignore the case of the URL. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1145/46181">Case Ignoring</a>.</td>
</tr>
<tr>
<td align="left">HTTP request header</td>
<td align="left">Resources differ by HTTP request header. The specified HTTP request headers can be concatenated to the URL to generate the cache key. You only need to enter the HTTP request header names, for example, `Accept-Language` and `User-Agent`, and the header values will be automatically included in the cache key.</td>
</tr>
<tr>
<td align="left">Cookie</td>
<td align="left">The `Cookie` parameter can be adjusted and concatenated to the URL to generate the cache key.</td>
</tr>
<tr>
<td align="left">Request protocol</td>
<td align="left">Whether to distinguish between caches by request protocol (HTTP/HTTPS). By default, they are not distinguished between.</td>
</tr>
</tbody></table>

## Sample Configuration

If the custom cache key of the domain name `www.example.com` is as follows:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/UfKJ282_QQ20221116-120926.png)

The cache key is formed by concatenating the URL (case-insensitive), My-Client-Header (regardless of the request protocol), and Cookie with specified parameters reserved.

Request A from the client:

URL: `https://www.example.com/path/demo.jpg?key1=value1&key2=value2`.

HTTP request header: Includes `My-Client-Header:fruit`.

Cookie: name1=yummy;name2=tasty;name3=strawberry.

Request B from the client:

URL: `http://www.example.com/path/demo.JPG?key1=value1&key2=value2&key3=value3`.

HTTP request header: Includes `My-Client-Header:fruit`.

Cookie: name1=yummy;name2=tasty;name3=blueberry.

Request C from the client:

URL: `http://www.example.com/path/demo.JPG?key1=value1&key2=value2&key3=value3&key4=value4`.

HTTP request header: Includes `My-Client-Header:sea`.

Cookie: name1=yummy;name2=tasty;name3=fish.


Requests A and B will hit the same cached resource, and request C will hit another.
