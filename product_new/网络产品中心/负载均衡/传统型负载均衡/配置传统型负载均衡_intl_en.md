After creating a classic CLB instance, you need to configure a listener to it. The listener listens to requests on the instance and routes traffic to the real server based on the balancing policy.

## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first and select "Classic CLB" as instance type.

## Configuring a Listener
### Step 1. Open the "Listener Management" page
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Select **Instance Management** on the left sidebar.
3. In the instance list, click the ID of the instance to be configured to enter the instance details page.
4. Click the **Listener Management** tab or click **Configure Listener** in the "Operation" column.
![](https://main.qcloudimg.com/raw/3c63dacadca27ea0bb84d015954d741a.png)
5. The "Listener Management" page is as shown below:
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
<td>Listener name</td>
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Listener protocol and listening port</td>
<td>Listener protocol and listening port<br><li>Listener protocol: CLB supports various protocols, including TCP, UDP, HTTP, and HTTPS. TCP is used in this example.</li><li>Listening port: A port used to receive requests and route them to the real server. Port range: 1-65535.</li><li>The listening port must be unique in the same CLB instance.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Backend port</td>
<td>The port through which the CVM provides services, and receives and processes the traffic from the CLB instance.</td>
<td>80</td>
</tr>
</tbody></table>

The specific configuration of the created TCP listener is as shown below:
![](https://main.qcloudimg.com/raw/3773d74e1c13df06f7d70e89e3820624.png)

#### 2. Advanced configuration
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Balancing method | For TCP listeners, CLB supports two scheduling algorithms: weighted round robin (WRR) and weighted least connections (WLC).<br><li>WRR: Requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the <strong>number of new connections</strong>, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: Loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li> | WRR |
| Session persistence status | Enables or disables session persistence<br><li>If session persistence is enabled, the CLB listener will deliver access requests from the same client to the same real server.</li><li>TCP session persistence is implemented based on client IP addresses, i.e., access requests from the same IP address are routed to the same real server.</li><li>Session persistence can be enabled for WRR scheduling but not WLC scheduling.</li> | Enabled |
| Session persistence time | Session persistence time<br><li>If there is no new request in the connection within the session persistence time, session persistence will be interrupted automatically.</li><li>Value range: 30-3,600s.</li> | 30s |

The specific configuration is as shown below:
![](https://main.qcloudimg.com/raw/ddc22b9e0638eb8f2d8803ffee6335f8.png)

#### 3. Health check
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Health check status | Enables or disables health check. In TCP listeners, CLB instances send SYN packets to the specified server port to perform health checks. | Enabled |
| Response timeout period | <li>Maximum response timeout period for health checks.</li><li>If a real server fails to respond correctly within the timeout period, it is considered abnormal.</li><li>Value range: 2-60s. Default value: 2s.</li> | 2s |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300s. Default value: 5s.</li> | 5s |
| Unhealthy threshold | <li>If the health check results received n times (n is the entered number) in a row are failures, the instance will be considered unhealthy, and the status displayed in the console will be **Abnormal**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |
| Healthy threshold | <li>If the health check results received n times (n is the entered number) in a row are successes, the instance will be considered healthy, and the status displayed in the console will be **healthy**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |

The specific configuration of health check is as shown below:
![](https://main.qcloudimg.com/raw/a05f5672d4999a60f6e01b74df38fc6b.png)

### Step 3. Bind a real server
Click **Bind** on the "Listener Management" page and select the real server to be bound in the pop-up window, as shown below:
![](https://main.qcloudimg.com/raw/7ad71ca47183798e8cb54dfd25b9cdb3.png)

Below is a screenshot after configuration:
![](https://main.qcloudimg.com/raw/ef63b9817686f4743408cb6e7fba19f3.png)

>If you configure multiple listeners on a classic CLB instance and bind multiple real servers, each listener will route requests to all real servers according to its own configuration.

### Step 4. Security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [Configuring a CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify/delete a listener (optional)
If you need to modify or delete a created listener, select the listener on the "Listener Management" page and select **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/b4003107882decddea5828bf887dab40.png)
