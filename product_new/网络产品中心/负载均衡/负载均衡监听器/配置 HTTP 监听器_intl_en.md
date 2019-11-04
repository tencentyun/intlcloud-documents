## HTTP Listener Overview
You can create an HTTP listener to a CLB instance to forward HTTP requests from the client. HTTP is suitable for applications where request contents need to be identified, such as web applications and mobile apps.

## Prerequisites
You need to [create a CLB instance](http://intl.cloud.tencent.com/document/product/214/6149) first.

## Configuring an HTTP Listener
### Step 1. Open the "Listener Management" page
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Select **Instance Management** on the left sidebar.
3. In the instance list, click the ID of the instance to be configured to enter the instance details page.
4. Click the **Listener Management** tab or click **Configure Listener** in the "Operation" column.
![](https://main.qcloudimg.com/raw/376f020caf12788e492e7f7300465ea8.png)
5. The "Listener Management" page is as shown below:
 ![](https://main.qcloudimg.com/raw/7f864bc406a222e937e5d68bafc17a5a.png)

### Step 2. Configure a listener
Click **Create** in **HTTP/HTTPS Listener** and configure an HTTP listener in the pop-up window.
#### 1. Create a listener
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Name | Listener name | test-http-80 |
| Listener protocol and listening port | <br><li>Listener protocol: CLB supports various protocols, including TCP, UDP, TCP SSL, HTTP, and HTTPS. HTTP is used in this example.</li><li>Listening port: A port used to receive requests and forward them to the real server. Port range: 1-65535.</li><li>The listening port must be unique in the same CLB instance.</li>| HTTP:80 |

The specific configuration of the created HTTP listener is as shown below:
![](https://main.qcloudimg.com/raw/b2843d7255b411cbb535d4a0f507dd69.png)

#### 2. Create a forwarding rule
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Domain name | Request domain name. <br><li>Exact domain names are supported, such as `www.example.com`. Wildcard domain names are also supported, such as `*.example.com` and `www.example.*`, where `*` can appear only once in a single domain name.</li><li>A non-regular domain name can contain the following characters: `a-z`, `0-9`, `.`, and `-`.</li><li>Regex is supported, but they cannot contain the following characters: `"`, `{`, `}`, `;`, `\`, ```, `~`, `'`, and `space`.</li><li>A domain name can contain 1-120 characters.</li> | www.example.com |
| URL path | Request path. <br><li>The path is in the format of `/` by default, must begin with `/`, and can contain 1-120 characters.</li><li>A non-regular URL path must begin with ` /` and can contain the following characters: `a-z`, `A-Z`, `0-9`, `.`, `-`, `/`, `=`, and `?`.</li><li>Regex is supported.</li><ol><li>Beginning with `=` indicates exact match.</li><li>Beginning with `^~` indicates that the URI begins with a general string and is not regex match.</li><li>Beginning with `~ ` indicates case-sensitive regex match.</li><li>Beginning with `~*` indicates non-case-sensitive regex match.</li><li>`/ ` indicates generic match, where any requests will be                                                                                     matched if there are no other matches.</li><li>A regular URL cannot contain the following characters: `"`, `{`, `}`, `;`, `\`, ```, `~`, `'`, and `space`. </ol>| /index |
| Balancing method | For HTTP listeners, CLB supports three scheduling algorithms: weighted round robin (WRR), weighted least connections (WLC), and IP hash.<li>WRR: Requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the **number of new connections**, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: Loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li><li>IP hash: Hash keys are used to locate the corresponding servers in the static hash table based on the source IPs of requests. If a server is available and not overloaded, requests will be delivered to it; otherwise, a null value will be returned.</li>| WRR |
| Getting client IP | Enabled by default | Enabled |
| Gzip compression | Enabled by default | Enabled |

Select the HTTP listener for which to create a forwarding rule and click **+** on the right. The specific configuration is as shown below:
![](https://main.qcloudimg.com/raw/ca73b8816fd88ab76b0cd17a5f7b911e.png)

#### 3. Health check
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Health check status | Health check can be enabled or disabled. In HTTP listeners, CLB instances send HTTP requests to the specified server port to perform health checks. | Enabled |
| Check domain name | Request domain name. <br><li>The forwarding domain name is used for this parameter by default.</li><li>It can contain 1-120 supported characters: `a-z`, `0-9`, `.`, and `-`.</li><li>Regex is not supported currently.</li><li>If a wildcard domain name is entered, a fixed domain name (non-regular) should be specified as the health check domain name.</li> | Default value (i.e., `www.example.com`) |
| Check path | Request path. <br><li>The path is in the format of `/` by default and must begin with `/`.</li><li>It can contain 1-120 supported characters: `a-z`, `0-9`, `.`, and `-`.</li><li>Regex is not supported currently.</li><li>It is recommended to specify a fixed URL path (static page) for health checks.</li> | Default value (i.e., `/`) |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300s. Default value: 5s.</li> | 5s |
| Unhealthy threshold | <li>If the health check results received n times (n is the entered number) in a row are failures, the instance will be considered unhealthy, and the status displayed in the console will be **Abnormal**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |
| Healthy threshold | <li>If the health check results received n times (n is the entered number) in a row are successes, the instance will be considered healthy, and the status displayed in the console will be **Healthy**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |
| HTTP request method | HTTP request method for health checks. Value range: GET, HEAD. Default value: GET.<li>If HEAD is used, the server will only return the HTTP header, which can reduce backend overheads and improve request efficiency; the corresponding real server needs to support HEAD.</li><li>If GET is used, the real server needs to support GET.</li> | GET |
| HTTP status code check | If the status code is the selected one, the real server is considered alive (healthy). Value range: http_1xx, http_2xx, http_3xx, http_4xx, http_5xx. | Multiple selections: http_1xx, http_2xx, http_3xx, http_4xx |

The specific configuration of health check is as shown below:
![](https://main.qcloudimg.com/raw/831f571073ccf0efc2fe6ba3ccd31c99.png)

#### 4. Session persistence
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Session persistence status | Session persistence can be enabled or disabled. <br><li>If session persistence is enabled, the CLB listener will deliver access requests from the same client to the same real server.</li><li>HTTP session persistence is implemented based on cookies, which are implanted into the client by the CLB instance.</li><li>Session persistence can be enabled for WRR scheduling but not WLC or IP hash scheduling.</li> | Enabled |
| Session persistence time | Session persistence time. <br><li>If there is no new request in the connection within the session persistence time, session persistence will be interrupted automatically.</li><li>Value range: 30-3,600s.</li> | 30s |

The specific configuration of session persistence is as shown below:
![](https://main.qcloudimg.com/raw/457a0179ac0db0201cd69d20098cad2e.png)

### Step 3. Bind a real server
1. On the "Listener Management" page, select the created listener `HTTP:80`. Click **+** on the left to expand the domain names and URL paths, select the desired URL path, and view the real servers bound to the path on the right of the listener.
![](https://main.qcloudimg.com/raw/45ab9753f5295b3ab9b4b8018695a5be.png)
2. Click **Bind** and select the real server to be bound and configure the server port and weight in the pop-up window.
 1. Add Port: In the "Selected" box on the right, click **Add Port** to add multiple ports for the same CVM instance, such as ports 80, 81, and 82.
 2. Default Port: Enter the "Default Port" first and then select the CVM instance. The port of every CVM instance is the default port.
![](https://main.qcloudimg.com/raw/da45ac2c8ef8eae6a32b31a2502919b6.png)

After these three steps are completed, the HTTP listener rule has been configured as shown below:
![](https://main.qcloudimg.com/raw/52150fde0ac149fa34c58f89bfc5d37a.png)

### Step 4. Security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [Configuring a CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify/delete a listener (optional)
If you need to modify or delete a created listener, click the listener/domain name/URL path on the "Listener Management" page and select **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/94df509ce8533a6934bc8587acd99bdf.png)
