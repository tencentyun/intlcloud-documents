With remote authentication, after authenticating a playback request, CSS will call an API to send the request to your server so that you can determine whether the request is legitimate. Based on the result your server returns, CSS will determine whether to approve the playback request. This ensures more precise authentication and improves security. However, you need to develop your own authentication server.

## Workflow


| No. | Description                                                         |
| ---- | ------------------------------------------------------------ |
| 1    | A playback request is sent to CSS.                               |
| 2    | If remote authentication is enabled for the playback domain, CSS will process the request as specified and then send it to your authentication server. |
| 3    | Your authentication server returns the result.                           |
| 4    | CSS approves or rejects the request based on the result.           |

## Prerequisites
- You have activated CSS and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have added a [playback domain](https://intl.cloud.tencent.com/document/product/267/35970).

## Configuring Remote Authentication
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Under the **Access Control** tab, find **Remote authentication**.
3. Click ![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png) to enable remote authentication and complete the following settings:


<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Authentication server address</td>
<td>The address of your authentication server (required). Format: http(s)://+Domain or IP address+Port+Path</td>
</tr><tr>
<td>Request method</td>
<td>POST is selected by default. You can also use HEAD or GET.</td>
</tr><tr>
<td>URL authentication</td>
<td>All URL parameters are kept by default. You can also specify parameters to keep or remove all parameters.<ul style="margin:0">
<li>If you select “Keep some”, in the box below, enter the parameters you want to keep. Separate them with commas, as in “value1,value2”.</li>
<li>The parameters are case-sensitive (“key” and “KEY” are different parameters).</li>
</td>
</tr><tr>
<td>Add authentication parameters</td>
<td>Click to add authentication parameters (max 50). You can either select a parameter to add or add a custom parameter.<ul style="margin:0">
<li>The parameters you can select include “host”, “uri”, “query”, “client_ip”, and “cdn_ip”.</li>
<li>If you select “Custom”, “Parameter” and “Value” are required. The names and values are case-sensitive (“key” and “KEY” are different parameters). Chinese characters and spaces are not allowed.</li>
</td>
</tr><tr>
<td>Request header authentication</td>
<td>All URL parameters are kept by default. You can also specify parameters to keep or remove all parameters.<ul style="margin:0">
<li>If you select “Keep some”, in the box below, enter the parameters you want to keep. Separate them with commas, as in “value1,value2”.</li>
<li>If you select “Keep all”, the CDN node will delete the host header. If you want to keep it, select “Keep some” or add a custom parameter.</li>
<li>The parameters are case-insensitive.</li>
</td>
</tr><tr>
<td>Add authentication parameters</td>
<td>Click to add authentication parameters (max 50). You can either select a parameter to add or add a custom parameter.<ul style="margin:0">
<li>The parameters you can select include “user_agent”, “referer”, “content_type”, and “x_forward_for”.</li>
<li>If you select “Custom”, “Parameter” and “Value” are required. The names and values are case-insensitive. Chinese characters and spaces are not allowed.</li>
</td>
</tr><tr>
<td>Timeout period (ms) per try</td>
<td>This is required. Enter a value between 500 and 3000. The default is 3000.</td>
</tr><tr>
<td>Max retries</td>
<td>Enter a value between 0 and 3. The default is 1.</td>
</tr><tr>
<td>Behavior upon timeout</td>
<td>The default is “Approve”. You can also set it to “Reject”.</td>
</tr>
</tbody></table>

4. Click **Save**.

## Modifying Remote Authentication Settings
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Under the **Access Control** tab, find **Remote authentication** and click **Edit**.
3. Modify the settings and click **Save**.

## Disabling Remote Authentication
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Under the **Access Control** tab, find **Remote authentication**, and click ![img](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) to disable remote authentication.