This document describes how to create an audio/video experience test task to test video playback on streaming media websites and in applications and get data such as the lag rate, lag duration, and time to first frame, so as to help you improve the video watch experience.

## Directions

1. Log in to the [CAT console](https://console.cloud.tencent.com/cat/probe/tasklist).
2. On the left sidebar, click **Tasks**.
3. Click **Create task** at the top of the **Tasks** page.
4. Configure the basic information as follows:
<table>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
<tr>
<td>Test mode</td>
<td>Select <b>Regular test</b>.</td>
</tr>
<tr>
<td>Task type</td>
<td>Select <b>Audio/Video experience</b> on the PC or mobile.</td>
</tr>
<tr>
<td>Test address</td>
<td>Enter the target web application address starting with <code>http://</code> or <code>https://</code>. For MP4 RTMP streams, indicate <code>mp4</code>.<br>For example:<br>1. http://www.tencent.com<br>2. RTMP stream: rtmp://host/server/mp4:res
</td>
</tr>
<tr>
<td>Test task name</td>
<td>Enter a custom test task name.</td>
</tr>
<tr>
<td>Test frequency</td>
<td>It can be <b>1 minute</b>, <b>5 minutes</b>, <b>10 minutes</b>, <b>15 minutes</b>, <b>30 minutes</b>, <b>60 minutes</b>, or <b>120 minutes</b>. For example, if you select <b>5 minutes</b>, each testing node will be tested once every five minutes.</td>
</tr></table>


5. Configure the testing node as follows:
    i. Select the method: You can select **Recommended testing node group** or **Custom testing node group** (the former contains common nodes).
    ii. Select testing nodes
     - Availability testing nodes: Only network quality and API monitoring tasks are supported. This option is suitable for network quality monitoring, API availability monitoring, and hijacking and blocking detection.
     - Scenario-based testing nodes: This option is suitable for page user experience and streaming lag monitoring, availability testing under poor network conditions, CDN selection, and path optimization. It covers global IDC, PC, and mobile testing nodes.
       - Recommended testing node group: Commonly used and recommended testing nodes.
       - Custom testing node group: Select the region, node type, and testing node on the right box. Node types are as detailed below:
<table>
<tr>
<th>Testing node Type</th>
<th>Description</th>
</tr>
<tr>
<td>IDC</td>
<td>It is the testing node deployed on the PC to test the PC user experience.</td>
</tr>
<tr>
<td>LastMile</td>
<td>It is the testing node deployed on the end user's PC to test the end user's experience on the PC.</td>
</tr>
<tr>
<td>Mobile</td>
<td>It is the testing node deployed on the mobile phone to test the mobile user experience.</td>
</tr></table>
 - My testing node group: You can select a common testing node group in **Scenario-based testing nodes** and click **Create testing node group** in the bottom-right corner. Then, you can directly select a common testing node you created from **My testing node group** when creating a task.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/udUe281_27intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
<dx-alert infotype="explain" title="Suggestions for selection">
**IDC** and **LastMile** have different network environments, and the former is more stable than the latter.
- To test the business availability, you can select the more stable **IDC**.
- To check the access experience and network conditions of end users, we recommend you select **LastMile** or **Mobile** to simulate the user access to an application.
</dx-alert>
6. Configure the test parameters (optional). By default, the system configures common test parameters. You can also customize test rules as follows:
<table>
<tr>
<th>Configuration Item</th>
<th>Description</th>
<th>Default Value</th>
</tr>
<tr>
<td>IP type</td>
<td>It can be <b>Auto</b>, <b>IPv4</b>, or <b>IPv6</b>.</td>
<td>Auto</td>
</tr>
<tr>
<td>Media type</td>
<td>It can be <b>Video</b> or <b>Audio</b>.</td>
<td>Video</td>
</tr>
<tr>
<td>Test duration (sec)</td>
<td>Customize the duration of each test. Value range: 0-60.</td>
<td>30s</td>
</tr>
<tr>
<td>Address type</td>
<td><ul style = "margin-bottom: 0px;">
<li>Resource address: The actual address of the streaming media to be monitored.</li>
<li>Page address: The page address of the streaming media to be monitored.</li></ul>
</td>
<td>Page address</td>
</tr>
<tr>
<td>Custom host</td>
<td>It supports polling by IP or random monitoring. Separate IP addresses by comma.<br>For example:
<ul style = "margin-bottom: 0px;">
<li>IPv4: <code>192.168.2.1,192.168.2.5:img.a.com&#124;192.168.2.1?]:img.a.com&#124;</code></li><li>IPv6: <code>[0:0:0:0:0:0:0:1][8080],[0:0:0:0:0:0:0:2][8081]:www.a.com|]</code></li></ul>
</td>
<td> -</td>
</tr>
<tr>
<td>Resource hijacking allowlist</td>
<td>Allow a DNS IP. If the IP from the DNS query is not in the allowlist, hijacking occurred, and the hijacking result can be selected and viewed in the details of the testing statistics. For more information, see <a href="https://www.tencentcloud.com/document/product/1169/52000">Hijacking Monitoring Parameter Description</a>.</td>
<td> -</td>
</tr>
<tr>
<td>Resource hijacking blocklist</td>
<td>Block a DNS IP. If the IP from the DNS query is in the blocklist, hijacking occurred, and the hijacking result can be selected and viewed in the details of the testing statitics. For more information, see <a href="https://www.tencentcloud.com/document/product/1169/52000">Hijacking Monitoring Parameter Description</a>.</td>
<td> -</td>
</tr>
</table>							
