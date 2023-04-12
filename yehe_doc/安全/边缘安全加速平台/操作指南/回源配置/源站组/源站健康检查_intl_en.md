## Overview
A health check task can be created to monitor the availability and health of an origin group. The origin group is considered healthy when it responds appropriately to origin-pull requests, otherwise it is in an unhealthy state.



## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Origin Configuration** > **Origin Group** on the left sidebar. Switch the tab to **Health check**.
![](https://qcloudimg.tencent-cloud.cn/raw/edc351ebd6dd28f8301952959cbf1652.png)
2. On the page displayed, select a target site to create or edit a health check task.
 - Create a health check task: Click **Create health check task**, enter the required parameters, and click **Create**.

<table>
<thead>
<tr>
<th colspan=2>Parameter</th>
<th>Description</th>
<th>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td colspan=2>Select origin group</td>
<td>Select one or more origin groups.</td>
<td><ul><li>The origin groups that you select must be used in <a href="https://intl.cloud.tencent.com/document/product/1145/46353">domain service</a>, i.e., these origin groups are bound to <a href="https://intl.cloud.tencent.com/document/product/1145/46193">load balancing tasks</a>.</li><li>For multiple origin groups bound to the same domain name, associate them with the same health check task.</li><li><a href="https://intl.cloud.tencent.com/document/product/1145/46194">L4 proxied</a> origin groups are not supported currently.</li></td>
</tr>
<tr>
<td rowspan=11>Configure health check task</td>
<td>Task name</td>
<td>Name of the health check task.</td>
<td>-</td>
</tr>
<tr>
 <td>URL</td>
<td>Request URL. The default path is <code>/</code>.</td>
<td>-</td>
</tr>
<tr>
 <td>HTTP method</td>
<td>HTTP request method.</td>
<td>-</td>
</tr>
<tr>
 <td>Check frequency</td>
<td>How often this health check task is initiated.</td>
<td>Checking frequently can detect origin failures more timely, but the origin load will be increased.</td>
</tr>
<tr>
 <td>Timeout period</td>
<td>The amount of time to wait for a response from an origin group until it is considered unhealthy.</td>
<td>-</td>
</tr>
<tr>
 <td>HTTP status code</td>
<td>HTTP status codes to be expected from a healthy origin group.</td>
<td>-</td>
</tr>
<tr>
 <td>Retries</td>
<td>The number of times to retry when the health check result is unhealthy.</td>
<td>-</td>
</tr>
<tr>
 <td>Healthy origins</td>
<td>The number of healthy origin servers required to consider an origin group healthy.</td>
<td>This parameter determines the health status of an origin group based on the number of healthy origin servers. A origin group may contain more than one origin server.</td>
</tr>
<tr>
 <td>Healthy threshold</td>
<td>The number of consecutive successes required for an origin group to be considered healthy and available.</td>
<td>-</td>
</tr>
<tr>
 <td>Follow redirect</td>
<td>Whether to follow 301/302 redirects (3 redirects by default). When it's on, a 301/302 code is returned to report a healthy status.</td>
<td>-</td>
</tr>
<tr>
 <td>Custom request header</td>
<td>Custom request header to send when a health check is initiated.</td>
<td>-</td>
</tr>
</tbody></table>

 - Edit a health check task: Click **edit** on the right of the target task. Modify the parameters and click **Save**.

## Must-knows
1. If an origin group is used for multiple load balancing tasks at the same time, its health is determined based on different load balancing tasks. Suppose an origin group is considered healthy in load balancing task A, while considered unhealthy in load balancing task B. In this case, EdgeOne will notify you via the console, Message Center, email and SMS.
2. If the health check task is not bound to any origin group, or the bound origin group is no longer used for load balancing, the health check task will be suspended.
