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

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

3. On the rule engine page, select the target site. The following content is supported:

### Supported actions

| Action       | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| Create a rule   | Click ![](https://qcloudimg.tencent-cloud.cn/raw/9841d7c20f4a9cc1d61f9f7b1f481599.png) to create a rule.                                                 |
| Save and release | Save the currently edited rule and release it to the production network for it to take effect.                         |
| Save only     | Save the currently edited rule without releasing it to the production network.                       |
| Sort       | Multiple IF statements in a single rule can be sorted in a custom way.<br>Multiple rules under a single site can be sorted in a custom way. Click ![](https://qcloudimg.tencent-cloud.cn/raw/9137077558f0404693d07da409b6b831.png) and drag and drop items to adjust the order. |
| Rule status   | Status icon ![](https://qcloudimg.tencent-cloud.cn/raw/ec67f18d322643c8c111c9658ec5ec77.png)  after each rule: <li>Enabled: It has been released to the production network and taken effect.</li><li>Disabled: It hasn't been released to the production network, and only the rule content is saved.</li> |
| Search       | You can search for rules by keyword.                           |

### Supported match conditions
>?
>- Only the `=` operator is supported currently.
>- Different match conditions can be connected with only logical AND (`And`).

| Match Condition         |                                                              |
| ---------------- | ------------------------------------------------------------ |
| All (any request) | All requests under the current site.<br>Note: We recommend you use this match condition to create a global rule as the baseline rule. |
| Host             | Subdomain under the current site, such as `www.example.com`, `foo.example.com`, and `foo.bar.example.com`. |
| URL Path         | Request URL path under the current site, such as `/example/foo.jpg` and `/example/foo/bar`. |

### Supported operations
**Supported operations are subject to the match condition.** For example, if the match condition is URL path, some operations are unavailable (as they don't support the URL granularity).
<table>
<thead>
<tr>
<th>Operation</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Access authentication</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46164">Token Authentication</a><br>Requests are authenticated according to the specified signing method.</td>
</tr>
<tr>
 <td  rowspan=2 >URL rewrite</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46166">Access URL Rewrite</a><br>The access URL rewrite feature rewrites the access URL in the request actually initiated by the client to the target URL, i.e., URL of the cached resource on the node.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46167">Origin-pull URL Rewrite</a><br>The origin-pull URL rewrite feature rewrites the URL in the origin-pull request initiated by a node to an origin server to the target URL, which doesn't affect the node cache key.</td>
</tr>
<tr>
<td>Network optimization</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46170">QUIC</a></td>
</tr>
<tr>
 <td  rowspan=6 >Cache configuration</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46174">Query string</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46175">Edge node cache TTL</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46176">Browser cache TTL</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46177">Offline caching</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46181">Case ignoring</a></td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46182">Smart acceleration</a></td>
</tr>
<tr>
<td>Origin-pull configuration</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46171">HTTP/2 origin-pull</a><br>Request origin-pull over the HTTP/2 protocol is supported.</td>
</tr>
<tr>
 <td  rowspan=2 >Header modification</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46186">HTTP request header modification</a><br>You can customize, add, and delete headers in HTTP origin-pull requests from nodes to the origin server.</td>
</tr>
<tr>
 <td><a href="https://intl.cloud.tencent.com/document/product/1145/46185">HTTP response header modification</a><br>You can customize, add, and delete headers in HTTP responses from nodes to clients, which will not affect the node cache.</td>
</tr>
<tr>
<td>Advanced configuration</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1145/46188">Custom error page</a><br>If an error status code is specified for origin server response, status code 302 will be returned, and the custom page will be redirected to.</td>
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
