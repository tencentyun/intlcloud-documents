A CLB instance can periodically send ping commands to real servers, attempt to connect with or send requests to them to check their running status. These are called "health check". It uses health checks to determine the availability of real servers and prevent exceptional real servers from affecting frontend services, thereby improving overall service availability.
- If a real server is confirmed as exceptional, the CLB instance will automatically distribute new requests to other normal servers instead of forwarding them to the exceptional server; after the exceptional server returns to the normal state, the CLB instance will automatically restore its service and distribute new requests to it again.
- After health check is enabled, regardless of the weights of real servers (including 0), the CLB instance will always perform health check.
- An auto scaling group will periodically use a similar method to check the running status of each instance in the group. For more information, please see [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).

## Health Check Configuration for Layer-4 Forwarding
The health check mechanism for layer-4 forwarding is as follows: CLB initiates an access request to the server port specified in the configuration. If access to the port is normal, the real server is considered healthy. Otherwise, it is considered unhealthy.
For TCP business, SYN packets are used for health check. For UDP business, the ping command is used.

| Health Check Configuration    | Description                    | Default Value                               |
| ------- | ------------------------ | ---------------------------------------- |
| Response timeout period | <li>Maximum response timeout period for health check.</li><li>If a real server fails to respond properly within the timeout period, it is considered as having an exception.</li><li>Value range: 2–60s.</li> | 2s |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5–300s. </li> | 5s |
| Unhealthy threshold | <li>If the health check results received are failures for n times (n is the entered number) in a row, the real server will be considered as unhealthy, and the status displayed in the console will be **unhealthy**.</li><li>Value range: 2–10.</li> | 3 times |
| Healthy threshold | <li>If the health check results received are successes for n times (n is the entered number) in a row, the real server will be considered as healthy, and the status displayed in the console will be **healthy**.</li><li>Value range: 2–10.</li> | 3 times |

## Health check configuration for Layer-7 forwarding

The health check mechanism for layer-7 forwarding is as follows: CLB sends an HTTP request to the real server for health check. CLB determines whether the server is healthy based on the HTTP return value. For example, assume HTTP return values include `http_1xx`, `http_2xx`, `http_3xx`, `http_4xx` and `http_5xx`, users can define `http_1xx` and `http_2xx` as normal status based on their business needs, and configure `http_3xx` to `http_5xx` as unhealthy status.

| Health Check Configuration    | Description                    | Default Value                                |
| ------- | ------------------------ | ---------------------------------------- |
| Check domain name | Health check domain name: <ul style="margin-bottom:0px;"><li>It can contain 1–80 characters. </li><li>It is the forwarded domain name by default. </li><li>Regex is not supported. If your forwarded domain name is a wildcard domain name, you should specify a fixed one (non-regex) as the health check domain name. </li><li>Supported characters: `a–z`, `0–9`, `.`, `-`. </li></ul> | Forwarded domain name |
| Check path | Health check path: <ul style="margin-bottom:0px;"><li>It can contain 1–200 characters. </li><li>It is `/` by default and must begin with `/`. </li><li>Regex is not supported. You are recommended to specify a fixed URL path (static page) for health checks. </li><li>Supported characters: `a–z`, `A–Z`, `0–9`, `.`, `-`, `_`, `/`, `=`, `?`. </li></ul>  | `/` |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5–300s. </li> | 5s |
| Unhealthy threshold | <li>If the health check results received are failures for n times (n is the entered number) in a row, the real server will be considered as unhealthy, and the status displayed in the console will be **unhealthy**.</li><li>Value range: 2–10.</li> | 3 times |
| Healthy threshold | <li>If the health check results received are successes for n times (n is the entered number) in a row, the real server will be considered as healthy, and the status displayed in the console will be **healthy**.</li><li>Value range: 2–10.</li> | 3 times |
| HTTP request method | HTTP request method for health checks. Valid values: GET, HEAD. <ul style="margin-bottom:0px;"><li>If HEAD is used, the server will only return the HTTP header, which can reduce backend overheads and improve request efficiency. The corresponding real server must support HEAD.</li><li>If GET is used, the real server must support GET.</li></ul> | GET |
| HTTP status code check | If the status code is the selected one, the real server is considered alive (healthy). Valid values: http_1xx, http_2xx, http_3xx, http_4xx, http_5xx. | http_1xx, http_2xx, http_3xx, http_4xx |

## Health Check Status
According to the health check detection conditions, the health check status of a real server may be one of the following four options:

| Status | Description | Whether to Forward Traffic |
| ------- | ----------- | ---------------- |
| Detecting | This is the state of the newly bound real server during the period of check interval * health threshold; for example, if the check interval is 2 seconds and the health threshold is 3 times, this will be state within 6 seconds. | CLB does not forward traffic to the real server in "detecting" status. |
| Healthy | The real server is normal. | CLB forwards traffic to the "healthy" real server. |
| Exceptional | The real server is exceptional. | <li>CLB does not forward traffic to "exceptional" real servers. </li><li>Under a layer-4 listener or layer-7 URL rule, if CLB detects that all real servers are unhealthy, it will activate the all-dead-all-alive logic, that is, requests will be forwarded to all real servers. </li>|
| Disabled | Health check has been disabled. | CLB forwards traffic to the real server. |

## How to Troubleshoot Health Check Issues
### Troubleshooting Layer-4 issues

Under TCP protocol, CLB uses SYN packets for check. Under UDP protocol, CLB uses `Ping` command for check.
When a real server port is marked as "unhealthy" on the page, troubleshoot via the following steps:

- Check whether the real server is configured with security groups that affect the service. For more information on access control over a real server to ensure normal running of services, please see [Real Server Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/6157).
- Run the `netstat` command to check whether there is a process listening on the real server port. If no such process is found, restart the service.

### Troubleshooting Layer-7 issues
For layer-7 (HTTP/HTTPS protocols) services, when a listener has an exception during health check, troubleshoot via the following steps:
1. Because layer-7 health check service of CLB communicates with the real server via the private network, you need to log in to the server to check whether the application server port is listened on normally at the private network address. If not, move the listener on the application server port to the private network to ensure normal communication between CLB and the real server.
Suppose both the CLB's frontend port and the real server's backend port are 80, and the CVM instance's private IP is `1.1.1.10`:
For a server on Windows, use the following command:
```
netstat -ano | findstr :80
```
For a server on Linux, use the following command:
```
netstat -anp | grep :80
```
If you can see the listening on `1.1.1.10:80` or `0.0.0.0:80`, the configuration is normal.
2. Make sure that the backend port configured in CLB listener has been enabled on the real server.
For layer-4 CLB, it is considered normal as long as backend port `telnet` responds. You can use `telnet 1.1.1.10 80` for testing. For layer-7 CLB, it is considered normal if an HTTP status code such as 200 is returned. Check as follows:
 - On Windows, you can directly enter the private IP in the browser on a CVM instance to test whether it is normal. This example uses `http://1.1.1.10`.
 - On Linux, you can run the `curl-I` command to check whether the status is `HTTP/1.1 200 OK`. This example uses the `curl -I 1.1.1.10` command.
3. Check whether the CVM has a firewall or other security software, which is likely to block the local IP address of the CLB. This causes CLB to be unable to communicate with the real server.
Check whether the private network firewall of the server allows port 80 to pass. You can temporarily disable the firewall for the test.
 - For Windows, run the `firewall.cpl' command to disable the firewall.
 - For Linux, run the `/etc/init.d/iptables stop` command to disable the firewall.
4. Check whether the health check parameters of CLB are configured correctly. We recommend you use the default health check parameter values in this document.
5. For the test file specified for health check, we recommend you use a simple page in HTML format, which is only used to check the returned results. Dynamic programming languages such as PHP are not recommended.
6. Check whether the real server has high load that leads to slow response.
7. Check the HTTP request method. If HEAD is used, the real server must support HEAD. If GET is used, the real server must support GET.

### Notes on high-frequency health checks
Health check packets are sent too frequently. Each health check packet is sent every 5 seconds as configured in the console, but the real server finds that one or multiple health check requests are received within 1 second. The reasons are as follows:
- If health check is too frequent, it may be caused by CLB's health check implementation mechanism. Suppose that 1 million requests from clients are distributed to four CLB real servers before being sent to the CVM instance. Each CLB real server conducts health check separately. If the CLB instances are configured to send a health check request every 5 seconds, each CLB real server will send a health check request every 5 seconds. The CVM instance will therefore receive multiple health check requests. (For example, if the cluster to which a CLB instance belongs has 8 physical servers, and each server sends a request every 5 seconds, then the CVM instance may receive 8 health check requests in 5 seconds.)
- The advantages of this implementation scheme are high efficiency, accurate check, and avoidance of mistaken removal. For example, if one of eight physical servers in CLB instance cluster fails, the other seven servers can still forward traffic normally. 

Therefore, if your real server is checked too frequently, you can configure the check interval to be much longer (for example, 15 seconds).
