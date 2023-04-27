This document describes how to create a API monitoring task to test the API response performance and availability over the GET/POST protocol or port, so as to ensure the user experience and business availability.

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
<td>Select <b>API monitoring</b> on the PC or mobile.</td>
</tr>
<tr>
<td>Test task name</td>
<td>Enter a custom test task name.</td>
</tr>
<tr>
<td>Test frequency</td>
<td>It can be <b>1 minute</b>, <b>5 minutes</b>, <b>10 minutes</b>, <b>15 minutes</b>, <b>30 minutes</b>, <b>60 minutes</b>, or <b>120 minutes</b>. For example, if you select <b>5 minutes</b>, each testing node will be tested once every five minutes.</td>
</tr>
<tr>
<td>Execution time</td>
<td>The task is performed every day by default. You can also customize an execution plan as needed. For example, you can set to execute a test task between 8:00 AM and 9:00 AM on any specified day of the week.</td>
</tr>
<tr>
<td>Task tag</td>
<td>CAT can be used with the Tencent Cloud resource tag feature to perform tag-based sub-account authorization and cost allocation. For more information, see <a href="https://www.tencentcloud.com/document/product/1169/52017">Resource Tag</a>.</td>
</tr>
</table>

5. Configure the testing node as follows:
    i. Select the method: You can select **Recommended testing node group** or **Custom testing node group** (the former contains common nodes).
    ii. Select the testing node:
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
<td>It is the location deployed on the mobile phone to test the mobile user experience.</td>
</tr>
</table>
 - My testing node group: You can select a common testing node group in **Scenario-based testing nodes** and click **Create testing node group** in the bottom-right corner. Then, you can directly select a common testing node you created from **My testing node group** when creating a task.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EDsN042_24intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
<dx-alert infotype="explain" title="Suggestions for selection">
**IDC** and **LastMile** have different network environments, and the former is more stable than the latter.
- To test the business availability, you can select the more stable **IDC**.
- To check the access experience and network conditions of end users, we recommend you select **LastMile** or **Mobile** to simulate the user access to an application.
</dx-alert>
6. Configure the test parameters (optional). By default, the system configures common test parameters. You can also customize test rules as follows:
**HTTP(s):**
<table>
<tr>
<th>Configuration Item</th>
<th>Description</th>
<th>Default Value</th>
</tr>
<tr>
<td>Protocol type</td>
<td>It can be <b>HTTP(s)</b>, <b>SSL</b>, <b>TCP</b>, or <b>UDP</b>.</td>
<td>Auto</td>
</tr>
<tr>
<td>Test address</td>
<td>Enter the target web application address starting with <code>http://</code>.<br>For example:<br>1. Domain: <code>http://www.tencent.com</code><br/>2. Domain and port: <code>http://www.tencent.com:80</code><br/>Note: You need to select the request type for <b>HTTP(s)</b>.</td><td>Plain text</td>
</tr>
<tr>
<td>Character encoding</td>
<td>The encoding type of the content sent, which can be **UTF-8**, **GBK**, **GB2312**, or **Unicode**.</td>
<td>UTF-8</td>
</tr>
<tr>
<td>Custom host</td>
<td>It supports polling by IP or random monitoring. Separate multiple IPs by comma.<br>For example: <ul style = "margin-bottom: 0px;"><li>IPv4: <code>192.168.2.1,192.168.2.5:img.a.com|192.168.2.1?]:img.a.com|</code></li><li>IPv6: <code>[0:0:0:0:0:0:0:1][8080],[0:0:0:0:0:0:0:2][8081]:www.a.com|]</code></li></ul></td>
<td> -</td>
</tr>
<tr>
<td> IP type</td>
<td>The type of the accessed server. Valid values: `Auto` (randomly tests the performance of an IPv4 or IPv6 server); `IPv4` (tests the performance of a specified IPv4 server); `IPv6` (tests the performance of a specified IPv6 server).</td>
<td>-</td>
</tr>
<tr>
<td>Request configuration</td>
<td>Customize the <b>Header</b>, <b>Authentication</b>, <b>Query parameters</b>, and <b>Cookies</b> to be added to an HTTP request.</td>
<td>-</td>
</tr>
<tr>
<td>Verification method</td>
<td>Customize the method to verify API data requests, which can be <b>statusCode</b>, <b>body</b>, or <b>header</b>.</td>
<td>-</td>
</tr>
</table>		
<b>Other configuration items of SSL, TCP, and UDP:</b>

<table>
<tr>
<th>Configuration Item</th>
<th>Description</th>
<th>Default Value</th>
</tr>
<tr>
<td>Request type</td>
<td>You can enter the request content, i.e., the request header information of the protocol, in plain text or binary streams.</td>
<td>-</td>
</tr>
<tr>
<td>Request content</td>
<td>Customize the request content for a API monitoring test.</td>
<td>-</td>
</tr>
<tr>
<td>Verification method</td>
<td><ul style = "margin-bottom: 0px;">
Customize the method to verify API data requests.
<li>No verification: Data integrity is not verified.</li>
<li>Full match: The response data must be exactly the same as the entered data.</li>
<li>Partial match: The response data need to contain part of or all the entered data, and the received data must be greater than the entered data in size.</li>
<li>MD5: The response data is saved as a file for MD5 checksum calculation, and the obtained value needs to be exactly the same as the expected value.</li></ul>
</td>
<td>No verification</td>
</tr>
</table>						
