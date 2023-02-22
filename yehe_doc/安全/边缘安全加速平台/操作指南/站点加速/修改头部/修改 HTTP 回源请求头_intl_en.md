
## Overview
You can customize, add, and delete headers in HTTP origin-pull requests from nodes to the origin.
>?EdgeOne forwards `X-Forwarded-For` and `X-Forwarded-Proto` to the origin by default, so you don't need to configure them.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create rules to configure HTTP request headers as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Description of configuration items:
<table>
<thead>
<tr>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Set</td>
<td>Sets the specified header to the specified value. The header must be unique.<br>Note: If the specified header does not exist, it will be added.</td>
</tr>
<tr>
<td>Add</td>
<td>Adds the specified header.<br>Note: If the header already exists, it will be overwritten for uniqueness.</td>
</tr>
<tr>
<td>Delete</td>
<td>Deletes the specified header.</td>
</tr>
</tbody></table>
Description of header types:
<table>
<thead>
<tr>
<th>Header Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Custom</td>
<td>Custom header.<ul><li>Name: Must be between 1-100 characters, containing numbers, letters and special symbols (<code>-</code>).</li><li>Value: Must be between 1-1000 characters.</td>
</tr>
<tr>
<td>Preset</td>
<td>`User-Agent` header, which contains information about the client: <ul><li>`EO-Client-Device`: The device that the client uses.<br>Values: `Mobile`, `Desktop`, `SmartTV`, `Tablet`, `Others`.</li>
<li>`EO-Client-OS`: The OS that the client uses.<br>Values: `Android`, `iOS`, `Windows`, `MacOS`, `Linux`, `Others`.</li>
<li>`EO-Client-Browser`: The web browser that the client uses.<br>Values: `Chrome`, `Safari`, `Firefox`, `IE`, `Others`.</li>
</td>
</tr>
</tbody></table>


## Notes
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