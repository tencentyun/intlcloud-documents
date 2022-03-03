Cloud Monitor collects raw data from the running CLB instances and displays the data entries in intuitive graphs. Statistics will be kept for one month by default. You can observe the operations of instances in the month to stay informed of the status of application services.

You can go to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) to view CLB monitoring data. Click **Cloud Product Monitoring** > [**Cloud Load Balancer**](https://console.cloud.tencent.com/monitor/clb) and then click the CLB instance ID to enter the monitoring details page. You can view monitoring data of the CLB instance, and expand it to view the listener and real server monitoring information.

## CLB Instance Level
>?The inbound bandwidth utilization and outbound bandwidth utilization are applicable to bill-by-IP accounts. To check your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).

| Metric | Unit | Description |
|----|------|----|
| Inbound bandwidth | Mbps | Bandwidth used by the client to access CLB over the public network within a sample period. |
| Outbound bandwidth | Mbps | Bandwidth used by CLB to access the public network within a sample period. |
| Inbound packets | Packets/s | Number of request data packets received by CLB per second within a sample period. |
| Outbound packets | Packets/s | Number of data packets sent by CLB per second within a sample period. |
|Outbound traffic | MB  | Traffic used by CLB to access the public network within a sample period.|
|Dropped connections | Connections/s  | Number of connections dropped by CLB per second within a sample period.|
|Dropped inbound bandwidth | bps  | Inbound bandwidth dropped by CLB per second within a sample period.|
|Dropped outbound bandwidth | bps  | Outbound bandwidth dropped by CLB per second within a sample period.|
|Dropped inbound data packets | Packets/s  |Number of inbound data packets dropped by CLB per second within a sample period. |
|Dropped outbound data packets | Packets/s  |Number of outbound data packets dropped by CLB per second within a sample period. |
|Inbound bandwidth utilization | %  | Inbound bandwidth utilization of CLB within a sample period.|
|Outbound bandwidth utilization | %  | Outbound bandwidth utilization of CLB within a sample period.|
|Client-to-CLB connections | N/A  | Number of connections between the client and CLB instance initiated by the listener within a sample period.|
|Client-to-CLB new connections | N/A  | Number of new connections between the client and CLB instance initiated by the listener within a sample period.|
|SNAT concurrent connections | N/A  | Number of concurrent connections initiated by the CLB SNAT IP per minute within a sample period.|
|SNAT port utilization | %  | Percentage of the CLB SNAT port usage within a sample period, which is calculated by SNAT concurrent connections / (Number of SNAT IPs * 55000 * Number of real servers).|
|Failed SNAT connections | N/A  | Number of failed connections between the CLB SNAT IP and real server per minute within a sample period.|




## Layer-4 Listener (TCP/UDP) Level
Layer-4 listeners allow you to view the monitoring metrics at three levels:
- Listener level
- Real server level
- Real server port level

| Metric | Unit | Description |
|----|------|----|
| Inbound bandwidth | Mbps | Bandwidth used by the client to access CLB over the public network within a sample period. |
| Outbound bandwidth | Mbps | Bandwidth used by CLB to access the public network within a sample period. |
| Inbound packets | Packets/s | Number of request data packets received by CLB per second within a sample period. |
| Outbound packets | Packets/s | Number of data packets sent by CLB per second within a sample period. |
|Outbound traffic | MB  | Traffic used by CLB to access the public network within a sample period.|
|CLB-to-real server connections | N/A  | Number of connections between the CLB instance and real server initiated by the listener within a sample period.|
|Client-to-CLB new connections | N/A  | Number of new connections between the CLB instance and real server initiated by the listener within a sample period.|
|Client-to-CLB connections | N/A  | Number of connections between the client and CLB instance initiated by the listener within a sample period.|
|Client-to-CLB new connections | N/A  | Number of new connections between the client and CLB instance initiated by the listener within a sample period.|


## Layer-7 Listener (HTTP/HTTPS) Level
Layer-7 listeners allow you to view the monitoring metrics at five levels:
- Listener level
- Domain name level
- URL forwarding path level
- Real server level
- Real server port level

| Metric | Unit | Description |
|------|---------|----|
| Outbound bandwidth | Mbps | Bandwidth used by CLB to access the public network within a sample period. |
| Inbound bandwidth | Mbps | Bandwidth used by the client to access CLB over the public network within a sample period. |
| Outbound packets | Packets/s | Number of data packets sent by CLB per second within a sample period. |
| Inbound packets | Packets/s | Number of request data packets received by CLB per second within a sample period. |
|Outbound traffic | MB  | Traffic used by CLB to access the public network within a sample period.|
|CLB-to-real server connections | N/A  | Number of connections between the CLB instance and real server initiated by the listener within a sample period.|
|Client-to-CLB connections | N/A  | Number of connections between the client and CLB instance initiated by the listener within a sample period.|
|Client-to-CLB new connections | N/A  | Number of new connections between the client and CLB instance initiated by the listener within a sample period.|
| Average request duration | ms | The average request duration of CLB within a sample period. The duration starts from the point when the CLB instance receives the first byte from the client and ends when the CLB instance sends the last byte to the client. |
| Maximum request duration | ms | The maximum request duration of CLB within a sample period. The duration starts from the point when the CLB instance receives the first byte from the client and ends when the CLB instance sends the last byte to the client. |
| Average response duration | ms | The average response duration of the real server within a sample period. The duration refers to the whole duration of the request, starting from the point when the CLB instance connects to the real server and ends when the real server receives the last byte of the response. |
| Maximum response duration | ms | The maximum response duration of the real server within a sample period. The duration refers to the whole duration of the request, starting from the point when the CLB instance connects to the real server and ends when the real server receives the last byte of the response. |
| Timed-out requests | Requests/minute |  Number of requests timed out within a sample period.  |
| Successful requests per minute | Requests/minute |  Number of successful CLB requests per minute within a sample period.|
| Requests per second | - | Number of CLB requests per second within a reference period, i.e., QPS. |
| 3xx status codes returned by CLB | - | Number of 3xx status codes returned by CLB within a reference period (sum of CLB and real server return codes).|
| 4xx status codes returned by CLB | - | Number of 4xx status codes returned by CLB within a reference period (sum of CLB and real server return codes).|
| 5xx status codes returned by CLB | - | Number of 5xx status codes returned by CLB within a reference period (sum of CLB and real server return codes).|
| 404 status codes returned by CLB | - | Number of 404 status codes returned by CLB within a reference period (sum of CLB and real server return codes).|
| 502 status codes returned by CLB | - | Number of 502 status codes returned by CLB within a reference period (sum of CLB and real server return codes).|
| 2xx status code | – | Number of 2xx status codes returned by the real server within a sample period. |
| 3xx status code | – | Number of 3xx status codes returned by the real server within a sample period. |
| 4xx status code | – | Number of 4xx status codes returned by the real server within a sample period. |
| 5xx status code | – | Number of 5xx status codes returned by the real server within a sample period. |
| 404 status code | – | Number of 404 status codes returned by the real server within a sample period. |
| 502 status code | – | Number of 502 status codes returned by the real server within a sample period. |

>!If you want to view the monitoring data of a CVM instance under a listener, please log in to the [CLB console](https://console.cloud.tencent.com/clb), click the monitoring bar icon near the CLB instance ID, and then browse the performance data of each instance in the floating window.



## Relevant Documentation
[Public Network CLB](https://intl.cloud.tencent.com/document/product/248/10997)
