## HTTP Listener Overview
You can create an HTTP listener to a CLB instance to forward HTTP requests from the client. HTTP is suitable for applications where request contents need to be identified, such as web applications and mobile apps.

## Prerequisites
You need to [create a CLB instance](https://intl.cloud.tencent.com/document/product/214/6149) first.

## Configuring an HTTP Listener
### Step 1. Open the **Listener Management** tab
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb).
2. Select **CLB Instance List** on the left sidebar.
3. In the instance list, click an instance ID to enter the details page.
4. Open the **Listener Management** tab. You can also enter the page by clicking **Configure Listener** under the **Operation** column of an instance.
![](https://main.qcloudimg.com/raw/fcb6b1899ee4022fdf154436da99d18c.png)
5. The **Listener Management** tab is as shown below:
![](https://main.qcloudimg.com/raw/f6c44a9d413cae333e53b31184da7fbe.png)

### Step 2. Configure a listener
Click **Create** in the **HTTP/HTTPS Listener** section and configure an HTTP listener in the pop-up window.
#### 1. Create a listener
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Name | Listener name | test-http-80 |
| Listening protocol and port | Listening protocol and port of a listener:<ul style="margin-bottom:0px;"><li>Listening protocol: CLB supports various protocols, including TCP, UDP, TCP SSL, HTTP, and HTTPS. HTTP is used in this example.</li><li>Listening port: A port used to receive requests and forward them to the real server. Port range: 1 - 65535. These ports are reserved and currently unavailable to users: 843, 1020, 1433, 1434, 3306, 3389, 6006, 20000, 36000, 42222, 48369, 56000, and 65010.</li><li>Listening ports of each CLB instance must be unique.</li></ul>| HTTP:80 |

The specific configuration of the created HTTP listener is as shown below:
![](https://main.qcloudimg.com/raw/437e90b575089c2953d701d37b0413b5.png)

#### 2. Create a forwarding rule
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Domain name | Forwarding domain name: <ul style="margin-bottom:0px;"><li>Length: 1 - 80 characters. </li><li>Underscores (_) cannot be the first character. </li><li>Exact and wildcard domain names are supported. </li><li>Regex is supported. </li><li>For detailed configuration rules, please see <a href="https://intl.cloud.tencent.com/document/product/214/9032">Layer-7 Domain Name Forwarding and URL Rules</a>.</li></ul> | www.example.com |
| Default domain name   | <li>If all domain names of the listener are not matched, the system will direct requests to the default domain name, making default access controllable.</li><li>Each listener can be configured with one default domain name only.</li>| Enabled |
| URL path | Forwarding URL path: <ul style="margin-bottom:0px;"><li>Length: 1 - 200 characters. </li><li>Regex is supported. </li><li>For detailed configuration rules, please see <a href="https://intl.cloud.tencent.com/document/product/214/9032">Layer-7 Domain Name Forwarding and URL Rules</a>.</li></ul>| /index |
| Balancing method | For HTTP listeners, CLB supports three scheduling algorithms: weighted round robin (WRR), weighted least connections (WLC), and IP hash.<ul style="margin-bottom:0px;"> <li>WRR: Requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the **number of new connections**, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: Loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li><li>IP hash: Hash keys are used to locate the corresponding servers in the static hash table based on the source IPs of requests. If a server is available and not overloaded, requests will be delivered to it; otherwise, a null value will be returned.</li></ul>| WRR |
| Getting client IP | Enabled by default | Enabled |
| Gzip compression | Enabled by default | Enabled |

Select the HTTP listener for which to create a forwarding rule and click **+** on the right. The specific configuration is as shown below:
![](https://main.qcloudimg.com/raw/2eae81e4a7bcc08aa4d826298e98d742.png)

#### 3. Health check
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Health check status | Health check can be enabled or disabled. In HTTP listeners, CLB instances send HTTP requests to the specified server port to perform health checks. | Enabled |
| Check domain name | Health check domain name: <ul style="margin-bottom:0px;"><li>Length: 1 - 80 characters. </li><li>It defaults to the forwarding domain name.</li><li>Regex is not supported. If your forwarding domain name is a wildcard one, you should specify a fixed one (non-regex) as the health check domain name.</li><li>Supported characters: `a-z` `0-9` `.` `-`.</li></ul> | www.example.com (default value) |
| Check path | Health check path: <ul style="margin-bottom:0px;"><li>Length: 1 - 200 characters. </li><li>It defaults to `/` and must start with `/`.</li><li>Regex is not supported. We recommend specifying a fixed URL path (static page) for health checks.</li><li>Supported characters: `a-z` `A-Z` `0-9` `.` `-` `_` `/` `=` `?`.</li></ul> | / (default value) |
| Response timeout | <li> Maximum response timeout for health checks.</li><li>If a real server fails to respond within the timeout period, the health check is considered abnormal.</li><li>Value range: 2 - 60 seconds. Default value: 2 seconds.</li> | 2 seconds |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5 - 300 seconds. Default value: 5 seconds.</li> | 5 seconds |
| Unhealthy threshold | <li>If the health check result has been failed for n (a custom value) consecutive times, the real server is unhealthy and **Abnormal** is displayed in the console.</li><li>Value range: 2 - 10 times. Default value: 3 times</li> | 3 times |
| Healthy threshold | <li>If the health check result has been successful for n (a custom value) consecutive times, the real server is healthy and **Healthy** is displayed in the console.</li><li>Value range: 2 - 10 times. Default value: 3 times</li> | 3 times |
| HTTP request method | HTTP request method for health checks. Valid values: GET (default value) and HEAD: <ul style="margin-bottom:0px;"><li>If HEAD is used, the server will only return the HTTP header, which can reduce backend overheads and improve request efficiency. The real server must support HEAD.</li><li>If GET is used, the real server must support GET.</li></ul> | GET |
| HTTP status code check | If the status code is of the selected ones, the real server is considered alive (healthy). Value range: http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx. | Multiple ones are selected: http_1xx, http_2xx, http_3xx, and http_4xx. |

The specific configuration of health check is as shown below:
![](https://main.qcloudimg.com/raw/11579d6111c1ef6dc018859d922fadd8.png)

#### 4. Session persistence
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
|Session persistence status | Session persistence can be enabled or disabled: <ul style="margin-bottom:0px;"><li>If session persistence is enabled, the CLB listener will deliver access requests from the same client to the same real server.</li><li>HTTP session persistence is implemented based on cookies, which are implanted into the client by the CLB instance.</li><li>Session persistence can be enabled for WRR scheduling but not for WLC or IP hash scheduling.</li></ul> | Enabled |
| Session persistence period | Session persistence period: <ul style="margin-bottom:0px;"><li>If there is no new request in the connection within the session persistence period, the session will be automatically disconnected.</li><li>Value range: 30 - 3600 seconds.</li></ul> | 30 seconds |

The specific configuration of session persistence is as shown below:
![](https://main.qcloudimg.com/raw/21f1ec9cd3d8b6c37f900ad745e2e5f3.png)

### Step 3. Bind a real server
1. On the **Listener Management** page, select the created listener `HTTP:80`. Click **+** on the left to expand the domain names and URL paths, select the desired URL path, and view the real servers bound to the path on the right of the listener.
![](https://main.qcloudimg.com/raw/fa7531928fc8493bc2da973458568657.png)
2. Click **Bind**, select the target real server, configure the server port and weight in the pop-up window.
 ① Add port: In the **Selected** box on the right, click **Add Port** to add multiple ports for the same CVM instance, such as ports 80, 81, and 82.
 ② Default port: Enter the **Default Port** first and then select the CVM instance. The port of every CVM instance is the default port.
![](https://main.qcloudimg.com/raw/84dae52ca3484eaa09ad5b31a6d9690f.png)
After these three steps are completed, the HTTP listener rule has been configured as shown below:
![](https://main.qcloudimg.com/raw/f307c4e60def622c1207e7e7f61fe942.png)

### Step 4. Security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [CLB Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify and delete a listener (optional)
If you need to modify or delete a created listener, click the listener/domain name/URL path on the **Listener Management** tab and select **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/a537c8b61b8a4977c4acf5b9d8048854.png)


