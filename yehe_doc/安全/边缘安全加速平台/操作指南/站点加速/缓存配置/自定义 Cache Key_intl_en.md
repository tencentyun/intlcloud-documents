## Overview
A cache key can be customized to suit your needs by setting the query string, HTTP header and URL case, so that requested resources can be loaded faster.

#### Cache key
A cache key identifies a resource cached on the node. When a resource is requested from the node, it searches for a match in the cache using the complete request URL as the cache key. For example, resources of the URLs `https://www.example.com/images/example.jpg?key1=value1` and `https://www.example.com/images/example.jpg?key2=value2` are identified by their respective query strings and cache keys.

## Use Cases
Use custom cache keys when you want the resources to be served based on the characteristics of client requests, such as the URL query string, URL case, HTTP headers and request protocol.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create rules to configure custom cache keys as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).

Description of configuration items:
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
<td align="left">
Resources to be requested differ according to HTTP request headers. You can specify the HTTP request headers to be concatenated in the URL as part of the cache key.
<ul><li>Custom header: Allow to define custom headers, such as `X-Client-Header`.</li>
<li>Preset header: Allow to specify preset headers that provide information about the `User-Agent` and client IP (such as the device/browser type).</li><ul>
<li>`EO-Client-Device`: The device type.<br>Values: `Mobile`, `Desktop`, `SmartTV`, `Tablet`, `Others`.</li>
<li>`EO-Client-OS`: The client OS.<br>Values: `Android`, `iOS`, `Windows`, `MacOS`, `Linux`, `Others`.</li>
<li>`EO-Client-Browser`: Type of the client browser.<br>Values: `Chrome`，`Safari`, Firefox`, `IE`, `Others`.</li>
<li>`EO-Client-IPCountry`: Location of the client IP.<br>Values: ISO 3166-1 alpha-2 codes, representing two-letter country/region codes defined in ISO 3166-1.</li></td>
</tr>
<tr>
<td align="left">Cookie</td>
<td align="left">The `Cookie` parameter can be adjusted and concatenated in the URL to generate the cache key.</td>
</tr>
<tr>
<td align="left">Request protocol</td>
<td align="left">Whether to distinguish between caches by request protocol (HTTP/HTTPS). By default, they are not distinguished between.</td>
</tr>
</tbody></table>

## Configuration Samples

The following configuration samples shows how to create a custom cache key for the domain name `www.example.com`:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/keQQ087_QQ20221116-120926.png)

The cache key is formed by concatenating the URL (which doesn’t differentiate the request protocol by default and ignores the case and query string), My-Client-Header, and specified Cookie.

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
