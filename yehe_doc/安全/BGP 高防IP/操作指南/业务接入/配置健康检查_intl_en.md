## Use Cases
Anti-DDoS Advanced can automatically identify the running status of your real servers and isolate exceptional ones through health checks. This reduces the impact of real server exceptions on your overall business availability.
- **Layer-4 business health check**
 The health check mechanism for layer-4 business protection in Anti-DDoS Advanced is as follows: an Anti-DDoS cluster node initiates access requests to the server port specified in the configuration. If access to the port is normal, the real server will be considered healthy; otherwise, it will be considered exceptional.
 Under the TCP protocol, it detects whether the port can be connected. Under the UDP protocol, it uses ping for reachability check.
- **Layer-7 business health check**
The health check mechanism for layer-7 business protection in Anti-DDoS Advanced is as follows: the Anti-DDoS forwarding cluster sends HTTP requests to the real server, and the Anti-DDoS system judges whether the server is normal according to the returned HTTP status codes.
You can customize the status represented by the response code. For example, in a certain scenario, if HTTP returned values include http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx, and you define http_1xx and http_2xx as normal status based on your business needs, then when a response code between http_3xx to http_5xx is returned, you can know that the server is exceptional.

>!When configuring a forwarding rule, if only one real server IP is configured in the rule, the health check feature will not be enabled, as it is suitable for scenarios with multiple real server IPs.

## Directions
### Health check configuration for layer-4 business
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) and click **Business Connection** on the left sidebar. On the business connection page, click **Port Connection** to enter the corresponding management page.
2. On the "Port Connection" tab, select the target Anti-DDoS Advanced instance and the corresponding rule and click **Edit** in its health check column.
![](https://main.qcloudimg.com/raw/1ff1f0502792f1f75719d55789b34c36.png)
3. On the health check editing page, click "Show Advanced Options", set the configuration items, and click **OK**.
>?
> - Heath check is enabled by default. When configuring health check, you are recommended to use the default values.
> - Under the TCP protocol, it detects whether the port can be connected. Under the UDP protocol, it uses ping for reachability check.
> 
![](https://main.qcloudimg.com/raw/4737846a7a9d3f7f4ae41c1719618a57.png)



### Health check configuration for layer-7 business
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) and click **Business Connection** on the left sidebar. On the business connection page, click **Domain Name Connection** to enter the corresponding management page.
2. On the "Domain Name Connection" tab, select the target Anti-DDoS Advanced instance and the corresponding rule and click **Configure** in its health check column.
![](https://main.qcloudimg.com/raw/10caff27108f8dc76acc5e8b2534632e.png)
3. On the health check editing page, click "Show Advanced Options", set the configuration items, and click **OK**.
>?Health check is disabled by default.
>
![](https://main.qcloudimg.com/raw/1159b957659ea780671f572f08c6cd75.png)

## Configuration Item Description
**Layer-4 health check**

| Configuration Item | Description | 
|---------|---------|
| Response timeout period | Maximum response timeout period for health check. If a real server fails to respond properly within the timeout period, the health check will be considered as failed. |
| Check interval | Interval between two health checks. | 
| Unhealthy threshold | When the health check status is "succeeded", if the health check "failed" status is received for n times (n is the entered number) in a row, the real server will be considered as unhealthy, and an exception will be displayed in the console. | 
| Healthy threshold | When the health check status is "failed", if the health check "succeeded" status is received for n times (n is the entered number) in a row, the real server will be considered as healthy, and nothing will be displayed in the console. | 

 **Layer-7 health check**
 
| Configuration Item | Description |
|---------|---------|
| Check interval | Interval between two health checks, which is 15 seconds by default. |
| Unhealthy threshold | When the health check status is "succeeded", if the health check "failed" status is received for n times (n is the entered number) in a row, the real server will be considered as unhealthy, and an exception will be displayed in the console. |
| Healthy threshold | When the health check status is "failed", if the health check "succeeded" status is received for n times (n is the entered number) in a row, the real server will be considered as healthy, and nothing will be displayed in the console. |
| HTTP request method and check path URL | The HEAD method is used by default, and the server will return only the header of the response packet. If the GET method is used, the server will return the complete response packet. The corresponding real server needs to support HEAD and GET. </br> <li>If the page used for health check is not the default homepage of the application server, you need to specify a specific check path. </li><li>If the `host` field parameter is specified in the HTTP HEAD request, you need to specify the check path, i.e., the URI of the page file used for the health check.</li>|
| HTTP status code detection | The HTTP status code used to determine whether the server is normal during health check. By default or if no selection is made, this value is http_1xx, http_2xx, http_3xx, and http_4xx. If the returned HTTP status code is not the default status value, the server will be considered as unhealthy. This value can be modified. |

