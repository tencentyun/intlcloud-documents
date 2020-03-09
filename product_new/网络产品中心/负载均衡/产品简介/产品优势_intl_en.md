CLB performance is evaluated mainly based on the following metrics:
- TPS (connection per second): the number of TCP connections created by a CLB instance per second.
- Maximum number of concurrent connections: the total number of established TCP connections when client sends requests to the server, i.e., the total number of TCP connections created by the server per second.
- QPS (query per second): also known as request per second (RPS). It is the number of GET, POST, and HEAD packets sent by the client to the HTTP service after a connection is established.
- Throughput: the total traffic/bandwidth supported by a CLB instance.

Tencent Cloud provides high-performance CLB services:
- A single CLB cluster can provide over 120 million concurrent connections and respond to hundreds of millions of web access requests.
- A single CLB cluster can handle a peak traffic of 40 GB/s with up to 6 million PPS (packets per second).
- CLB strictly isolates the traffic of each tenant and provides active protection against DDoS attacks. If your service is under DDoS attack, CLB will provide you free defense capability against 2–10 GB of attack traffic.

> 
> - If you have higher protection requirements, you can purchase [Anti-DDoS Pro](https://intl.cloud.tencent.com/product/ddos-bgp), which helps defend against up to 300 GB of attack traffic.
> - To protect the application layer, you can purchase [Tencent Cloud Web Application Firewall (WAF)](https://intl.cloud.tencent.com/product/waf). It protects web security at the application layer against web vulnerability attacks, malicious crawlers, and CC attacks. 
