You can create a TCP SSL listener to a CLB instance to forward encrypted TCP requests from the client. TCP SSL is applicable to scenarios where ultra-high performance and large-scale TLS offloading are required. For TCP SSL listeners, the real server can directly get the real client IP.
>?TCP SSL listener is currently supported only for CLB but not classic CLB.
>


## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first.

## Directions
### Step 1. Configure a listener
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. Select a region in the top-left corner of the CLB instance list page and click **Configure Listener** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/e3b94945c6dbe084ba51e1e22b46b341.png)
3. Under **TCP/UDP/TCP SSL/QUIC Listener**, click **Create** and configure the TCP SSL listener in the **Create Listener** pop-up window.
 **a. Basic configuration**
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
<td>Listener name.</td>
<td><span>test-tcpssl-9000&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Listener Protocol and Ports</td>
<td><ul><li>Listener protocol: TCP SSL is used in this example.</li><li>Listener port: a port used to receive requests and forward them to the real server. Port range: 1-65535.</li><li>The listener port must be unique in the same CLB instance.</li></ul></td>
<td>TCP SSL:9000</td>
</tr>
<tr>
<td>SSL parsing method</td>
<td>One-way authentication and mutual authentication are supported.</td>
<td>One-way authentication</td>
</tr>
<tr>
<td>Server certificate</td>
<td>You can select an existing certificate in the <a href="https://console.cloud.tencent.com/ssl">SSL Certificates Service</a> or upload a certificate</td>
<td>Existing certificate</td>
</tr>
<tr>
<td>Balancing Method</td>
<td>For TCP SSL listeners, CLB supports two scheduling algorithms: weighted round robin (WRR) and weighted least connections (WLC).<br><ul><li>WRR: requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the <strong>number of new connections</strong>, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li></ul></td>
<td>WRR</td>
</tr>
</tbody></table>
 <b>b. Health check</b></br>
For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/39251">Health Check Configuration</a>.</br>
 <b>c. Session persistence (not supported currently)</b></br>
TCP SSL listeners don't support session persistence currently.

### Step 2. Bind a real server
1. On the **Listener Management** page, click the created listener `TCP SSL:9000` to view the bound real servers on the right of the listener.
2. Click **Bind**, select the target real server, configure the server port and weight in the pop-up window.
>? Default port: enter the **Default Port** first and then select the CVM instance. The port of every CVM instance is the default port.
>

### Step 3. Configure a security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [CLB Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 4. Modify and delete a listener (optional)
If you need to modify or delete a created listener, click the listener on the **Listener Management** page and click ![](https://qcloudimg.tencent-cloud.cn/raw/4ab10b98316964812832043bbfd99df6.svg) for modification or ![](https://qcloudimg.tencent-cloud.cn/raw/e863cc51c29790d665d53feba800fd90.svg) for deletion.
