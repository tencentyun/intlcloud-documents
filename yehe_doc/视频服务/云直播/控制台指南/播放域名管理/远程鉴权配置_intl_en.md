With remote authentication, after authenticating a push/playback request for hotlink protection, CSS will call your server API to send the request to your server so that you can determine whether the request is legitimate. Based on the result your server returns, CSS will approve or reject the push/playback request. This ensures more precise authentication and improves security. However, you need to develop your own authentication server.

## Workflow
Remote authentication works as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/e0b53fa1bccc5cf193df5312a3b1fa3a.png)

| No. | Description                                                         |
| ---- | ------------------------------------------------------------ |
| 1    | A request is sent to CSS.                               |
| 2    | If remote authentication is enabled for the domain, CSS will process the request as specified and then send it to your authentication server. |
| 3    | Your authentication server returns the result. The HTTP status code 200 indicates that the request should be approved, while the code 403 indicates that the request should be rejected. |
| 4    | CSS approves or rejects the request based on the result.           |

## Prerequisites
- You have activated CSS and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have added a [playback domain name](https://www.tencentcloud.com/document/product/267/35970).

## Configuring Remote Authentication
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Under the **Access Control** tab, find **Remote authentication**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/73648ec779caa4cc2be1be8a7c88931b.png" width=900>
3. Click ![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png) to enable remote authentication and complete the following settings:<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/86867489b1dc604cdd7c4bd5bc4ed3e1.png" width=800>
<table>
<thead><tr><th width="20%">Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Authentication server address</td>
<td>The address of your authentication server (required). Format: <code>http(s)://+Domain or IP address+Port+Path</code>.</td>
</tr><tr>
<td>Request method</td>
<td>POST is selected by default. You can also use HEAD or GET.</td>
</tr><tr>
<td>URL authentication - Parameters to keep</td>
<td>All URL parameters are kept by default. You can also specify parameters to keep or remove all parameters.<ul style="margin:0">
<li>If you select "Keep some", fill in the box the parameters you want to keep. Separate them with |, as in <code>value1|value2</code>.</li>
<li>The parameters are case-sensitive (“key” and “KEY” are different parameters).</li>
</ul></td>
</tr><tr>
<td>URL authentication - Custom parameters to add</td>
<td>Click "Add" to add authentication parameters (max 50). You can either select a parameter to add or add a custom parameter.<ul style="margin:0">
<li>The parameters you can select include "host", "uri", "client_ip", and "cdn_ip", which represent the playback domain, the original request URL, the client IP address, and the CDN IP address respectively.</li>
<li>If you select "Custom", "Parameter" and "Value" are required. The names and values are case-sensitive ("key" and "KEY" are different parameters). Chinese characters are not allowed.</li>
</ul></td>
</tr><tr>
<td>Request header authentication - Request header to keep</td>
<td>All URL parameters are kept by default. You can also specify parameters to keep or remove all parameters.<ul style="margin:0">
<li>If you select "Keep some", fill in the box the parameters you want to keep. Separate them with |, as in <code>value1|value2</code>.</li>
<li>If you select "Keep all", the CDN node will delete the host header. If you want to keep it, select "Keep some" or add a custom parameter.</li>
<li>The parameters are case-insensitive.</li>
</ul></td>
</tr><tr>
<td>Request header authentication - Custom parameters to add</td>
<td>Click "Add" to add authentication parameters (max 50). You can either select a parameter to add or add a custom parameter.<ul style="margin:0">
<li>The parameters you can select include "User-Agent", "Referer", and "X-Forwarded-For", which represent the system and browser information of the user, the referer of the URL, and the URL disguise.</li>
<li>If you select "Custom", "Parameter" and "Value" are required. The names and values are case-insensitive. Chinese characters not allowed.</li>
</ul></td>
</tr><tr>
<td>Timeout period (ms) per try</td>
<td>This is required. Enter a value between 500 and 3000. The default is 3000.</td>
</tr><tr>
<td>Max retries</td>
<td>Enter a value between 0 and 3. The default is 1.</td>
</tr><tr>
<td>Behavior upon timeout</td>
<td>Whether to approve or reject a request if the system does not receive a response (HTTP status code <code>200</code> or <code>403</code>) after the total timeout period elapses (Total timeout period = Timeout period per try x (Max retries + 1)). The default is "Approve". You can also set it to "Reject".</td>
</tr></tbody></table>
4. Click **Save**.



## Modifying Remote Authentication Settings
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Under the **Access Control** tab, find **Remote authentication** and click **Edit**.
3. Modify the settings and click **Save**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/30044c0f1f3cb90cd5f8024e01a5efc8.png" width=800>


## Disabling Remote Authentication
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Under the **Access Control** tab, find **Remote authentication**, and click ![img](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) to disable remote authentication.
