After creating a Classic CLB instance, you need to configure a listener for it. The listener listens to requests on the instance and forwards traffic to real servers based on the load balancing policy.

## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first and select "Classic CLB" as the instance type.

## Configuring the listener
### Step 1. Open the "Listener Management" page
1. Log into the [CLB Console](https://console.cloud.tencent.com/clb).
2. Select **Instance Management** on the left sidebar.
3. In the instance list, click the ID of the instance to be configured to enter the instance details page.
4. Click the **Listener Management** tab or click **Configure listener** in the "Operation" column.
![](https://main.qcloudimg.com/raw/3c63dacadca27ea0bb84d015954d741a.png)
4. The "Listener Management" page is as shown below.
![](https://main.qcloudimg.com/raw/61ff0540f4eccdc24cb5f06f76af5299.png)

### Step 2. Configure a listener
Click **Create** in **Listener** and configure a TCP listener in the pop-up window.
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
<td>Listener Name</td>
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Listener protocol and port</td>
<td>Listener protocol and listener port<br><li>Listener protocol: CLB supports various protocols, including TCP, TCP, HTTP, and HTTPS. UDP is used in this example.</li><li>Listener port: used to receive and forward requests to real servers, the port value range: 1–65535.</li><li>The listener port must be unique in the same CLB instance.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Backend port</td>
<td>The port through which the CVM provides services, receives and processes the traffic from CLB</td>
<td>80</td>
</tr>
</tbody></table>

The specific configuration for creating a TCP listener is as shown below:
![](https://main.qcloudimg.com/raw/3773d74e1c13df06f7d70e89e3820624.png)

#### 2. Advanced Configuration
| Configuration Item    | Description                    | Example                                 |
| ------- | ------------------------ | ---------------------------------------- |
| Balancing method | For TCP listeners, CLB supports two scheduling algorithms: weighted round-robin (WRR) and weighted least-connection (WLC) <br><li>WRR: requests are sequentially forwarded to different real servers according to their weights. Scheduling is based on the <strong>number of new connections</strong>, where servers with higher weights have more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: loads on servers are estimated according to their number of active connections. Scheduling is based on server loads and weights. If their weights are the same, servers with fewer active connections will have more polls (i.e., a higher probability).</li> | WRR |
| Session persistence status | Whether to enable or disable session persistence<br><li>If session persistence is enabled, the CLB listener will distribute access requests from the same client to the same real server.</li><li>TCP session persistence is implemented based on client IP address, i.e., access requests from the same IP address are forwarded to the same real server.</li><li>Session persistence can be enabled for WRR scheduling but not WLC scheduling.</li> | Enabled |
| Session persistence time | Session persistence time<br><li>If there is no new request in the connection within the session persistence time, session persistence will be automatically disconnected.</li><li>Value range: 30–3,600s.</li> | 30s |

The specific configuration is as shown below:
![](https://main.qcloudimg.com/raw/ddc22b9e0638eb8f2d8803ffee6335f8.png)

#### 3. Health check
| Health Check Configuration Item    | Description                    | Example                                |
| ------- | ------------------------ | ---------------------------------------- |
| Health check status | Whether to enable or disable health check. In TCP listeners, CLB instances send SYN packets to specified server ports to perform health checks. | Enabled |
| Response timeout period | <li> Maximum response timeout period for health checks.</li><li>If a real server fails to respond within the timeout period, it is considered abnormal.</li><li>Value range: 2–60s. Default value: 2s.</li> | 2s |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5–300s. Default value: 5s.</li> | 5s |
| Unhealthy threshold | <li>If the health check results received are failures for n times (n is the entered number) in a row, the instance will be considered unhealthy, and the status displayed in the console will be **abnormal**.</li><li>Value range: 2–10 times. Default value: 3 times</li> | 3 times |
| Healthy threshold | <li>If the health check results received are successes for n times (n is the entered number) in a row, the instance will be considered healthy, and the status displayed in the console will be **healthy**.</li><li>Value range: 2–10 times. Default value: 3 times.</li> | 3 times |

The specific configuration of health check is as shown below:
![](https://main.qcloudimg.com/raw/a05f5672d4999a60f6e01b74df38fc6b.png)

### Step 3. Bind a CVM instance
Click **Bind** on the "Listener Management" page and select the CVM instance to be bound in the pop-up window, as shown below:
![](https://main.qcloudimg.com/raw/7ad71ca47183798e8cb54dfd25b9cdb3.png)

Below is a screenshot after configuration:
![](https://main.qcloudimg.com/raw/ef63b9817686f4743408cb6e7fba19f3.png)

>If you configure multiple listeners to a Classic CLB instance and bind multiple real servers, each listener will forward requests to all real servers according to its configuration.

### Step 4. Configure the security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, please see [Configuring a CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify or delete a listener (optional)
If you need to modify or delete a created listener, select the listener on the "Listener Management" page and select **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/b4003107882decddea5828bf887dab40.png)
