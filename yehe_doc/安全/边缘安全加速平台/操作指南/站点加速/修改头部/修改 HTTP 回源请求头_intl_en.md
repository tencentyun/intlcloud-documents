
## Overview
You can customize, add, and delete headers in HTTP origin-pull requests from nodes to the origin.
>? EdgeOne forwards `X-Forwarded-For` and `X-Forwarded-Proto` to the origin by default, so you don't need to configure them.

## Operation Guide
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
<li>`EO-Client-Browser`: Type of the client browser.<br>Values: `Chrome`，`Safari`, Firefox`, `IE`, `Others`.</li>
</td>
</tr>
</tbody></table>


## Must-knows
- During one HTTP request header modification operation, you can add up to 30 headers of different types, which will be executed in sequence from top to bottom.
- The following standard headers cannot be modified:
<table>
<thead>
<tr>
<td>Accept</td>
<td>Accept-Charset</td>
<td>Accept-Encoding</td>
<td>Accept-Language</td>
</tr>
</thead>
<tbody><tr>
<td>Accept-Ranges</td>
<td>Age</td>
<td>Authorization</td>
<td>Cache-Control</td>
</tr>
<tr>
<td>chunked</td>
<td>close</td>
<td>Connection</td>
<td>Content-Encoding</td>
</tr>
<tr>
<td>Content-Length</td>
<td>Content-Range</td>
<td>Content-Type</td>
<td>Cookie</td>
</tr>
<tr>
<td>Date</td>
<td>Etag</td>
<td>Expect</td>
<td>Expires</td>
</tr>
<tr>
<td>From-Tencent-Lego-Cluster</td>
<td>From-Tencent-Lego-Cluster-Client-Info</td>
<td>From-Tencent-Lego-Cluster-Edge-Server-Info</td>
<td>From-Tencent-Lego-Dsa</td>
</tr>
<tr>
<td>From-Tencent-Lego-Dsa-Client-Info</td>
<td>From-Tencent-Lego-Dsa-Edge-Server-Info</td>
<td>From-Tencent-Lego-Overload</td>
<td>Host</td>
</tr>
<tr>
<td>identity</td>
<td>If-Match</td>
<td>If-Modified-Since</td>
<td>If-None-Match</td>
</tr>
<tr>
<td>If-Range</td>
<td>keep-alive</td>
<td>Last-Modified</td>
<td>Location</td>
</tr>
<tr>
<td>multirange</td>
<td>normal</td>
<td>Pragma</td>
<td>Proxy-Authorization</td>
</tr>
<tr>
<td>Proxy-Connection</td>
<td>Range</td>
<td>Referer</td>
<td>Server</td>
</tr>
<tr>
<td>Server-Timing</td>
<td>Set-Cookie</td>
<td>Transfer-Encoding</td>
<td>upgrade</td>
</tr>
<tr>
<td>Upgrade</td>
<td>Upgrade-Insecure-Requests</td>
<td>User-Agent</td>
<td>Via</td>
</tr>
<tr>
<td>X-Cache-Lookup</td>
<td>X-Forwarded-For</td>
<td>X-Last-Update-Info</td>
<td>x-redirect-to-self</td>
</tr>
<tr>
<td>X-Via</td>
<td>-</td>
<td>-</td>
<td>-</td>
</tr>
</tbody></table>