## Comparative analysis of CLB algorithms

### Weighted round-robin scheduling
The weighted round-robin scheduling algorithm is to schedule requests to different servers based on polling. It can solve problems with imbalanced performance of different servers. It uses weight to represent the processing performance of a server and schedules requests to different servers by weight in a polling manner. It schedules servers based on the number of new connections, where servers with a higher weight receive connections earlier and have a higher chance to be polled. Servers with the same weight will process the same number of connections.
- **Advantage**: this algorithm features simplicity and high practicability. It does not need to record the status of all connections and is therefore a stateless scheduling algorithm.
- **Disadvantage**: this algorithm is relatively simple, so it is unsuitable for situations where the service time of a request changes significantly, or each request needs to consume different amounts of time. In these cases, it will cause imbalanced load distribution among servers.
- **Applicable scenario**: this algorithm is suitable for scenarios where each request consumes basically the same amount of time on the backend with the best loading performance. It is usually used in non-persistent connection services such as HTTP service.
- **Recommendation**: If you know that each request consumes basically the same amount of time on the backend (for example, requests processed by a real server are of the same or similar types), we recommend you use weighted round-robin scheduling. If the time difference between each request is small, we recommend you use this algorithm because it has a low consumption, high efficiency, and no need for traversal.

### Weighted least-connection scheduling
- **How it works**
In actual situations, the time each client request spends on the server may vary greatly. If a simple round-robin or random load balancing algorithm is used as the working time gets longer, the number of connection processes on each server may vary greatly and load balancing may not be achieved. Contrary to round-robin scheduling, least connection scheduling is a dynamic scheduling algorithm that estimates the load on a server based on its number of active connections. The scheduler needs to record the number of connections currently established on each server. If a request is scheduled to a server, its number of connections increases by 1. If a connection stops or times out, its number of connections decreases by 1. The weighted least-connection scheduling algorithm is based on least-connection scheduling, and different weights are allocated to servers according to their processing performance. Based on its weight, the server can then receive a corresponding number of requests. This algorithm is an improvement of least-connection scheduling.
 1. Suppose the weight of a real server is Wi (i = 1... n) and its current number of connections is Ci (i = 1... n). The Ci/Wi value of each server is calculated in sequence. The real server with the smallest Ci/Wi value will be the next server to receive a new request.
 2. For real servers with the same Ci/Wi value, they will be scheduled based on weighted round robin scheduling.
- **Advantages**
This algorithm is suitable for requests requiring long-time processing, such as FTP.
- **Disadvantages**
Due to API restrictions, least-connection and session persistence cannot be enabled at the same time.
- **Use cases**
This algorithm is suitable for scenarios where the time used by each request on the backend varies greatly. It is usually used in persistence connection services.
- **Recommendations**
If you need to process different requests and their service time on the backend varies greatly (such as 3 milliseconds and 3 seconds), we recommend you use weighted least-connection scheduling to achieve load balancing.

### Source hashing scheduling (ip_hash)
- **How it works**
Source hashing scheduling uses the source IP address of the request as the hash key and finds the corresponding server from the statically assigned hash table. The request will be sent to this server if it is available and not overloaded. Otherwise, null will be returned.
- **Advantages**
ip_hash can achieve certain session persistence by remembering the source IP and mapping requests from a client to the same real server via the hash table. In scenarios where session persistence is not supported, ip_hash can be used for scheduling.
- **Recommendations**
This algorithm calculates the hash value of the source address of a request and distributes the request to the corresponding real server based on its weight. This allows requests from the same client IP to be distributed to the same server. This algorithm is suitable for load balancing over TCP protocol that does not support cookie.

## Load Balancing Algorithm Selection and Weight Configuration Examples
In the upcoming features of CLB, **Layer-7 forwarding will support the least-connection balancing method.** We provide examples for your reference on how to choose load balancing algorithm and configure weight, so you can ensure that real server clusters undertake business in different scenarios with stability.
- Scenario 1
Suppose there are 3 real servers with the same configuration (CPU and memory) and you configure their weights all to 10. Suppose 100 TCP connections have been established between each real server and the client. If a new real server is added, we recommend you use the least connection scheduling algorithm, which can quickly increase the load of the 4th server and reduce the pressure on the other 3 servers.
- Scenario 2
Suppose you use Tencent Cloud services for the first time. Your website has just been built and has low load. We recommend you purchase real servers of the same configuration because they are all access-layer servers. In this scenario, you can configure the weights of all real servers to 10 and use weighted round-robin scheduling algorithm to distribute traffic.
- Scenario 3
Suppose you have 5 real servers to undertake simple access requests to static websites, and the ratio of their computing power (calculated by CPU and memory) is 9:3:3:3:1. In this scenario, you can configure the weights of servers to 90, 30, 30, 30, and 10 respectively. As access requests to static websites are mostly of non-persistence connection type, you can use weighted round-robin scheduling algorithm, so CLB can allocate requests based on the performance ratio of real servers.
- Scenario 4
Suppose you have 10 real servers to undertake massive amounts of web access requests, and you do not want to purchase more servers. One of the servers often restarts due to overload. In this scenario, we recommend you configure the weights of existing servers based on their performance. Server with higher load should have a smaller weight. In addition, you can use least-connection scheduling algorithm to allocate requests to real servers with fewer active connections to avoid server overload.
- Scenario 5
Suppose you have 3 real servers to process persistent connections, and the ratio of their computing power (calculated by CPU and memory) is 3:1:1. The server with the best performance processes more requests, but you do not want it to be overloaded. Instead, you want to allocate new requests to idle servers. In this scenario, you can use least connection scheduling algorithm and appropriately reduce the weights of busy servers, so CLB can allocate requests to real servers with fewer active connections, thereby achieving load balancing.
- Scenario 6
Suppose you want subsequent requests from the client to be allocated to the same server. The weighted round-robin or weighted least-connection scheduling cannot ensure that requests from the same client are allocated to the same server. To meet the requirements of your specified application server and maintain the "stickiness" (or "continuity") of client sessions, we recommend you use ip_hash to distribute the traffic. This algorithm ensures that all requests from the same client will be distributed to the same real server, unless the number of servers changes or the server becomes unavailable.

## Difference Between Resetting Weight to 0 and Unbinding Real Server
- Resetting the weight to 0: TCP listeners keep forwarding existing connections, UDP listeners keep forwarding connections with the same quintuple, and HTTP/HTTPS listeners keep forwarding existing connections.
- Unbinding the real server: TCP/UDP listeners stop forwarding existing connections, and HTTP/HTTPS listeners keep forwarding existing connections.


## References
[Managing Real Servers](https://intl.cloud.tencent.com/document/product/214/6156)
