
## Overview
You can customize, add, and delete headers in HTTP origin-pull requests from nodes to the origin server.
>?By default, EdgeOne supports origin-pull with `X-Forwarded-For` and `X-Forwarded-Proto`, which no longer needs to be configured.
>

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and modify HTTP request header rules as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Configuration item description:
<table>
<thead>
<tr>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Set</td>
<td>It changes the specified header parameter to the set value.<br>Note:<ul><li>If the specified header doesn't exist, it will be added.</li><li>If the header already exists, the original header will be overwritten for uniqueness.</li></td>
</tr>
<tr>
<td>Add</td>
<td>It adds the specified header.<br>Note: If the header already exists, the original header will be overwritten for uniqueness.</td>
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
<table>
<thead>
<tr>
<td align="left">Host</td>
<td align="left">Content-Length</td>
<td align="left">If-Modified-Since</td>
<td align="left">Etag</td>
</tr>
</thead>
<tbody><tr>
<td align="left">Accept-Encoding</td>
<td align="left">Last-Modified</td>
<td align="left">Content-Range</td>
<td align="left">Content-Type</td>
</tr>
<tr>
<td align="left">X-Cache-Lookup</td>
<td align="left">X-Last-Update-Info</td>
<td align="left">Transfer-Encoding</td>
<td align="left">Content-Encoding</td>
</tr>
<tr>
<td align="left">Connection</td>
<td align="left">Range</td>
<td align="left">Server</td>
<td align="left">Date</td>
</tr>
<tr>
<td align="left">Location</td>
<td align="left">Expect</td>
<td align="left">Cache-Control</td>
<td align="left">Expires</td>
</tr>
<tr>
<td align="left">Referer</td>
<td align="left">User-Agent</td>
<td align="left">Cookie</td>
<td align="left">X-Forwarded-For</td>
</tr>
<tr>
<td align="left">Accept-Language</td>
<td align="left">Accept-Charset</td>
<td align="left">Accept-Ranges</td>
<td align="left">Set-Cookie</td>
</tr>
<tr>
<td align="left">Via</td>
<td align="left">X-Via</td>
<td align="left">Pragma</td>
<td align="left">Upgrade</td>
</tr>
<tr>
<td align="left">If-None-Match</td>
<td align="left">If-Match</td>
<td align="left">If-Range</td>
<td align="left">From-Tencent-Lego-Cluster</td>
</tr>
<tr>
<td align="left">From-Tencent-Lego-Cluster-Client-Info</td>
<td align="left">From-Tencent-Lego-Cluster-Edge-Server-Info</td>
<td align="left">From-Tencent-Lego-Dsa</td>
<td align="left">From-Tencent-Lego-Dsa-Client-Info</td>
</tr>
<tr>
<td align="left">From-Tencent-Lego-Dsa-Edge-Server-Info</td>
<td align="left">Accept</td>
<td align="left">Upgrade-Insecure-Requests</td>
<td align="left">Server-Timing</td>
</tr>
<tr>
<td align="left">Age</td>
<td align="left">Proxy-Connection</td>
<td align="left">Authorization</td>
<td align="left">Proxy-Authorization</td>
</tr>
<tr>
<td align="left">normal</td>
<td align="left">multirange</td>
<td align="left">chunked</td>
<td align="left">identity</td>
</tr>
<tr>
<td align="left">keep-alive</td>
<td align="left">close</td>
<td align="left">upgrade</td>
<td align="left">x-redirect-to-self</td>
</tr>
<tr>
<td align="left">From-Tencent-Lego-Overload</td>
<td align="left">-</td>
<td align="left">-</td>
<td align="left">-</td>
</tr>
</tbody></table>
