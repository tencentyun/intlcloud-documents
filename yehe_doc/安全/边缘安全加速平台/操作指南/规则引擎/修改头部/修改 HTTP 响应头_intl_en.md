## Overview
You can customize, add, and delete headers in HTTP responses from nodes to clients, which will not affect the node cache. This feature can implement cross-origin access.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to modify HTTP response header rules as needed.
>!Currently, you can configure and modify HTTP response headers only if the match condition is **All (any request)** or **Host**.

Parameter description:
<table>
<thead>
<tr>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Change</td>
<td>It changes the specified header parameter to the set value.<br>Note:<ul><li>If the specified header doesn't exist, it will be added.</li><li>If the header already exists (even if there are multiple duplicate headers), the original header will be overwritten, and multiple duplicate headers will be merged into one for uniqueness.</td>
</tr>
<tr>
<td>Add</td>
<td>It adds the specified header.<br>Note: <br>If the header already exists (even if there are multiple duplicate headers), the original header will be overwritten, and multiple duplicate headers will be merged into one for uniqueness.</td>
</tr>
<tr>
<td>Delete</td>
<td>It deletes the specified header.</td>
</tr>
</tbody></table>

## Notes
- A header parameter must be in the following format:
  - Parameter name: It can contain 1–100 digits, letters, and hyphens.
  - Parameter value: It can contain 1–1000 characters.
- During one HTTP request header modification operation, you can add up to 30 headers of different types, which will be executed in sequence from top to bottom.
- The following standard headers cannot be modified:
```
Date
Expires
Content-Type
Content-Encoding
Content-Length
Transfer-Encoding
Cache-Control
If-Modified-Since
Last-Modified
Connection
Content-Range
ETag
Accept-Ranges
Age
Authentication-Info
Proxy-Authenticate
Retry-After
Set-Cookie
Vary
WWW-Authenticate
Content-Location
Content-MD5
Content-Range
Meter
Allow
Error
```
