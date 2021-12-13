When configuring listeners, you can enable health check to obtain the availability information of real servers. For more information on health check, please see [Health Check Overview](https://intl.cloud.tencent.com/document/product/214/6097).

<span id="postreq"></span>
## Prerequisites
1. Create a CLB instance. For more information, please see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
2. Create a CLB listener.
 - To create a TCP listener, please see more information in [Configuring a TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517).
 - To create a UDP listener, please see more information in [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518).
 - To create a TCP SSL listener, please see more information in [Configuring a TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519).
 - To create an HTTP listener, please see more information in [Configuring an HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515).
 - To create an HTTPS listener, please see more information in [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).

## TCP Listener
Layer-4 TCP listeners support three types of health checks, namely the layer-4 TCP health check, layer-7 HTTP health check, and custom protocol health check.
- TCP health checks are conducted with SYN packets, that is, TCP three-way handshakes are initiated to obtain the status information of backend CVM instances.
- HTTP health checks are conducted by sending HTTP requests to obtain the status information of backend CVM instances.
- Custom protocol health checks are conducted by customizing the input and output content of the application layer protocol to obtain the status information of backend CVM instances.

### Configuring TCP health check
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
2. In the step of **Health Check**, select **TCP** as the protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/45dba40d269d5692fe55e800537a5ff2.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Protocol</td><td>TCP health checks will be conducted if <b>TCP</b> is selected.</td>
</tr>
<tr>
<td>Port</td><td>It is optional. We recommend not specifying the port unless you need to check specific ones. The real server port will be checked if the port is not specified here.</td>
</tr>
<tr>
<td>Show advanced options</td><td>For more information, please see <a href="#advance">Advanced Options</a>.</td>
</tr>
</table>

### Configuring HTTP health check
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
2. In the step of **Health Check**, select **HTTP** as the protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/34162d1e3d350560ca4d0cbb5ccbce40.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Protocol</td><td>HTTP health checks will be conducted if <b>HTTP</b> is selected.</td>
</tr>
<tr>
<td>Port</td><td>It is optional. We recommend not specifying the port unless you need to check specific ones. The real server port will be checked if the port is not specified here.</td>
</tr>
<tr>
<td>Check domain</td><td>Requirements on health check domain names:
<ul>
<li>Length: 1 to 80 characters.</li>
<li>It is the forwarding domain name by default.</li>
<li>Regular expressions are not supported. If your forwarding domain name is a wildcard one, you need to specify a fixed (non-regular) domain name as the health check domain name.</li>
<li>Supported characters: lowercase letters (a to z), digits (0 to 9), decimal points (.), and hyphens (-).</li>
</ul></td>
</tr>
<tr>
<td>Path</td><td>Requirements on health check paths:
<ul>
<li>Length: 1 to 200 characters.</li>
<li>`/` is the default value and should be the first character.</li>
<li>Regular expressions are not supported. We recommend specifying a fixed URL (static webpage) for the health check.</li>
<li>Supported characters: lowercase letters (a to z), uppercase letters (A to Z), digits (0 to 9), decimal points (.), hyphens (-), underscores (_), forward slashes (/), equal signs (=), and question marks (?).</li>
</ul></td>
</tr>
<tr>
<td>HTTP request method</td><td>HTTP request method of health checks. Options: GET (default method) and HEAD.
<ul>
<li>If HEAD is selected, the server will only return the HTTP header information, which can reduce backend overheads and improve request efficiency. The real server must support HEAD.</li>
<li>If GET is selected, the real server must support GET.</li>
</ul></td>
</tr>
<tr>
<td>HTTP version</td><td>HTTP version of the real server.
<ul>
<li>If the version supported by the real server is HTTP 1.0, then the host field of the request does not need authentication, that is, the check domain does not need to be configured.</li>
<li>If the version supported by the real server is HTTP 1.1, then the host field of the request needs authentication, that is, the check domain needs to be configured, or the error code 404 will be returned.</li>
</ul></td>
</tr>
<tr>
<td>Normal status code</td><td>If the status code is of the selected ones, the real server is considered as alive (healthy). Options: http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx. You can select multiple ones.</td>
</tr>
<tr>
<td>Show advanced options</td><td>For more information, please see <a href="#advance">Advanced Options</a>.</td>
</tr>
</table>

### Configuring custom protocol health check
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
2. In the step of **Health Check**, select **HTTP** as the protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/8d90b2ec22f711c3547467ae92d02e98.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Protocol</td><td>Custom protocol health checks will be conducted if <b>Custom Protocol</b> is selected.</td>
</tr>
<tr>
<td>Port</td><td>It is optional. We recommend not specifying the port unless you need to check specific ones. The real server port will be checked if the port is not specified here.</td>
</tr>
<tr>
<td>Input format</td><td>Text and hexadecimal strings are supported.
<ul>
<li>If Text is selected, the text will be converted into a binary string for sending requests and comparing returned results.</li>
<li>If Hexadecimal is selected, the hexadecimal string will be converted into a binary string for sending requests and comparing returned results.</li>
</ul></td>
</tr>
<tr>
<td>Request</td><td>Custom health check request content.</td>
</tr>
<tr>
<td>Return result</td><td>When customizing a health check request, you need to enter the health check return result.</td>
</tr>
<tr>
<td>Show advanced options</td><td>For more information, please see <a href="#advance">Advanced Options</a>.</td>
</tr>
</table>


## UDP Listener
UDP listeners support UDP health checks, which can be conducted by checking ports and running the Ping command.

### Configuring UDP health check - port check
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
2. In the step of **Health Check**, select **Port** as the protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/0437fe0ef1f0206bb8c5e125188ff4f3.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Protocol</td><td>If Port is selected, UDP detection packets will be sent to the backend CVM instance via the VIP (i.e., the IP address used by a CLB instance to provide service to clients), and the IP of the backend CVM instance will be pinged to obtain the backend CVM instance status.</td>
</tr>
<tr>
<td>Port</td><td>It is optional. We recommend not specifying the port unless you need to check specific ones. The real server port will be checked if the port is not specified here.</td>
</tr>
<tr>
<td>Input format</td><td>Text and hexadecimal strings are supported.
<ul>
<li>If Text is selected, the text will be converted into a binary string for sending requests and comparing returned results.</li>
<li>If Hexadecimal is selected, the hexadecimal string will be converted into a binary string for sending requests and comparing returned results.</li>
</ul></td>
</tr>
<tr>
<td>Request</td><td>It is optional. Custom health check request content.</td>
</tr>
<tr>
<td>Return result</td><td>It is optional. When customizing a health check request, you need to enter the health check return result.</td>
</tr>
<tr>
<td>Show advanced options</td><td>For more information, please see <a href="#advance">Advanced Options</a>.</td>
</tr>
</table>


### Configuring UDP health check - Ping command
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
2. In the step of **Health Check**, select **PING** as the protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/b20a1cf59bcdb4d85c27d635eadf8fa9.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Protocol</td><td>If PING is selected, the IP of the backend CVM instance will be pinged to obtain the backend CVM instance status.</td>
</tr>
<tr>
<td>Show advanced options</td><td>For more information, please see <a href="#advance">Advanced Options</a>.</td>
</tr>
</table>


## TCP SSL Listener

### Configuring TCP health check
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
2. In the step of **Health Check**, select **TCP** as the protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/e0257dcb94a83d99b4cc82407724a2ae.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Protocol</td><td>TCP health checks will be conducted if <b>TCP</b> is selected.</td>
</tr>
<tr>
<td>Port</td><td>The health check port and listening port of TCP SSL listeners are the same.</td>
</tr>
<tr>
<td>Show advanced options</td><td>For more information, please see <a href="#advance">Advanced Options</a>.</td>
</tr>
</table>

### Configuring HTTP health check
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
2. In the step of **Health Check**, select **HTTP** as the protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/fe6bb16d3065b906f3df698717719b67.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Protocol</td><td>HTTP health checks will be conducted if <b>HTTP</b> is selected.</td>
</tr>
<tr>
<td>Port</td><td>The health check port and listening port of TCP SSL listeners are the same.</td>
</tr>
<tr>
<td>Check domain</td><td>Requirements on health check domain names:
<ul>
<li>Length: 1 to 80 characters.</li>
<li>It is the forwarding domain name by default.</li>
<li>Regular expressions are not supported. If your forwarding domain name is a wildcard one, you need to specify a fixed (non-regular) domain name as the health check domain name.</li>
<li>Supported characters: lowercase letters (a to z), digits (0 to 9), decimal points (.), and hyphens (-).</li>
</ul></td>
</tr>
<tr>
<td>Path</td><td>Requirements on health check paths:
<ul>
<li>Length: 1 to 200 characters.</li>
<li>`/` is the default value and should be the first character.</li>
<li>Regular expressions are not supported. We recommend specifying a fixed URL (static webpage) for the health check.</li>
<li>Supported characters: lowercase letters (a to z), uppercase letters (A to Z), digits (0 to 9), decimal points (.), hyphens (-), underscores (_), forward slashes (/), equal signs (=), and question marks (?).</li>
</ul></td>
</tr>
<tr>
<td>HTTP request method</td><td>HTTP request method of health checks. Options: GET (default method) and HEAD.
<ul>
<li>If HEAD is selected, the server will only return the HTTP header information, which can reduce backend overheads and improve request efficiency. The real server must support HEAD.</li>
<li>If GET is selected, the real server must support GET.</li>
</ul></td>
</tr>
<tr>
<td>HTTP version</td><td>HTTP version of the real server. Only the HTTP 1.1 is supported. The real server needs to authenticate the host field of the request, that is, the check domain needs to be configured, or the error code 404 will be returned.
</td>
</tr>
<tr>
<td>Normal status code</td><td>If the status code is of the selected ones, the real server is considered as alive (healthy). Options: http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx. You can select multiple ones.</td>
</tr>
<tr>
<td>Show advanced options</td><td>For more information, please see <a href="#advance">Advanced Options</a>.</td>
</tr>
</table>

<span id="http"></span>
## HTTP Listener
### Configuring HTTP health check
1. Configure a listener to the step of **Health Check** as instructed in [Prerequisites](#postreq).
![](https://qcloudimg.tencent-cloud.cn/raw/b274aded44b2d1de9d653737b2ad1822.png)
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td>Health check</td><td>It can be enabled or disabled. We recommend enabling it for automatic checks on backend CVM instances and removal of abnormal ports.</td>
</tr>
<tr>
<td>Check domain</td><td>Requirements on health check domain names:
<ul>
<li>Length: 1 to 80 characters.</li>
<li>It is the forwarding domain name by default.</li>
<li>Regular expressions are not supported. If your forwarding domain name is a wildcard one, you need to specify a fixed (non-regular) domain name as the health check domain name.</li>
<li>Supported characters: lowercase letters (a to z), digits (0 to 9), decimal points (.), and hyphens (-).</li>
</ul></td>
</tr>
<tr>
<td>Path</td><td>The health check path can be set as the root directory of the real server or a specified URL. The requirements are as follows:
<ul>
<li>Length: 1 to 200 characters.</li>
<li>`/` is the default value and should be the first character.</li>
<li>Regular expressions are not supported. We recommend specifying a fixed URL (static webpage) for the health check.</li>
<li>Supported characters: lowercase letters (a to z), uppercase letters (A to Z), digits (0 to 9), decimal points (.), hyphens (-), underscores (_), forward slashes (/), equal signs (=), and question marks (?).</li>
</ul>
</td>
</tr>
<tr>
<td>Response timeout</td><td><ul><li>Maximum response timeout for a health check.</li><li>If a real server fails to respond within the timeout, it is considered as abnormal.</li><li>Value range: 2-60 seconds.</li></ul></td>
</tr>
<tr>
<td>Check interval</td><td><ul><li>Interval between two health checks.</li><li>Value range: 5-300 seconds.</li></ul></td>
</tr>
<tr>
<td>Unhealthy threshold</td><td><ul><li>If the health check result is failed for n (a customizable value) times, it is considered that the backend CVM instance is unhealthy, and the status displayed in the console is **Abnormal**.</li><li>Value range: 2-10 times.</li></ul></td>
</tr>
<tr>
<td>Healthy threshold</td><td><ul><li>If the health check result is successful for n (a customizable value) times, it is considered that the backend CVM instance is healthy, and the status displayed in the console is **Healthy**.</li><li>Value range: 2-10 times. </li></ul></td>
</tr>
<tr>
<td>HTTP request method</td><td>HTTP request method of health checks. Options: GET (default method) and HEAD.
<ul>
<li>If HEAD is selected, the server will only return the HTTP header information, which can reduce backend overheads and improve request efficiency. The real server must support HEAD.</li>
<li>If GET is selected, the real server must support GET.</li>
</ul></td>
</tr>
<tr>
<td>Normal status code</td><td>If the status code is of the selected ones, the real server is considered as alive (healthy). Options: http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx. You can select multiple ones.</td>
</tr>
</table>

## HTTPS Listener
>?If HTTP is selected as the backend protocol of the HTTPS listener's forwarding rules, HTTP health checks will be conducted; if HTTPS is selected, HTTPS health checks will be conducted.
>
For the health check configuration of HTTPS listeners, please see <a href="#http">HTTP Listener</a>.

<span id="advance"></span>
## Advanced Options
| Health Check Configuration    | Description                    | Default Value                              |
| ------- | ------------------------ | ---------------------------------------- |
| Response timeout | <li>Maximum response timeout for a health check.</li><li>If a real server fails to respond within the timeout, it is considered as abnormal.</li><li>Value range: 2-60 seconds.</li> | 2 seconds |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300 seconds.</li> | 5 seconds |
| Unhealthy threshold | <li>If the health check result is failed for n (a customizable value) times, it is considered that the backend CVM instance is unhealthy, and the status displayed in the console is **Abnormal**.</li><li>Value range: 2-10 times.</li> | 3 times |
| Healthy threshold |<li>If the health check result is successful for n (a customizable value) times, it is considered that the backend CVM instance is healthy, and the status displayed in the console is **Healthy**.</li><li>Value range: 2-10 times. </li> | 3 times |
