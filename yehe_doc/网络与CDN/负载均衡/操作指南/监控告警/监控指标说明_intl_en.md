Cloud Monitor collects raw data from the running CLB instances and displays the data entries in intuitive graphs. Statistics will be kept for one month by default. You can observe the operations of instances in the month to stay informed of the status of application services.

You can go to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) to view CLB monitoring data. Click **Cloud Product Monitoring** > [**Cloud Load Balancer**](https://console.cloud.tencent.com/monitor/clb) and then click the CLB instance ID to enter the monitoring details page. You can view monitoring data of the CLB instance, and expand it to view the listener and real server monitoring information.
>?The metrics in this document are all basic metrics. If you need more monitoring capabilities, you can activate paid advanced metrics.
>- Advanced CLB metrics include max connections utilization (ConcurConnVipRatio) and new connections utilization (NewConnVipRatio) at the instance level.
>- Currently, only the ConcurConnVipRatio and NewConnVipRatio metrics of LCU-supported CLB instances report data once enabled, while shared CLB instances don't report data for the time being.
>

## CLB Instance Level

| Parameter | Metric Name | Description | Unit | Statistical Period (Sec) |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------- |
| ClientConnum        | Client-to-CLB active connections   | Number of active connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientInactiveConn  | Client-to-CLB inactive connections | Number of inactive connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientConcurConn    | Client-to-CLB concurrent connections   | Number of concurrent connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientNewConn       | Client-to-CLB new connections   | Number of new connections initiated from the client to the CLB instance in the statistical period     | -   | 10s, 60s, 300s       |
| ClientInpkg | Inbound packets from the client to the LB | The number of data packets per second sent from the client to the load balancer within the statistical granularity. | Count/sec | 10, 60, 300 |
| ClientOutpkg | Outbound packets from the client to the LB | The number of data packets per second sent from the load balancer to the client within the statistical granularity. | Count/sec | 10, 60, 300 |
| ClientAccIntraffic | Inbound traffic from the client to the LB | The traffic flows from the client to the load balancer within the statistical granularity. | MB | 10, 60, 300 |
| ClientAccOuttraffic | Outbound traffic from the client to the LB | The traffic flows from the load balancer to the client within the statistical granularity. | MB | 10, 60, 300 |
| ClientOuttraffic | Outbound bandwidth from the client to the LB | The bandwidth used by the load balancer to access the client within the statistical granularity. | Mbps | 10, 60, 300 |
| ClientIntraffic     | Client-CLB inbound bandwidth       | Inbound bandwidth used by the traffic from the client to the CLB instance in the statistical period.               | Mbps    | 10, 60, 300       |
| OutTraffic | Outbound bandwidth from the LB to the RS | The bandwidth used by the RS to access the load balancer within the statistical granularity. | Mbps | 60, 300 |
| InTraffic | Inbound bandwidth from the LB to the RS | The bandwidth used by the load balancer to access the RS within the statistical granularity. | Mbps | 60, 300 |
| AccOuttraffic | Outbound traffic from the LB to the RS | The traffic flows from the load balancer to the RS within the statistical granularity.<br/>This metric is only supported by the public network CLB instances. | MB | 10, 60, 300, 3600 |
| DropTotalConns | Dropped connections | Number of connections dropped by the LB or listener within the statistical granularity.<br/>This metric is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). | Count | 10, 60, 300 |
| InDropBits | Dropped inbound bandwidth | The bandwidth dropped by the client when accessing the load balancer through the public network within the statistical granularity.<br/>This metric is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). | Byte | 10, 60, 300 |
| OutDropBits | Dropped outbound bandwidth | The bandwidth dropped by the load balancer when accessing the public network within the statistical granularity.<br/>This metric is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). | Byte | 10, 60, 300 |
| InDropPkts | Dropped inbound packets | The packets dropped by the client when accessing the load balancer through the public network within the statistical granularity.<br/>This metric is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). | Count/sec | 10, 60, 300 |
| OutDropPkts | Dropped outbound packets | The packets dropped by the load balancer when accessing the public network within the statistical granularity.<br/>This metric is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). | Count/sec | 10, 60, 300 |
| DropQps | Dropped QPS | The requests dropped by the load balancer or listener within the statistical granularity.<br/>This metric is dedicated to the layer-7 listener. It is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). | Count | 60, 300 |
| IntrafficVipRatio | Utilization of inbound bandwidth | The utilization of bandwidth used by the client to access the load balancer through the public network within the statistical granularity. <br/>This metric is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). This metric is currently in beta. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20CLB&level3_id=1071&queue=96&scene_code=34639&step=2). | % | 10, 60, 300 |
| OuttrafficVipRatio | Utilization of outbound bandwidth | The utilization of bandwidth used by the load balancer to access the public network within the statistical granularity. <br/>This metric is only supported by a bill-by-IP account and not supported by a bill-by-CVM account. For details on account types, see [Checking Account Type](https://www.tencentcloud.com/document/product/684/15246). This metric is currently in beta. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20CLB&level3_id=1071&queue=96&scene_code=34639&step=2). | % | 10, 60, 300 |
| ReqAvg | Average request time | The average request time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| ReqMax | Maximum request time | The maximum request time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspAvg | Average response time | The average response time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspMax | Maximum response time | The maximum response time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspTimeout | Number of response timeouts | The number of CLB response timeouts in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| SuccReq | Successful requests per minute | The number of successful CLB requests per minute in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| TotalReq | Requests per second | The number of CLB requests per second in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | - | 60s, 300s |
| ClbHttp3xx | 3xx status codes returned by CLB | The number of 3xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp4xx | 4xx status codes returned by CLB | The number of 4xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp5xx | 5xx status codes returned by CLB | The number of 5xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp404 | 404 status codes returned by CLB | The number of 404 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp499 | 499 status codes returned by CLB | The number of 499 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp502 | 502 status codes returned by CLB | The number of 502 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp503 | 503 status codes returned by CLB | The number of 503 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp504 | 504 status codes returned by CLB | The number of 504 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http2xx | 2xx status codes | The number of 2xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http3xx | 3xx status codes | The number of 3xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http4xx | 4xx status codes | The number of 4xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http5xx | 5xx status codes | The number of 5xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http404 | 404 status codes | The number of 404 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http499 | 499 status codes | The number of 499 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http502 | 502 status codes | The number of 502 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http503 | 503 status codes | The number of 503 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http504 | 504 status codes | The number of 504 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| OverloadCurConn | Concurrent SNAT connections | The concurrent connections of the CLB instance's SNAT IP per minute in the statistical period. <br/>This metric is currently in beta. To try it out, [submit a ticket](https://console.tencentcloud.com/workorder/category). | Count/min | 60s |
| ConnRatio           | SNAT port utilization            | Utilization of ports of the CLB instance's SNAT IPs in the statistical period.<br/>Port utilization = number of concurrent SNAT connections / (number of SNAT IPs * 55,000 * number of real servers). <br/>This metric is currently in beta. To try it out, [submit a ticket](https://console.tencentcloud.com/workorder/category). | %       | 60s           |
| SnatFail | Failed SNAT connections | The number of failed connections between the CLB instance's SNAT IP and the RS per minute in the statistical period.<br/>This metric is currently in beta. To try it out, [submit a ticket](https://console.tencentcloud.com/workorder/category). | Count/min | 60s |
| UnhealthRsCount | Number of abnormal health check | The number of load balancer’s abnormal health check within the statistical granularity. | Count | 60, 300 |



## Layer-4 Listener (TCP/UDP) Level
Layer-4 listeners allow you to view the monitoring metrics at three levels:
- Listener level
- Real server level
- Real server port level

| Parameter | Metric Name | Description | Unit | Statistical Period (Sec) |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------- |
| ClientConnum        | Client-to-CLB active connections   | Number of active connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientNewConn       | Client-to-CLB new connections   | Number of new connections initiated from the client to the CLB instance in the statistical period     | -   | 10s, 60s, 300s       |
| ClientInpkg | Inbound packets from the client to the LB | The number of data packets per second sent from the client to the load balancer within the statistical granularity. | Count/sec | 10, 60, 300 |
| ClientOutpkg | Outbound packets from the client to the LB | The number of data packets per second sent from the load balancer to the client within the statistical granularity. | Count/sec | 10, 60, 300 |
| ClientAccIntraffic | Inbound traffic from the client to the LB | The traffic flows from the client to the load balancer within the statistical granularity. | MB | 10, 60, 300 |
| ClientAccOuttraffic | Outbound traffic from the client to the LB | The traffic flows from the load balancer to the client within the statistical granularity. | MB | 10, 60, 300 |
| ClientOuttraffic | Outbound bandwidth from the client to the LB | The bandwidth used by the load balancer to access the client within the statistical granularity. | Mbps | 10, 60, 300 |
| ClientIntraffic | Inbound bandwidth from the client to the LB | The bandwidth used by the client to access the load balancer within the statistical granularity. | Mbps | 10, 60, 300 |
| OutTraffic | Outbound bandwidth from the LB to the RS | The bandwidth used by the RS to access the load balancer within the statistical granularity. | Mbps | 60, 300 |
| InTraffic | Inbound bandwidth from the LB to the RS | The bandwidth used by the load balancer to access the RS within the statistical granularity. | Mbps | 60, 300 |
| OutPkg | Outbound packets from the LB to the RS | The number of packets per second sent from the RS to the load balancer within the statistical granularity. | Count/sec | 60, 300 |
| InPkg | Inbound packets from the LB to the RS | The number of packets per second sent from the load balancer to the RS within the statistical granularity. | Count/sec | 60, 300 |
| AccOuttraffic | Outbound traffic from the LB to the RS | The traffic flows from the load balancer to the RS within the statistical granularity.<br/>This metric is only supported by the public network CLB instances. | MB | 10, 60, 300, 3600 |
| ConNum | CLB-to-RS connections | Number of connections initiated from the CLB instance to the RS in the statistical period | - | 60s, 300s |
| NewConn | CLB-to-RS new connections | Number of new connections initiated from the CLB instance to the RS in the statistical period | Count/min | 60s, 300s |
| UnhealthRsCount | Number of abnormal health check | The number of load balancer’s abnormal health check within the statistical granularity. | Count | 60, 300 |



## Layer-7 Listener (HTTP/HTTPS) Level
Layer-7 listeners allow you to view the monitoring metrics at three levels:
- Listener level
- Real server level
- Real server port level

| Parameter | Metric Name | Description | Unit | Statistical Period (Sec) |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------- |
| ClientConnum        | Client-to-CLB active connections   | Number of active connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientNewConn       | Client-to-CLB new connections   | Number of new connections initiated from the client to the CLB instance in the statistical period     | -   | 10s, 60s, 300s       |
| ClientInpkg | Inbound packets from the client to the LB | The number of data packets per second sent from the client to the load balancer within the statistical granularity. | Count/sec | 10, 60, 300 |
| ClientOutpkg | Outbound packets from the client to the LB | The number of data packets per second sent from the load balancer to the client within the statistical granularity. | Count/sec | 10, 60, 300 |
| ClientAccIntraffic | Inbound traffic from the client to the LB | The traffic flows from the client to the load balancer within the statistical granularity. | MB | 10, 60, 300 |
| ClientAccOuttraffic | Outbound traffic from the client to the LB | The traffic flows from the load balancer to the client within the statistical granularity. | MB | 10, 60, 300 |
| ClientOuttraffic | Outbound bandwidth from the client to the LB | The bandwidth used by the load balancer to access the client within the statistical granularity. | Mbps | 10, 60, 300 |
| ClientIntraffic | Inbound bandwidth from the client to the LB | The bandwidth used by the client to access the load balancer within the statistical granularity. | Mbps | 10, 60, 300 |
| OutTraffic | Outbound bandwidth from the LB to the RS | The bandwidth used by the RS to access the load balancer within the statistical granularity. | Mbps | 60, 300 |
| InTraffic | Inbound bandwidth from the LB to the RS | The bandwidth used by the load balancer to access the RS within the statistical granularity. | Mbps | 60, 300 |
| OutPkg | Outbound packets from the LB to the RS | The number of packets per second sent from the RS to the load balancer within the statistical granularity. | Count/sec | 60, 300 |
| InPkg | Inbound packets from the LB to the RS | The number of packets per second sent from the load balancer to the RS within the statistical granularity. | Count/sec | 60, 300 |
| AccOuttraffic | Outbound traffic from the LB to the RS | The traffic flows from the load balancer to the RS within the statistical granularity.<br/>This metric is only supported by the public network CLB instances. | MB | 10, 60, 300, 3600 |
| ConNum | CLB-to-RS connections | Number of connections initiated from the CLB instance to the RS in the statistical period | - | 60s, 300s |
| NewConn | CLB-to-RS new connections | Number of new connections initiated from the CLB instance to the RS in the statistical period | Count/min | 60s, 300s |
| ReqAvg | Average request time | The average request time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| ReqMax | Maximum request time | The maximum request time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspAvg | Average response time | The average response time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspMax | Maximum response time | The maximum response time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspTimeout | Number of response timeouts | The number of CLB response timeouts in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| SuccReq | Successful requests per minute | The number of successful CLB requests per minute in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| TotalReq | Requests per second | The number of CLB requests per second in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | - | 60s, 300s |
| ClbHttp3xx | 3xx status codes returned by CLB | The number of 3xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp4xx | 4xx status codes returned by CLB | The number of 4xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp5xx | 5xx status codes returned by CLB | The number of 5xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp404 | 404 status codes returned by CLB | The number of 404 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp499 | 499 status codes returned by CLB | The number of 499 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp502 | 502 status codes returned by CLB | The number of 502 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp503 | 503 status codes returned by CLB | The number of 503 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp504 | 504 status codes returned by CLB | The number of 504 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http2xx | 2xx status codes | The number of 2xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http3xx | 3xx status codes | The number of 3xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http4xx | 4xx status codes | The number of 4xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http5xx | 5xx status codes | The number of 5xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http404 | 404 status codes | The number of 404 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http499 | 499 status codes | The number of 499 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http502 | 502 status codes | The number of 502 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http503 | 503 status codes | The number of 503 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http504 | 504 status codes | The number of 504 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| UnhealthRsCount | Number of abnormal health check | The number of load balancer’s abnormal health check within the statistical granularity. | Count | 60, 300 |


>?If you want to view the monitoring data of a CVM instance under a listener, please log in to the [CLB console](https://console.cloud.tencent.com/clb), click the monitoring bar icon near the CLB instance ID, and then browse the performance data of each instance in the floating window.



## References
[Public Network CLB](https://intl.cloud.tencent.com/document/product/248/10997)
