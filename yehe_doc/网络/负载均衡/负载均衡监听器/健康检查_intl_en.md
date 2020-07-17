A CLB instance can periodically send ping commands to real servers, attempt to connect with or send requests to them to check their running status. These are called "health check". The CLB instance uses health checks to determine the availability of real servers and prevent unhealthy real servers from affecting frontend services, thereby improving overall service availability.
- If a real server is confirmed as unhealthy, the CLB instance will automatically distribute new requests to other normal servers instead of forwarding requests to it. When an unhealthy server recovers to normal status, the CLB instance will automatically restore its service and distribute new requests to it again.
- After health check is enabled, the CLB instance will always perform health check, regardless of the weights of real servers (including 0).
- An auto scaling group will periodically use a similar method to check the running status of each instance in the group. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).

## Health Check Configuration for Layer-4 Forwarding
The health check works for the layer-4 forwarding as follows: the CLB instance initiates an access request to the server port specified in the configuration. If the port can be accessed normally, the real server is considered as healthy. Otherwise, it is unhealthy.
For TCP business, SYN packets are used for health check. For UDP business, the ping command is used.

| Health Check Configuration    | Description                    | Default Value                               |
| ------- | ------------------------ | ---------------------------------------- |
| Response timeout period | <li>Maximum response timeout period for health check.</li><li>If a real server fails to respond properly within the timeout period, it is considered unhealthy.</li><li>Value range: 2-60 seconds.</li> | 2s |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300 seconds. </li> | 5s |
| Unhealthy threshold | <li>If the health check returns `failure` for consecutive n times (n is user-defined), the real server is unhealthy, and displays the **unhealthy** status in the console.</li><li>Value range: 2-10 times.</li> | 3 times |
| Healthy threshold | <li>If the health check returns `success` for consecutive n times (n is user-defined), the real server is healthy, and display the **healthy** status in the console.</li><li>Value range: 2-10 times.</li> | 3 times |

## Health Check Configuration for Layer-7 Forwarding

The health check works for the layer-7 forwarding as follows: a CLB instance sends an HTTP request to the real server for health check, and determines the healthy status of the server based on the HTTP response. For example, assume HTTP responses include `http_1xx`, `http_2xx`, `http_3xx`, `http_4xx` and `http_5xx`, you can define `http_1xx` and `http_2xx` as healthy status as needed, and configure `http_3xx` to `http_5xx` as unhealthy status.

| Health Check Configuration    | Description                    | Default Value                                |
| ------- | ------------------------ | ---------------------------------------- |
| Check domain name | Health check domain name:<ul style="margin-bottom:0px;"><li>It contains 1-80 characters.</li><li>It is the forwarded domain name by default.</li><li>Regular expression is not supported. If your forwarded domain name is a wildcard domain name, you should specify a fixed one (non-regex) as the health check domain name.</li><li>Supported character sets: `a-z` `0-9` `.` `-`.</li></ul> | Forwarded domain name |
| Check path | Health check path: <ul style="margin-bottom:0px;"><li>It contains 1-200 characters </li><li>It defaults to and must begin with `/`.</li><li>Regular expression is not supported. We recommend you specify a fixed URL path (static page) for health checks.</li><li>Supported character sets: `a-z` `A-Z` `0-9` `.` `-` `_` `/` `=` `?`.</li></ul>  | `/` |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5-300 seconds. </li> | 5s |
| Unhealthy threshold | <li>If the health check returns `failure` for consecutive n times (n is user-defined), the real server is unhealthy, and displays the **unhealthy** status in the console.</li><li>Value range: 2-10 times.</li> | 3 times |
| Healthy threshold | <li>If the health check returns `success` for consecutive n times (n is user-defined), the real server is healthy, and display the **healthy** status in the console.</li><li>Value range: 2-10 times.</li> | 3 times |
| HTTP request method | HTTP request method for health checks. Valid values: GET or HEAD.<ul style="margin-bottom:0px;"><li>If HEAD is used, the server will only return the HTTP header, which can reduce backend overheads and improve request efficiency. The real server must support HEAD.</li><li>If GET is used, the real server must support GET.</li> | GET |
| HTTP status code check | If the status code returned is included in the status code specified, the real server is considered as alive (healthy). Valid values: http_1xx, http_2xx, http_3xx, http_4xx, http_5xx. | http_1xx, http_2xx, http_3xx, http_4xx |

## Health Check Status
According to the health check detection conditions, a real server may have one of the following four health check status:

| Status | Description | Whether to Forward Traffic|
| ------- | ----------- | ---------------- |
| Detecting | The status of a new real server during the period of check interval × health threshold. For example, assume the check interval is 2 seconds and the health threshold is 3 times, the new real server remains in this status within 6 seconds. | No. |
| Healthy | The real server is normal. | Yes. |
| Unhealthy | The real server has an exception. |  <li>No.</li><li> Under a layer-4 listener or layer-7 URL rule, if a CLB instance detects that all real servers are unhealthy, it will activate the all-alive logic and forwards requests to all real servers.</li>|
| Disabled | Health check has been disabled. | Yes |

## How to Troubleshoot Health Check Issues
### Troubleshooting layer-4 issues

Under the TCP protocol, CLB uses SYN packets for check. Under the UDP protocol, CLB uses `Ping` command for check.
When a real server port is marked as "unhealthy" on the page, troubleshoot it as follows:

- Check whether the real server is configured with security groups that affect the service. For more information on access control over a real server to ensure normal running of services, please see [Real Server Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/6157).
- Run the `netstat` command to check whether there is a process listening on the real server port. If no such process is found, restart the service.

### Troubleshooting layer-7 issues
For layer-7 (HTTP/HTTPS protocols) services, when a listener has an exception during health check, troubleshoot it as follows:
1. For the purpose of health check, the layer-7 CLB instance communicates with the real server via the private network. You need to log in to the server to check whether the application server port is listened on normally at the private network address. If not, move the listening on the application server port to the private network, thereby ensuring normal communication between CLB instances and the real server.
Suppose both the CLB’s frontend port and the real server’s backend port are 80, and the CVM instance's private IP is `1.1.1.10`:
For a Windows server, use the following command:
```
netstat -ano | findstr :80
```
For a Linux server, use the following command:
```
netstat -anp | grep :80
```
If you can see the listening on `1.1.1.10:80` or `0.0.0.0:80`, the configuration is correct.
2. Make sure that the backend port configured in CLB listener has been enabled on the real server.
For a layer-4 CLB instance, use `telnet 1.1.1.10 80`. It is considered normal if the backend port responds to `telnet`. For a layer-7 CLB instance, it is considered normal if a healthy HTTP status code such as 200 is returned. Check as follows:
 - On Windows, you can directly enter the private IP in the browser on a CVM instance to test whether it is normal. This example uses `http://1.1.1.10`.
 - On Linux, you can run the `curl-I` command to check whether the status is `HTTP/1.1 200 OK`. This example uses the `curl -I 1.1.1.10` command.
3. Check whether the CVM has a firewall or other security software, which is likely to block the local IP address of the CLB instance. As a result, the CLB instance is unable to communicate with the real server.
Check whether the private network firewall of the server allows port 80 to pass. You can temporarily disable the firewall for the test.
 - On Windows, run the `firewall.cpl` command to disable the firewall.
 - On Linux, run the `/etc/init.d/iptables stop` command to disable the firewall.
4. Check whether the health check parameters of the CLB instance are configured correctly. We recommend you use the default health check parameter values in this document.
5. For the test file specified for health check, we recommend you use a simple page in HTML format, which is only used to check the returned results. Dynamic programming languages such as PHP are not recommended.
6. Check whether the real server has a high load that leads to slow response.
7. Check the HTTP request method. If HEAD is used, the real server must support HEAD. If GET is used, the real server must support GET.
8. If both the quick repossession (tcp_tw_recycle) and timestamp (tcp_timestamps) of the TCP protocol are enabled, the health check may be abnormal. We recommend disabling `tcp_tw_recycle`. For more information, see [Cause Analysis](https://intl.cloud.tencent.com/document/product/214/10328).

### Notes on high-frequency health checks
Health check packets are sent too frequently. The health check packet is sent every 5 seconds as configured in the console, but the real server receives one or multiple health check requests within 1 second. The reasons are as follows:
- The frequent health checks may be caused by the health check implementation mechanism on the CLB real server. Suppose that 1 million requests from the client are distributed to four CLB real servers before being sent to the CVM instance. Each CLB real server conducts health check separately. If the CLB instances are configured to send a health check request every 5 seconds, each CLB real server will send a health check request every 5 seconds. The CVM instance will therefore receive multiple health check requests. (For example, if the cluster in which a CLB instance resides has 8 real servers, and each server sends a request every 5 seconds, then the CVM instance may receive 8 health check requests in 5 seconds.)
- This implementation scheme features high efficiency, accurate check, and error-free removal. For example, if one of the eight real servers in CLB instance cluster fails, the other seven servers can still forward traffic normally. 

Therefore, if your real server is checked too frequently, you can configure a longer check interval (for example, 15 seconds).
