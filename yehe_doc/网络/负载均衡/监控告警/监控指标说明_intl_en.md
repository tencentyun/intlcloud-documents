Cloud Monitor collects raw data from the running CLB instances and displays the data entries in intuitive graphs. Statistics will be kept for one month by default. You can observe the operations of instances in the month to stay informed of the status of application services.

You can go to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) to view CLB monitoring data. Click **Cloud Product Monitoring** >[**Cloud Load Balancer**](https://console.cloud.tencent.com/monitor/clb) and then click the CLB instance ID to enter the monitoring details page. You can view monitoring data of the CLB instance and expand it to view the listener and real server monitoring information.

## CLB Instance Level
| Metric | Unit | Description |
|----|------|----|
| Inbound bandwidth | Mbps | Bandwidth used by the client to access CLB over the public network within a reference period. |
| Outbound bandwidth | Mbps | Bandwidth used by CLB to access the public network within a reference period. |
| Number of inbound packets | Packets/s | Number of request data packets received by CLB per second within a reference period. |
| Number of outbound packets | Packets/s | Number of data packets sent by CLB per second within a reference period. |

## Layer-4 Listener (TCP/UDP) Level
Layer-4 listeners allow you to view the monitoring metrics at three levels:
- Listener level
- Real server level
- Real server port level

| Metric | Unit | Description |
|----|------|----|
| Number of connections | - | Number of connections on the listener within a reference period. |
| Number of new connections | - | Number of newly established connections on the listener within a reference period. |
| Inbound bandwidth | Mbps | Bandwidth used by the client to access CLB over the public network within a reference period. |
| Outbound bandwidth | Mbps | Bandwidth used by CLB to access the public network within a reference period. |
| Number of inbound packets | Packets/s | Number of request data packets received by CLB per second within a reference period. |
| Number of outbound packets | Packets/s | Number of data packets sent by CLB per second within a reference period. |

## Layer-7 Listener (HTTP/HTTPS) Level
Layer-7 listeners allow you to view the monitoring metrics at five levels:
- Listener level
- Domain name level
- URL forwarding path level
- Real server level
- Real server port level

| Metric | Unit | Description |
|----|------|----|
| Number of connections | - | Number of connections on the listener within a reference period. |
| Number of new connections | - | Number of newly established connections on the listener within a reference period. |
| Inbound bandwidth | Mbps | Bandwidth used by the client to access CLB over the public network within a reference period. |
| Outbound bandwidth | Mbps | Bandwidth used by CLB to access the public network within a reference period. |
| Number of inbound packets | Packets/s | Number of request data packets received by CLB per second within a reference period. |
| Number of outbound packets | Packets/s | Number of data packets sent by CLB per second within a reference period. |
| Average response time | ms | Average response time of CLB within a reference period. |
| Maximum response time | ms | Maximum response time of CLB within a reference period. |
| Number of response timeouts | - | Number of CLB response timeouts within a reference period. |
| Requests per second | - | Number of CLB requests per second within a reference period, i.e., QPS. |
| 2xx status code | - | Number of 2xx status codes returned by the real server within a reference period. |
| 3xx status code | - | Number of 3xx status codes returned by the real server within a reference period. |
| 4xx status code | - | Number of 4xx status codes returned by the real server within a reference period. |
| 5xx status code | - | Number of 5xx status codes returned by the real server within a reference period. |
| 404 status code | - | Number of 404 status codes returned by the real server within a reference period. |
| 502 status code | - | Number of 502 status codes returned by the real server within a reference period. |
| 3xx status code returned by CLB | - | Number of 3xx status codes returned by CLB within a reference period (sum of CLB and real server return codes). |
| 4xx status code returned by CLB | - | Number of 4xx status codes returned by CLB within a reference period (sum of CLB and real server return codes). |
| 5xx status code returned by CLB | - | Number of 5xx status codes returned by CLB within a reference period (sum of CLB and real server return codes). |
| 404 status code returned by CLB | - | Number of 404 status codes returned by CLB within a reference period (sum of CLB and real server return codes). |
| 502 status code returned by CLB | - | Number of 502 status codes returned by CLB within a reference period (sum of CLB and real server return codes). |

>!If you want to view the monitoring data of a CVM instance under a listener, please log in to the [CLB Console](https://console.cloud.tencent.com/clb), click the monitoring icon near the CLB instance ID, and then browse the performance data of each instance in the floating window.

