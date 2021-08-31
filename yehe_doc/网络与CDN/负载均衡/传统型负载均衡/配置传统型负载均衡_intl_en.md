After creating a classic CLB instance, you need to configure a listener for it. The listener listens to requests on the instance and distributes traffic to real servers based on the load balancing policy.

## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first and select "Classic CLB" for **Instance type**.
>!Currently, there are two types of Tencent Cloud accounts: bill-by-EIP/CLB and bill-by-CVM. All Tencent Cloud accounts registered after June 17, 2020 00:00:00 are bill-by-EIP/CLB accounts. For Tencent Cloud accounts registered before June 17, 2020, [check your account types](https://intl.cloud.tencent.com/document/product/684/15246) in the console. Bill-by-EIP/CLB accounts no longer support classic CLB. You can now only purchase a CLB instance.

## Configuring the Listener
### Step 1. Open the **Listener Management** page
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Select **CLB Instance List** on the left sidebar.
3. On the **Instance Management** page, click the ID/Name of the instance to be configured to enter the instance details page.
4. Select the **Listener Management** tab, or click **Configure listener** under the **Operation** column on the **Instance Management** page.
![](https://main.qcloudimg.com/raw/3c63dacadca27ea0bb84d015954d741a.png)
5. The **Listener Management** page is as shown below.
![](https://main.qcloudimg.com/raw/61ff0540f4eccdc24cb5f06f76af5299.png)

### Step 2. Configure a listener
Click **Create** under **Listener Management** and configure a TCP listener in the pop-up window.
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
<td>Listener name.</td>
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Listener Protocol Ports</td>
<td>Listener protocol and listening port<br><li>Listener protocol: CLB supports protocols such as TCP, UDP, HTTP, and HTTPS. This example uses TCP.</li><li>Listening port: used to receive and forward requests to real servers. The port range is 1-65535.</li><li>The listening port must be unique in the same CLB instance.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Backend Port</td>
<td>The port through which the CVM instance provides services, receives and processes traffic from a CLB instance.</td>
<td>80</td>
</tr>
</tbody></table>

To create a TCP listener, complete the basic configuration as shown below:
![](https://main.qcloudimg.com/raw/3773d74e1c13df06f7d70e89e3820624.png)

#### 2. Advanced configuration
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Balance Method | For TCP listeners, CLB supports two scheduling algorithms: weighted round robin (WRR) and weighted least-connection (WLC).<br><li>WRR: requests are forwarded to different real servers sequentially according to their weights. Scheduling is based on the <strong>number of new connections</strong>, where servers with higher weights have more polls (i.e., a higher probability) and servers with the same weight process the same number of connections.</li><li>WLC: loads on servers are estimated according to their number of active connections. Scheduling is based on server loads and weights. If their weights are the same, real servers with fewer active connections will have more polls (i.e., a higher probability).</li> | WRR |
| Session Persistence | Whether to enable or disable session persistence.<br><li>After session persistence is enabled, CLB listener will distribute access requests from the same client to the same real server.</li><li>TCP session persistence is implemented based on client IP address. The access requests from the same IP address are forwarded to the same real server.</li><li>Session persistence can be enabled for WRR scheduling but not WLC scheduling.</li> | Enabled |
| Hold Time | Session persistence time.<br><li>If there is no new request in the connection within the session persistence time, session persistence will be automatically disconnected.</li><li>Value range: 30-3600 seconds.</li> | 30s |

Complete the configuration as shown below:
![](https://main.qcloudimg.com/raw/ddc22b9e0638eb8f2d8803ffee6335f8.png)

#### 3. Health check
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Health Check | Whether to enable or disable health check. In TCP listeners, CLB instances send SYN packets to specified server ports to perform health checks. | Enabled |
| Check Protocol | To be added. | To be added |
| Check Port | To be added. | To be added |
| Response Timeout | <li> Maximum response timeout period for health check.</li><li>If a real server fails to respond within the timeout period, it is considered as unhealthy.</li><li>Value range: 2-60 seconds. Default value: 2s.</li> | 2s |
| Check Interval | <li>Interval between two health checks.</li><li>Value range: 5-300 seconds. Default value: 5s.</li> | 5s |
| Unhealthy Threshold | <li>If the health check returns `failure` for n consecutive times (n is user-defined), the real server is unhealthy and the **unhealthy** status is displayed in the console.</li><li>Value range: 2-10 times. Default value: 3 times</li> | 3 times |
| Healthy Threshold | <li>If the health check returns `success` for n consecutive times (n is user-defined), the real server is healthy and the **healthy** status is displayed in the console.</li><li>Value range: 2-10 times. Default value: 3 times.</li> | 3 times |

Complete the health check configuration as shown below:
![](https://main.qcloudimg.com/raw/a05f5672d4999a60f6e01b74df38fc6b.png)

### Step 3. Bind a real server
Click **Bind** on the **Listener Management** page and select the real server to be bound in the pop-up window, as shown below:
![](https://main.qcloudimg.com/raw/7ad71ca47183798e8cb54dfd25b9cdb3.png)

The configuration is as shown below:
![](https://main.qcloudimg.com/raw/ef63b9817686f4743408cb6e7fba19f3.png)

>?If you configure multiple listeners to a classic CLB instance and bind multiple real servers, each listener will forward requests to all real servers based on its configuration.

### Step 4. Security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [Configuring a CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify or delete a listener (optional)
If you need to modify or delete an existing listener, select the listener on the **Listener Management** page and click **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/b4003107882decddea5828bf887dab40.png)
