You can create a [QUIC](https://www.chromium.org/quic) listener to a CLB instance to forward encrypted QUIC requests from the client. For QUIC listeners, the real server can directly get the real client IP.

QUIC (Quick UDP Internet Connection) is a transport layer network protocol designed by Google, multiplexing concurrent data streams using UDP. Compared with the popular TCP+TLS+HTTP2 protocol, QUIC has the following advantages:
- Reduce the time to establish a connection.
- Improve congestion control.
- Multiplex without head-of-line (HOL) blocking.
- Connection migration.

## Use Cases
A QUIC listener supports connection migration. When your network changes, such as frequent switches between 4G and Wi-Fi networks, it can smoothly migrate the connections without interruption. This is suitable for audio/video services, game services, etc.

## Restrictions
- QUIC listener is supported only for CLB but not classic CLB.
- QUIC listener is supported only for CLB instances in VPCs but not the classic network.
- Only IPv4 and IPv6 NAT64 CLB instances support the QUIC listener.

## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first.

## Directions
### Step 1. Configure a listener
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. Select a region in the top-left corner of the CLB instance list page and click **Configure Listener** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/e3b94945c6dbe084ba51e1e22b46b341.png)
3. Under **TCP/UDP/TCP SSL/QUIC Listener**, click **Create** and configure the QUIC listener in the **Create Listener** pop-up window.
    **1. Basic Configuration**
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
<td><span>test-quic-443</span></td>
</tr>
<tr>
<td>Listener Protocol and Ports</td>
<td>
<ul><li>Listener protocol: QUIC is used in this example. After QUIC is selected, CLB can receive QUIC requests made by clients, but TCP is still used between CLB and real server.</li><li>Listener port: a port used to receive requests and forward them to the real server. Port range: 1-65535.</li><li>The listener port must be unique in the same CLB instance.</li></ul></td>
<td>QUIC:443</td>
</tr>
<tr>
<td>SSL parsing method</td>
<td>One-way authentication and mutual authentication are supported.</td>
<td>One-way authentication</td>
</tr>
<tr>
<td>Server certificate</td>
<td>You can select an existing certificate in the <a href="https://console.cloud.tencent.com/ssl">SSL certificate console</a> or upload a certificate.</td>
<td>Existing certificate</td>
</tr>
<tr>
<td>Balancing method</td>
<td>For QUIC listeners, CLB supports two scheduling algorithms: weighted round robin (WRR) and weighted least connections (WLC). <br><ul><li>WRR: Requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the <strong>number of new connections</strong>, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: Loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li></ul></td>
<td>WRR</td>
</tr>
</tbody></table>
 <b>2. Health check</b></br>
For details of health check, see <a href="https://intl.cloud.tencent.com/document/product/214/39251">Configuring Health Check</a>.</td>
<b>3. Session persistence</b>
</br>QUIC listeners don't support session persistence currently.

### Step 2. Bind a backend CVM
1. On the **Listener Management** page, click the created listener `QUIC:443` to view the bound real servers on the right of the listener.
2. Click **Bind**, select the target real server, and configure the server port and weight in the pop-up window.
>? Default port: Enter the **Default Port** first and then select the CVM instance. The port of every CVM instance is the default port.
>

### Step 3. Configure a security group
You need to configure a CLB security group to isolate public network traffic. For more information, see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 4. Modify or delete a listener (optional)
If you need to modify or delete a created listener, click the listener on the **Listener Management** page and click ![](https://qcloudimg.tencent-cloud.cn/raw/4ab10b98316964812832043bbfd99df6.svg) for modification or ![](https://qcloudimg.tencent-cloud.cn/raw/e863cc51c29790d665d53feba800fd90.svg) for deletion.


## References
[Using QUIC Protocol on CLB](https://intl.cloud.tencent.com/document/product/214/37353)
