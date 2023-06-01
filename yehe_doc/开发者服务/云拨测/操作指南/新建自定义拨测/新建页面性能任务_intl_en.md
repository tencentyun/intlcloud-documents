This document describes how to create a page performance monitoring task to get the webpage experience data by ISP, region, browser version, operating system, or device, so that you can comprehensively know the page performance.

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
<td>Select <b>Page performance</b> on the PC or mobile.</td>
</tr>
<tr>
<td>Test address</td>
<td>Enter the target web application address starting with <code>http://</code> or <code>https://</code>.<br>For example:<br/>1. Domain: http://www.tencent.com<br/>2. Domain and port: http://www.tencent.com:80<br/><b>Note: </b>You need to enter the port when using <b>TCP</b> or <b>UDP</b> in <b>Ping monitoring</b>.
</td>
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
<td>CAT can be used with the Tencent Cloud resource tag feature to perform tag-based sub-account authorization and cost allocation. </td>
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
</table>
 - My testing node group: You can select a common testing node group in **Scenario-based testing nodes** and click **Create testing node group** in the bottom-right corner. Then, you can directly select a common testing node you created from **My testing node group** when creating a task.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/syUR261_28intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
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
<td> IP type</td>
<td>It can be <b>Auto</b>, <b>IPv4</b>, or <b>IPv6</b>.</td>
<td>Auto</td>
</tr>
<tr>
<td>Custom host</td>
<td>It supports polling by IP or random monitoring. Separate IP addresses by comma.<br>For example: <ul style = "margin-bottom: 0px;"><li>IPv4: <code>192.168.2.1,192.168.2.5:img.a.com&#124;192.168.2.1?]:img.a.com&#124;</code></li><li>IPv6: <code>[0:0:0:0:0:0:0:1][8080],[0:0:0:0:0:0:0:2][8081]:www.a.com|]</code></li></ul></td>
<td> -</td>
</tr>
<tr>
<td>Traffic hijacking (elements to be identified)</td>
<td>When a 302 redirect from the page occurs, if the number of elements on the new page exceeds the set value, the page is hijacked. The hijacking details can be selected and viewed on the <a href="https://console.intl.cloud.tencent.com/cat/analyze">Test Statistics</a> page. 
<td> -</td>
</tr>
<tr>
<td>Traffic hijacking (hijacking flag)</td>
<td>Set the key information of the match. The traffic hijacking monitoring collects data when the browsed page reported the 302 error code. The prerequisites are that the page has the 302 element and the monitored basic document reported the 302 error code.</td>
<td> -</td>
</tr>
<tr>
<td>Page tampering</td>
<td>A page is considered tampered with when elements that are not configured in the domain settings appear, such as pop-up ads, floating ads, and redirects.</td>
<td> -</td>
</tr>
<tr>
<td>DNS hijacking allowlist</td>
<td>If the IP from the DNS query is not in the allowlist, hijacking occurred, and the hijacking result can be selected and viewed in the details of the testing statistics. For more information, see <a href="https://www.tencentcloud.com/document/product/1169/52000">Hijacking Monitoring Parameter Description</a>.</td>
<td> -</td>
</tr>
<tr>
<td>DNS hijacking blocklist</td>
<td>If the IP from the DNS query is in the blocklist, hijacking occurred, and the hijacking result can be selected and viewed in the details of the testing statistics. For more information, see <a href="https://www.tencentcloud.com/document/product/1169/52000">Hijacking Monitoring Parameter Description</a>.</td>
<td> -</td>
</tr>
</table>

