This document describes how to create a network quality test task to monitor the reliability of the application network and route, DNS resolution accuracy, ICMP latency, and packet loss rate.

## Directions
### Creating a test task
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
<td>Select <b>Network quality</b> on the PC or mobile.</td>
</tr>
<tr>
<td>Test address</td>
<td>Enter the target web application address starting with <code>http://</code> or <code>https://</code>.<br>For example:<br>1. Domain: http://www.tencent.com<br/>2. Domain and port: http://www.tencent.com:80<br/><b>Note: </b>You need to enter the port when using <b>TCP</b> or <b>UDP</b> in <b>Ping monitoring</b>.</td>
</tr>
<tr>
<td>Test task name</td>
<td>Enter a test task name.</td>
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
<td>CAT can be used with the Tencent Cloud resource tag feature to perform tag-based sub-account authorization and cost allocation.</td>
</tr>
</table>

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
</table>
  - My testing node group: You can select a common testing node group in **Scenario-based testing nodes** and click **Create testing node group** in the bottom-right corner. Then, you can directly select a common testing node you created from **My testing node group** when creating a task.
    ![](https://staticintl.cloudcachetci.com/yehe/backend-news/kKUC446_25intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
<dx-alert infotype="explain" title="Suggestions for selection">
**IDC** and **LastMile** have different network environments, and the former is more stable than the latter.
- To test the business availability, you can select the more stable **IDC**.
- To check the access experience and network conditions of end users, we recommend you select **LastMile** or **Mobile** to simulate the user access to an application.
</dx-alert>
6. Configure the test parameters (optional). By default, the system configures common test parameters. You can also customize test rules as follows:
<table>
<th>Configuration Type</th>
<th>Configuration Item</th>
<th>Description</th>
<th>Default Value</th>
</tr>
<tr>
<td>IP type</td>
<td>-</td>
<td>It can be <b>Auto</b>, <b>IPv4</b>, or <b>IPv6</b>.</td>
<td>Auto</td>
</tr>
<tr>
<td rowspan="6">Ping monitoring</td>
<td>Protocol type</td>
<td>It can be <b>ICMP</b>, <b>TCP</b>, or <b>UDP</b>.</td>
<td>ICMP</td>
</tr>
<tr>
<td>Test timeout period (sec)</td>
<td>Define the test timeout period. Value range: 0-60 (excluding `0`).</td>
<td>20 seconds</td>
</tr>
<tr>
<td>Execution interval (sec)</td>
<td>Define the interval for executing Ping test tasks, which can be <b>0.5s</b>, <b>1s</b>, <b>2s</b>, <b>3s</b>, <b>4s</b>, <b>5s</b>, or <b>10s</b>.</td>
<td>0.5s</td>
</tr>
<tr>
<td>Packages</td>
<td>Enter the number of test data packages.</td>
<td>4</td>
</tr>
<tr>
<td>Package size (KB)</td>
<td>Enter the size of the test data package.</td>
<td>32 KB</td>
</tr>
<tr>
<td>Package split</td>
<td>Decide whether to split the test data package as needed.</td>
<td>Split</td>
</tr>
<tr>
<td rowspan="5">DNS monitoring</td>
<td>Test timeout period (s)</td>
<td>Define the test timeout period. Value range: 0-45.</td>
<td>5s</td>
</tr>
<tr>
<td>Query method</td>
<td>It can be <b>Recursive</b> or <b>Iterative</b>.</td>
<td>Recursive</td>
</tr>
<tr>
<td>Specify NS server</td>
<td>It specifies the server for DNS. Enter the NS service address.</td>
<td>-</td>
</tr>
<tr>
<td>dig command</td>
<td>Whether to enable the test result in dig command format.</td>
<td>Disable</td>
</tr>
<tr>
<td>DNS server type</td>
<td>It can be <b>Auto</b>, <b>IPv4</b>, or <b>IPv6</b>.</td>
<td>IPv4</td>
</tr>
<tr>
<td rowspan="2">TRACERT monitoring</td>
<td>Test timeout period (s)</td>
<td>Define the test timeout period. Value range: 0-300 (excluding `0`).</td>
<td>60s</td>
</tr>
<tr>
<td>Maximum number of hops</td>
<td>Enter the number of hops. A route is one hop.</td>
<td>20</td>
</tr>
<tr>
<td rowspan="2">Hijacking monitoring</td>
<td>DNS hijacking allowlist</td>
<td>If the IP from the DNS query is not in the allowlist, hijacking occurred, and the hijacking result can be selected and viewed in the details of the testing statistics. For more information, see <a href="https://www.tencentcloud.com/document/product/1169/52000">Hijacking Monitoring Parameter Description</a>.
</td>
<td>-</td>
</tr>
<tr>
<td>DNS hijacking blocklist</td>
<td>If the IP from the DNS query is in the blocklist, hijacking occurred, and the hijacking result can be selected and viewed in the details of the testing statistics. For more information, see <a href="https://www.tencentcloud.com/document/product/1169/52000">Hijacking Test Parameter Description</a>.
</td>
<td>-</td>
</tr>
</table>



### Batch creating test tasks
>? You can create up to 20 test tasks in batch.

On the **Create task** page, click **+** below the **Task name** and enter the task name and address. The created test tasks will be displayed in the task list.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2axy219_26intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
