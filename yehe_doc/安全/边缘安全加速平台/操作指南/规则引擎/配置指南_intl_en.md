## Overview
Finer granularities are supported, so you can use conditional statements to flexibly create custom configurations.

## Definitions

| Item     | Description                                                         |
| -------- | :----------------------------------------------------------- |
| Rule     | You can create multiple rules under a single site, and a single rule can contain multiple IF statements.         |
| IF       | Conditional expression, which is followed by a match condition.                               |
| Match condition | It identifies/matches a request and is in the format of `match type + operator + value` such as `URL path = /example/foo.jpg`. |
| And      | Logical AND, which can connect different match conditions, such as `Host = www.example.com And URL path = /example/foo`. |
| Operation     |  <li>Specific operation to be executed by a request that is matched to a condition. It must follow a match condition.</li> <li>A match condition must have an operation.</li> |
| Execution sequence | <li>Multiple IF statements in a single rule will be executed from top to bottom in sequence.</li> <li>Multiple rules under a site will be executed starting from number one from top to bottom in sequence.</li>Note: If an IF statement contains multiple operations, and some of them are authentication operations, authentication operations will be always executed first (top priority) without being subject to the sequence. |

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
3. On the rule engine page, select the target site. The following content is supported:

### Supported actions

| Action       | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| Create a rule   | Click ![](https://qcloudimg.tencent-cloud.cn/raw/9841d7c20f4a9cc1d61f9f7b1f481599.png) to create a rule.                                                 |
| Save and publish | Save the currently edited rule and publish it to the production network for it to take effect.                         |
| Save only     | Save the currently edited rule without releasing it to the production network.                       |
| Sort       | Multiple IF statements in a single rule can be sorted in a custom way.<br>Multiple rules under a single site can be sorted in a custom way. Click ![](https://qcloudimg.tencent-cloud.cn/raw/9137077558f0404693d07da409b6b831.png) and drag and drop items to adjust the order. |
| Enable/Disable rules   | Click the toggle ![](https://qcloudimg.tencent-cloud.cn/raw/ec67f18d322643c8c111c9658ec5ec77.png) to change the status. <li>On: The rule is published to the production network and takes effect.</li><li>Off: The rule is saved but not published to the production network, and does not take effect.</li> |
| Search       | You can search for rules by keyword.                           |

### Supported match conditions

| Condition             | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| HOST                 | Match requests by host, eg: `www.example.com`.          |
| URL path             | Match requests by URL path, eg: `/example/foo/bar`.      |
| Full URL             | Match requests by full URL, eg: `https://www.example.com/foo`. |
| File extension             | Match requests by file extension, eg: jpg, png, or css. |
| File name             | Match requests by file name, eg: "foo" is the file name of the file "foo.jpg".         |
| All (any request) | Match all requests from the current site. We recommend you create a match-all rule that can apply to any request. |



### Supported actions
**Supported operations are subject to the match condition.** For example, if the match condition is URL path, some operations are unavailable (as they don't support the URL granularity).
<table>
<thead>
<tr>
<th>Operation</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td  rowspan=2 >Access control</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46164">Token Authentication</a><br></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46969">Video Dragging</a><br></td>
</tr>
<tr>
 <td  rowspan=6 >Cache configuration</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46175">Node Cache TTL</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46176">Browser Cache TTL</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46177">Offline Caching</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46964">Status Code Cache TTL</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/47615">Custom Cache Key</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/48548">Node Cache Prefresh</a></td>
</tr>
<tr>
 <td  rowspan=4 >Network optimization</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46170">HTTP/3 (QUIC)</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46971">WebSocket</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46970">Real Client IP Header</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46172">Maximum Upload Size</a></td>
</tr>
<tr>
 <td  rowspan=2 >URL rewrite</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46166">Access URL Rewrite</a><br></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46167">Origin-pull URL Rewrite</a><br></td>
</tr>
<tr>
 <td  rowspan=3>Origin-pull optimization</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46182">Smart Acceleration</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46171">HTTP/2</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46966">Range GETs</a></td>
</tr>
<tr>
 <td  rowspan=5 >HTTPS configuration</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46356">Forced HTTPS</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46356">Origin-pull HTTPS</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46356">HSTS</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46356">TLS version</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46356">OCSP stapling</a></td>
</tr>
<tr>
 <td  rowspan=3 >HTTP header modification</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46186">Modifying HTTP Request Header</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46185">Modifying HTTP Response Header</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46965">Host Header Rewrite</a></td>
</tr>
<tr>
<td>Advanced configuration</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46188">Custom Error Page</a></td>
</tr>
</tbody></table>

## Configuration Samples

You can configure the following content to create rules with a finer granularity for the current site `example.com`, customize the cache policies for two subdomains `www.example.com` and `blog.example.com`, and add an HTTP request header to indicate that origin-pull is requested from an EdgeOne node:
#### www.example.com rule
```js.
IF 
Host = www.example.com

THEN
Node cache TTL: Custom time - 10 days
Browser cache TTL: Custom time - 10 days
HTTP request header modification: Add `CDN = EdgeOne`
```

#### blog.example.com rule
```js.
IF
Host = blog.example.com

THEN
Dynamic acceleration: Off
Node cache TTL: Custom time - 30 days
Browser cache TTL: Custom time - 30 days
HTTP request header modification: Add `CDN = EdgeOne`
```
