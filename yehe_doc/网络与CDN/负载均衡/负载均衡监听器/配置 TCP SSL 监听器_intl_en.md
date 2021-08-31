## TCP SSL Listener Overview
You can create a TCP SSL listener to a CLB instance to forward encrypted TCP requests from the client. TCP SSL is applicable to scenarios where ultra-high performance and large-scale TLS offloading are required. For TCP SSL listeners, the real server can directly get the real client IP.
>The TCP SSL listener feature is currently in beta test and only available to public network CLB but not private network CLB or classic CLB. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB) for application.

## Prerequisites
You need to [create a CLB instance](http://intl.cloud.tencent.com/document/product/214/6149) first.

## Configuring a TCP SSL Listener
### Step 1. Open the "Listener Management" page
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Select **Instance Management** on the left sidebar.
3. In the instance list, click the ID of the instance to be configured to enter the instance details page.
4. Click the **Listener Management** tab or click **Configure Listener** in the "Operation" column.
![](https://main.qcloudimg.com/raw/ec8e5fd6668f0d58a88d6da66a4424e9.png)
5. The "Listener Management" page is as shown below:
![](https://main.qcloudimg.com/raw/5d5f9cdb61a7ea3e4fd88036a7c01d0d.png)

### Step 2. Configure a listener
Click **Create** in **TCP/UDP/TCP SSL Listener** and configure a TCP SSL listener in the pop-up window.
#### 1. Basic configuration
<table>
<thead>
<tr>
<th width="15%">Configuration Item</th>
<th width="70%">Description</th>
<th width="15%">Example</th>
</tr>
</thead>
<tbody><tr>
<td>Name</td>
<td>Listener name</td>
<td><span>test-tcpssl-9000&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Listener protocol and listening port</td>
<td>Listener protocol and listening port. <br><li>Listener protocol: CLB supports various protocols, including TCP, UDP, TCP SSL, HTTP, and HTTPS. TCP SSL is used in this example.</li><li>Listening port: A port used to receive requests and forward them to the real server. Port range: 1-65535.</li><li>The listener port must be unique in the same CLB instance.</li></td>
<td>TCP SSL:9000</td>
</tr>
<tr>
<td>SSL parsing method</td>
<td>One-way authentication and mutual authentication are supported</td>
<td>One-way authentication</td>
</tr>
<tr>
<td>Server certificate</td>
<td>You can select an existing certificate in the <a href="https://console.cloud.tencent.com/ssl">SSL certificate service</a> or upload a certificate</td>
<td>Select the existing certificate cc/UzxFoXsE</td>
</tr>
<tr>
<td>Balancing method</td>
<td>For TCP SSL listeners, CLB supports two scheduling algorithms: weighted round robin (WRR) and weighted least connections (WLC). <br><li>WRR: Requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the <strong>number of new connections</strong>, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: Loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li></td>
<td>WRR</td>
</tr>
</tbody></table>

The specific configuration of the created TCP SSL listener is as shown below:
![](https://main.qcloudimg.com/raw/7107604b6c756183c4ea329c20bcbf00.png)

#### 2. Health check
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Health check status | Health check can be enabled or disabled. In TCP SSL listeners, CLB instances send SYN packets to the specified server port to perform health checks. | Enabled |
| Response timeout period | <li>Maximum response timeout period for health checks.</li><li>If a real server fails to respond correctly within the timeout period, it is considered abnormal.</li><li>Value range: 2-60s. Default value: 2s.</li> | 2s |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300s. Default value: 5s.</li> | 5s |
| Unhealthy threshold | <li>If the health check results received n times (n is the entered number) in a row are failures, the instance will be considered unhealthy, and the status displayed in the console will be **Abnormal**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |
| Healthy threshold | <li>If the health check results received n times (n is the entered number) in a row are successes, the instance will be considered healthy, and the status displayed in the console will be **Healthy**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |

The specific configuration of health check is as shown below:
![](https://main.qcloudimg.com/raw/6d57f6df374edba777d3a8841f50adc2.png)

#### 3. Session persistence (not supported currently)
![](https://main.qcloudimg.com/raw/8cde7bd598be6bdb8d5c300e32c90659.png)

### Step 3. Bind a real server
1. On the "Listener Management" page, click the created listener `TCP SSL:9000` to view the bound real servers on the right of the listener.
![](https://main.qcloudimg.com/raw/6dc93b60bb493c58a067604d69dd309b.png)
2. Click **Bind** and select the real server to be bound and configure the server port and weight in the pop-up window.
 1. Add Port: In the "Selected" box on the right, click **Add Port** to add multiple ports for the same CVM instance, such as ports 80, 81, and 82.
 2. Default Port: Enter the "Default Port" first and then select the CVM instance. The port of every CVM instance is the default port.
![](https://main.qcloudimg.com/raw/0285f5f04916c94c9549baae5bdffda6.png)

After these three steps are completed, the TCP SSL listener rule has been configured as shown below:
![](https://main.qcloudimg.com/raw/bfa1e03aec1f29b24d9bf9929edef49d.png)

### Step 4. Security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [Configuring a CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify/delete a listener (optional)
If you need to modify or delete a created listener, click the listener on the "Listener Management" page and select **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/8a3ddb3d362434e283ec563dcc9e14f5.png)
