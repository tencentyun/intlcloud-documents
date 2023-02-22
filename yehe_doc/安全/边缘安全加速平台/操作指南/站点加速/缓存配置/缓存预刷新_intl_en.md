## Overview
Cached resources are validated via origin-pull before expiration, so that your site can respond to requests more rapidly.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Site Acceleration** > **Cache Configuration** on the left sidebar.
2. On the page that appears, select a target site, and then toggle on the switch in the **Node cache prefresh** card.
![](https://qcloudimg.tencent-cloud.cn/raw/ce9ffd87c7a8c2de9b9fbe8c8b21754a.png)
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>On/Off</td>
<td>The switch is on by default.</td>
</tr>
<tr>
<td>Prefresh interval</td>
<td>Enter an integer between 1-99. Default: 90. Suppose a resource has a 10-second node cache TTL and the prefresh interval is set to 60% of the resource's TTL. In this case, EdgeOne nodes will asynchronously validate the cached resource before its TTL expires.<ul><li>If the resource is valid, the resource's TTL will be reset to 10 seconds.</ll><li>If the resource expires, the newest resource will be fetched from the origin server and the TTL will be reset to 10 seconds.</li></td>
</tr>
</tbody></table>

3. Click **Set** to set a prefresh interval.