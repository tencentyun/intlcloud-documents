## Use Cases
Anti-DDoS Advanced health checks identify the running status of backend servers, where abnormal servers will be isolated to reduce the impact on overall business availability.
- **Layer-4 health check**
 The Anti-DDoS Advanced layer-4 health check mechanism is as follows: The Anti-DDoS cluster nodes initiate an access request to the server port specified and determine whether the port access is normal. If it is considered normal, the backend server is running properly, otherwise, the backend server is not functioning correctly.
 Under TCP protocol, the mechanism determines if the port is connected, while under UDP protocol, it determines whether the port is reachable with the `ping` command.
- **Layer-7 health check**
The Anti-DDoS Advanced layer-7 health check mechanism is as follows: The Anti-DDoS cluster nodes initiate an HTTP request to the backend server specified and determine whether the backend server works properly according to HTTP response status codes.
HTTP response status codes can be user-defined. Assume that `http_1xx`, `http_2xx`, `http_3xx`, `http_4xx` and `http_5xx` are returned. You can select `http_1xx` and `http_2xx` to indicate that the service is normal, while the unselected codes represent that the service is not working properly.

>!If only one real server IP is configured in a single forwarding rule, health checks will not be enabled. This feature is used when multiple real server IPs are configured.

## Directions
### Layer-4 health check configuration
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4), select **Anti-DDoS Advanced (New)** > **Application Accessing** on the left sidebar, and then open the **Access via ports** tab.
2. Select an Anti-DDoS Advanced instance and rules before you click **Edit**.
![](https://main.qcloudimg.com/raw/1ff1f0502792f1f75719d55789b34c36.png)
3. On the page that pops up, click **Show advanced options**, set configuration items, and then click **OK**.
>?
> - By default, layer-4 health check is enabled. We recommend you use the default values when you configure this feature.
> - Under TCP protocol, the layer-4 health check determines if the port is connected, while under UDP protocol, it determines whether the port is reachable with the `ping` command.

![](https://main.qcloudimg.com/raw/4737846a7a9d3f7f4ae41c1719618a57.png)



### Layer-7 health check configuration
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4), select **Anti-DDoS Advanced (New)** > **Application Accessing** on the left sidebar, and then open the **Access via ports** tab.
2. Select an Anti-DDoS Advanced instance and rules before you click **Configuration**.
![](https://main.qcloudimg.com/raw/10caff27108f8dc76acc5e8b2534632e.png)
3. On the page that pops up, click **Show advanced options**, set configuration items, and then click **OK**.
>?By default, layer-7 health check is disabled.

![](https://main.qcloudimg.com/raw/1159b957659ea780671f572f08c6cd75.png)

## Configuration Items
**Layer-4 health check**

| Item | Description |
|---------|---------|
| Response timeout | Maximum timeout for each health check response. If the backend server does not respond correctly within the specified period, then the health check fails. |
| Check interval | The interval at which a health check is performed. |
| Unhealthy threshold | If the health check fails n times (n is the entered number) in a row, the healthy backend server will become unhealthy, and the status displayed in the console will be **Abnormal**. |
| Healthy threshold | If the health check succeeds n times (n is the entered number) in a row, the unhealthy backend server will become healthy, but the status will not be displayed in the console. |

 **Layer-7 health check**

| Item | Description |
|---------|---------|
| Check interval | The interval at which a health check is performed. Default: 15 seconds. |
|Unhealthy threshold|If the health check fails n times (n is the entered number) in a row, the healthy backend server will become unhealthy, and the status displayed in the console will be **Abnormal**.|
|Healthy threshold|If the health check succeeds n times (n is the entered number) in a row, the unhealthy backend server will become healthy, but the status will not be displayed in the console.|
|HTTP request method and URL|By default, the HEAD method is used and the backend server returns the message header only in the response. If the GET method is used, the complete message will be returned. The backend server must support both HEAD and GET methods.</br> <li>If the health check page is not the default home page of the application server, you need to specify a path.</li><li>If the host field is specified by the HTTP HEAD request, you need to specify a path, i.e., the URI of the health check page.</li>|
|HTTP status code detection|It determines whether the HTTP status code is healthy. When the default configuration is used or no selection is made, `http_1xx`, `http_2xx`, `http_3xx` and `http_4xx` are returned. If non-default ones are returned, the HTTP status code is considered unhealthy, and you can modify the configuration.|

