You can create a TCP listener to a CLB instance to forward TCP requests from the client. TCP is suitable for scenarios that have high requirements for reliability and data accuracy but relatively low requirements for transfer speed, such as file transfer, email messaging, and remote login. For TCP listeners, the real server can directly get the real client IP.

## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first.

## Directions
### Step 1. Configure a listener
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. Select a region in the top-left corner of the CLB instance list page and click **Configure Listener** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/e3b94945c6dbe084ba51e1e22b46b341.png)
3. Under **TCP/UDP/TCP SSL/QUIC Listener**, click **Create** and configure the TCP listener in the **Create Listener** pop-up window.
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
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Listener Protocol and Ports</td>
<td>
<ul><li>Listener protocol: TCP is used in this example.</li><li>Listener port: a port used to receive requests and forward them to the real server. Port range: 1-65535.</li><li>The listener port must be unique in the same CLB instance.</li></ul></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Balancing Method</td>
<td>For TCP listeners, CLB supports two scheduling algorithms: weighted round robin (WRR) and weighted least connections (WLC).<br><ul><li>WRR: requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the <strong>number of new connections</strong>, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li></ul>
<dx-alert infotype="explain" title="">
The listener does not support enabling the session affinity feature after Weighted Least Connection is selected for load balancing.
</dx-alert>
</td>
<td>WRR</td>
</tr>
<tr>
<td>Two-Way RST</td>
<td>If this option is selected, corresponding operations will send RST packets to both ends (client and server) to close the connection; otherwise, two-way RST packets will not be sent, and the persistent connection will exist until it times out.</td>
<td><span>Selected</span></td>
</tr>
</tbody>
</table>	
 <b>b. Health check</b></br>
For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/39251">Health Check Configuration</a>.</br>
<b>c. Session persistence</b>
<table>
<tr>
<th width="15%">Session Persistence Configuration</th>
<th width="70%">Description</th>
<th width="15%">Example</th>
</tr>
<tr>
<td width="15%">Session Persistence Switch</td>
<td width="70%"><ul><li>After session persistence is enabled, CLB listener will distribute access requests from the same client to the same real server.</li><li>TCP session persistence is implemented based on client IP address. The access requests from the same IP address are forwarded to the same real server.</li><li>Session persistence can be enabled for WRR scheduling but not WLC scheduling.</li></ul></td>
<td width="15%">Enabled</td>
</tr>
<tr>
<td width="15%">Session Persistence Duration</td>
<td width="70%">Session persistence duration<br><ul><li>If there is no new request within the connection beyond the session persistence duration, session persistence will be disabled automatically.</li><li>Value range: 30-3600s.</li></ul></td>
<td width="15%">30s</td>
</tr>
</table>	



### Step 2. Bind a real server
1. On the **Listener Management** page, click the created listener `TCP:80` to view the bound real servers on the right of the listener.
2. Click **Bind**, select the target real server, configure the server port and weight in the pop-up window.
>? Default port: enter the **Default Port** first and then select the CVM instance. The port of every CVM instance is the default port.


### Step 3. Configure a security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [CLB Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 4. Modify and delete a listener (optional)
If you need to modify or delete a created listener, click the listener on the **Listener Management** page and click ![](https://qcloudimg.tencent-cloud.cn/raw/4ab10b98316964812832043bbfd99df6.svg) for modification or ![](https://qcloudimg.tencent-cloud.cn/raw/e863cc51c29790d665d53feba800fd90.svg) for deletion.



