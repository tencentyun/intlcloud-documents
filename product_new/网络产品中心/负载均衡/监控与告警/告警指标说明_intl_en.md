## Alarm Descriptions
You can create alarms for specified instance metrics so that your CLB instance will send alarm information to target user groups when its running status meets a certain condition. By doing so, you can detect any exceptions in a timely manner and take appropriate actions to ensure system stability and reliability. For more information, see [Alarm Overview](http://intl.cloud.tencent.com/document/product/248/6126).
CLB alarm policies cover the following:
- Public network listener
- Private network listener
- Server port (other)
  - Listener level
  - Server port level
- Server port (private network Classic type)
- Layer-7 protocol monitoring

## Public/Private Network Listeners
Currently, both public network (Application and Classic) and private network CLB (application and classic) support alarming at the listener level. The specific metrics are as follows:

| Metric | Unit | Description |
|----|------|----|
| Inbound bandwidth | bps | Bandwidth used by the client to access CLB over the public network within a reference period. |
| Outbound bandwidth | bps | Bandwidth used by CLB to access the public network within a reference period. |
| Number of inbound packets | packets/s | Number of request data packets received by CLB per second within a reference period. |
| Number of outbound packets | packets/s | Number of data packets sent by CLB per second within a reference period. |

## Server Port (Other)
All CLB instances except for private network Classic CLB instances, which include public network CLB, public network Classic CLB and private network CLB, support alarming at the following two levels:
1. Listener level
You can configure the number of exceptional real server ports of a listener for exception statistics of all bound server ports under the listener, which will trigger alarms based on the configured threshold. As shown below, the number of exceptional ports of all real servers under the selected listener is collected once every minute; if the number is greater than 10 per second for two consecutive reference period, it will trigger an alarm once per day.
>? To activate listener-level alarming, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

 - Configure alarm objects:
![](https://main.qcloudimg.com/raw/f31ddad5ce6f1f4694cb5a18c43feca5.png)
 - Configure trigger conditions:
![](https://main.qcloudimg.com/raw/ae8e92f519132461ee42cc946345f69c.png)
2. Server port level
You can configure exception alarms for a specified port of a backend CVM instance bound to a listener, so that alarms will be sent whenever the port is exceptional.
 - Configure alarm objects:
![](https://main.qcloudimg.com/raw/55cbd5f98729fefc3caa1c800afc9576.png)
 - Configure trigger conditions:
![](https://main.qcloudimg.com/raw/eb302d19c10be1d42b4c37986e523355.png)
>!
>- Real server port exception: it means that CLB finds the port of the real server unavailable; in some cases, network jitter can also trigger port exceptions.
>- Statistics at the listener level include port status of all real servers under the listener, from single alarm convergence to threshold alarming. To avoid the impact of network jitter, we recommend you to use listener-level alarming.

## Server Port (Private Network Classic Type)
You can configure server port exception alarms for private network Classic CLB as instructed in "Server Port (Other) > Server port level".
You can configure exception alarms for a specified port of a backend CVM instance bound to a listener, so that alarms will be sent whenever the port is exceptional.

## Layer-7 Protocol Monitoring
You can configure unique monitoring metric alarm policies for all layer-7 (HTTP/HTTPS) listeners. The specific metrics are as follows:

| Metric | Unit | Description |
|----|------|----|
| Inbound bandwidth | bps | Bandwidth used by the client to access CLB over the public network within a reference period. |
| Outbound bandwidth | bps | Bandwidth used by CLB to access the public network within a reference period. |
| Number of inbound packets | packets/s | Number of request data packets received by CLB per second within a reference period. |
| Number of outbound packets | packets/s | Number of data packets sent by CLB per second within a reference period. |
| Number of new connections | - | Number of new connections established per minute within a reference period. |
| Number of active connections | - | Number of active connections per minute within a reference period. |
| Average response time | ms | Average response time of CLB within a reference period. |
| Maximum response time | ms | Maximum response time of CLB within a reference period. |
| 2xx status code | - | Number of 2xx status codes returned by the real server within a reference period. |
| 3xx status code | - | Number of 3xx status codes returned by the real server within a reference period. |
| 4xx status code | - | Number of 4xx status codes returned by the real server within a reference period. |
| 5xx status code | - | Number of 5xx status codes returned by the real server within a reference period. |
| 404 status code | - | Number of 404 status codes returned by the real server within a reference period. |
| 502 status code | - | Number of 502 status codes returned by the real server within a reference period. |
| 3xx status code returned by CLB | - | Number of 3xx status codes returned by CLB within a reference period. |
| 4xx status code returned by CLB | - | Number of 4xx status codes returned by CLB within a reference period. |
| 5xx status code returned by CLB | - | Number of 5xx status codes returned by CLB within a reference period. |
| 404 status code returned by CLB | - | Number of 404 status codes returned by CLB within a reference period. |
| 502 status code returned by CLB | - | Number of 502 status codes returned by CLB within a reference period. |
