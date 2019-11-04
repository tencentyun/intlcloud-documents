## HTTPS Listener Overview
You can create an HTTPS listener to a CLB instance to forward HTTPS requests from the client. HTTPS is suitable for HTTP applications where data transfer needs to be encrypted.

## Prerequisites
You need to [create a CLB instance](http://intl.cloud.tencent.com/document/product/214/6149) first.

## Configuring an HTTPS Listener
### Step 1. Open the "Listener Management" page
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Select **Instance Management** on the left sidebar.
3. In the instance list, click the ID of the instance to be configured to enter the instance details page.
4. Click the **Listener Management** tab or click **Configure Listener** in the "Operation" column.
![](https://main.qcloudimg.com/raw/376f020caf12788e492e7f7300465ea8.png)
5. The "Listener Management" page is as shown below:
![](https://main.qcloudimg.com/raw/43d1a431f8cb19dfe6438f1a7612bca3.png)

### Step 2. Configure a listener
Click **Create** in **HTTP/HTTPS Listener** and configure an HTTPS listener in the pop-up window.
#### 1. Create a listener
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Name | Listener name | test-https-443 |
| Listener protocol and listening port | <br><li>Listener protocol: CLB supports various protocols, including TCP, UDP, TCP SSL, HTTP, and HTTPS. HTTPS is used in this example.</li><li>Listening port: A port used to receive requests and forward them to the real server. Port range: 1-65535.</li><li>The listening port must be unique in the same CLB instance.</li>| HTTPS:443 |
| SSL parsing method | One-way authentication and mutual authentication are supported | One-way authentication |
| Server certificate | You can select an existing certificate in the [SSL certificate service](https://console.cloud.tencent.com/ssl) or upload a certificate | Select the existing certificate cc/UzxFoXsE |

The specific configuration of the created HTTPS listener is as shown below:
![](https://main.qcloudimg.com/raw/6046157bc0455aa3e6381e946d213019.png)

#### 2. Create a forwarding rule
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Domain name | Request domain name. <br> <li>Exact domain names are supported, such as `www.example.com`. Wildcard domain names are also supported, such as `*.example.com` and `www.example.*`, where `*` can appear only once in a single domain name.</li><li>A non-regular domain name can contain the following characters: `a-z`, `0-9`, `.`, and `-`.</li><li>Regex is supported, but they cannot contain the following characters: `"`, `{`, `}`, `;`, `\`, ```, `~`, `'`, and `space`.</li><li>A domain name can contain 1-120 characters.</li> | www.example.com |
| URL path | Request path. <br> <li>The path is in the format of `/` by default, must begin with `/`, and can contain 1-120 characters.</li><li>A non-regular URL path must begin with `/` and can contain the following characters: `a-z`, `A-Z`, `0-9`, `.`, `-`, ` /`, `=`, and `?`.</li><li>Regex is supported.</li><ol><li>Beginning with `=` indicates exact match.</li><li>Beginning with `^~` indicates that the URI begins with a general string and is not regex match.</li><li>Beginning with `~ ` indicates case-sensitive regex match.</li><li>Beginning with `~*` indicates non-case-insensitive regex match.</li><li>`/ ` indicates generic match, where any requests will be matched if there are no other matches.</li><li>A regular URL cannot contain the following characters: `"`, `{`, `}`, `;`, `\`, ```, `~`, `'`, and `space`. </li></ol> | /index |
| Balancing method | For HTTPS listeners, CLB supports three scheduling algorithms: weighted round robin (WRR), weighted least connections (WLC), and IP hash. <br><li>WRR: Requests are sequentially delivered to different real servers according to their weights. Scheduling is done based on the **number of new connections**, where servers with higher weights will undergo more polls (i.e., a higher probability), while servers with the same weight process the same number of connections.</li><li>WLC: Loads of servers are estimated according to the number of active connections to the servers. Scheduling is done based on server loads and weights. If their weights are the same, servers with fewer active connections will undergo more polls (i.e., a higher probability).</li><li>IP hash: Hash keys are used to locate the corresponding servers in the static hash table based on the source IPs of requests. If a server is available and not overloaded, requests will be delivered to it; otherwise, a null value will be returned. | WRR |
| Getting client IP | Enabled by default | Enabled |
| Gzip compression | Enabled by default | Enabled |

Select the HTTPS listener for which to create a forwarding rule and click **+** on the right. The specific configuration is as shown below:
![](https://main.qcloudimg.com/raw/76a619051e14d1985664a1601e9be9ab.png)

#### 3. Health check
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Health check status | Health check can be enabled or disabled. In HTTPS listeners, CLB instances send HTTPS requests to the specified server port to perform health checks. | Enabled |
| Check domain name | Request domain name. <br> <li>The access domain name is used for this parameter by default.</li><li>It can contain 1-120 supported characters: `a-z`, `0-9`, `.`, and `-`.</li><li>Regex is not supported currently.</li><li>If a wildcard domain name is entered, a fixed domain name (non-regular) should be specified as the health check domain name.</li> | Default value (i.e., `www.example.com`) |
| Check path | Request path. <br><li>The path is in the format of `/` by default and must begin with `/`.</li><li>It can contain 1-120 supported characters: `a-z`, `0-9`, `.`, and `-`.</li><li>Regex is not supported currently.</li><li>It is recommended to specify a fixed URL path (static page) for health checks.</li> | Default value (i.e., `/`) |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300s. Default value: 5s.</li> | 5s |
| Unhealthy threshold | <li>If the health check results received n times (n is the entered number) in a row are failures, the instance will be considered unhealthy, and the status displayed in the console will be **Abnormal**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |
| Healthy threshold | <li>If the health check results received n times (n is the entered number) in a row are successes, the instance will be considered healthy, and the status displayed in the console will be **Healthy**.</li><li>Value range: 2-10. Default value: 3.</li> | 3 times |
| HTTP request method | HTTP request method for health checks. Value range: GET, HEAD. Default value: GET.<li>If HEAD is used, the server will only return the HTTP header, which can reduce backend overheads and improve request efficiency; the corresponding real server needs to support HEAD.</li><li>If GET is used, the real server needs to support GET.</li> | GET |
| HTTP status code check | If the status code is the selected one, the real server is considered alive (healthy). Value range: http_1xx, http_2xx, http_3xx, http_4xx, http_5xx. | Multiple selections: http_1xx, http_2xx, http_3xx, http_4xx |

The specific configuration of health check is as shown below:
![](https://main.qcloudimg.com/raw/de01c90e722082daa21415448c443520.png)

#### 4. Session persistence
| Configuration Item | Description | Example |
| ------- | ------------------------ | ---------------------------------------- |
| Session persistence status | Session persistence can be enabled or disabled. <li>If session persistence is enabled, the CLB listener will deliver access requests from the same client to the same real server.</li><li>HTTPS session persistence is implemented based on cookies, which are implanted into the client by the CLB instance.</li><li>Session persistence can be enabled for WRR scheduling but not WLC or IP hash scheduling.</li> | Enabled |
| Session persistence time | Session persistence time</li><li>If there is no new request in the connection within the session persistence time, session persistence will be interrupted automatically.</li><li>Value range: 30-3,600s.</li> | 30s |

The specific configuration of session persistence is as shown below:
![](https://main.qcloudimg.com/raw/b5f1ac8e1a2afec01d749e548d1e0cf1.png)

### Step 3. Bind a real server
1. On the "Listener Management" page, select the created listener `HTTPS:443`. Click **+** on the left to expand the domain names and URL paths, select the desired URL path, and view the real servers bound to the path on the right of the listener.
![](https://main.qcloudimg.com/raw/48419a0fd31748324d84fb474d73cd3a.png)
2. Click **Bind** and select the real server to be bound and configure the server port and weight in the pop-up window.
 1. Add Port: In the "Selected" box on the right, click **Add Port** to add multiple ports for the same CVM instance, such as ports 80, 81, and 82.
 2. Default Port: Enter the "Default Port" first and then select the CVM instance. The port of every CVM instance is the default port.
![](https://main.qcloudimg.com/raw/dc56fe828615fe560e9cd2c708be8d56.png)

After these three steps are completed, the HTTPS listener rule has been configured as shown below:
![](https://main.qcloudimg.com/raw/23ce41ef935f0093c1513cecae9323de.png)

### Step 4. Security group (optional)
You can configure a CLB security group to isolate public network traffic. For more information, see [Configuring a CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).

### Step 5. Modify/delete a listener (optional)
If you need to modify or delete a created listener, click the listener/domain name/URL path on the "Listener Management" page and select **Modify** or **Delete**.
![](https://main.qcloudimg.com/raw/97e5fd6249d5017c2fd30891c9369313.png)
