A load balancing method is an algorithm that allocates traffic to [real servers](https://intl.cloud.tencent.com/document/product/214/32388). Each method produces different load balancing effects.

## Weighted Round-Robin Scheduling
The weighted round-robin scheduling algorithm is to schedule requests to different servers based on polling. It can solve problems with imbalanced performance of different servers. It uses weight to represent the processing performance of a server and schedules requests to different servers by weight in a polling manner. It schedules servers based on the number of new connections, where servers with a higher weight receive connections earlier and have a higher chance to be polled. Servers with the same weight will process the same number of connections.
- **Advantage**: this algorithm features simplicity and high practicability. It does not need to record the status of all connections and is therefore a stateless scheduling algorithm.
- **Disadvantage**: this algorithm is relatively simple, so it is unsuitable for situations where the service time of a request changes significantly, or each request needs to consume different amounts of time. In these cases, it will cause imbalanced load distribution among servers.
- **Applicable scenario**: this algorithm is suitable for scenarios where each request consumes basically the same amount of time on the backend with the best loading performance. It is usually used in non-persistent connection services such as HTTP service.
- **Recommendation**: if you know that each request consumes basically the same amount of time on the backend (for example, requests processed by a real server are of the same type or similar types), you are recommended to use weighted round-robin scheduling. If the time difference between each request is small, this algorithm is also recommended as it has low consumption and high efficiency with no need of traversal.

## Weighted Least-Connection Scheduling
In actual situations, the time requests from the client spend staying on the server may vary greatly. As the working time gets longer, if a simple round-robin or random load balancing algorithm is used, the number of connection processes on each server may vary hugely, which cannot achieve load balancing effect.
Contrary to round-robin scheduling, least-connection scheduling is a dynamic scheduling algorithm that estimates the load of a server by its active connection quantity. The scheduler needs to record the number of current established connections on each server. If a request is scheduled to a server, the number of connections will be increased by 1. If a connection stops or times out, the number of connections will be decreased by 1.
In the weighted least-connection scheduling algorithm that is based on least-connection scheduling, different weights are allocated to servers according to their processing capability. In this way, a server can receive a corresponding number of requests according to its weight, which is an improvement on least-connection scheduling.
>? Suppose that the weight of a real server is wi, and the current number of connections is ci. The ci/wi values of each server are calculated in sequence. The real server with the smallest ci/wi value will be the next server that receives a new request. If there are real servers with the same ci/wi value, they will be scheduled based on weighted round-robin scheduling.

- **Advantage**: this algorithm is suitable for requests requiring long-time processing, such as FTP.
- **Disadvantage**: due to API restrictions, least-connection and session persistence cannot be enabled at the same time.
- **Applicable scenario**: this algorithm is suitable for scenarios where the time used by each request on the backend varies greatly. It is usually used in persistent connection services.
- **Recommendation**: if you need to process different requests and the service time needed by them on the backend varies greatly (such as 3 milliseconds and 3 seconds), you are recommended to use weighted least-connection scheduling to achieve load balancing.

## Source Hashing Scheduling
The source hashing scheduling algorithm (ip_hash) uses the source IP address of the request as the hash key and finds the corresponding server from the statically assigned hash table. The request will be sent to this server if it is available and not overloaded; otherwise, null will be returned.
- **Advantage**: ip_hash can map requests from a client to the same real server through the hash table. Therefore, in scenarios where session persistence is not supported, it can be used to achieve simple session persistence effect.
- **Recommendation**: this algorithm calculates the hash value of the source address of a request and distributes the request to the matched real server based on its weight. In this way, all requests from the same client IP can be distributed to the same server. This algorithm is suitable for the protocols that do not support cookie.

## Choosing Load Balancing Algorithm and Configuring Weight
In order to allow real server clusters to undertake business in a stable manner in different scenarios, some cases regarding how to choose the load balancing algorithm and configure weight are provided below for your reference.
- **Scenario 1**:
 1. Suppose that there are 3 real servers with the same configuration (CPU and memory) and you set all their weights to 10 as they have the same performance.
 2. 100 TCP connections have been established between each real server and the client, and a new real server is added.
 3. In this scenario, you are recommended to use the least-connection scheduling algorithm, which can quickly increase the load of the 4th real server and reduce the pressure on the other 3 ones.
- **Scenario 2**:
 1. Suppose that you use Tencent Cloud services for the first time and your website was just built with low load. You are recommended to purchase real servers of the same configuration since they are all equivalent access-layer servers.
 2. In this scenario, you can set the weights of all real servers to the default value of 10 and use the weighted round-robin scheduling algorithm to distribute the traffic.
- **Scenario 3**:
 1. Suppose that you have 5 real servers that undertake simple access requests to static pages, and the ratio of computing power (calculated by CPU and memory) of these servers is 9:3:3:3:1.
 2. In this scenario, you can set the weight of the real servers to 90, 30, 30, 30, and 10, respectively. As most access requests to static web pages are of non-persistent connection type, you can use the weighted round-robin scheduling algorithm, so that the CLB instance can allocate requests based on the servers' performance ratio.
- **Scenario 4**:
 1. Suppose that you have 10 real servers to undertake massive amounts of web access requests and do not want to purchase more servers as that will increase the expenditure, and one of the servers often restarts due to overload.
 2. In this scenario, you are recommended to set the weights of existing servers based on their performance and set a relatively small weight to servers with high load. In addition, you can use the least-connection scheduling algorithm to allocate requests to real servers with fewer active connections so as to avoid server overload.　
- **Scenario 5**:
 1. Suppose that you have 3 real servers for processing some persistent connections, the ratio of computing power (calculated by CPU and memory) of these servers is 3:1:1.
 2. The server with the best performance processes more requests, but you do not want it to be overloaded and want to allocate new requests to idle servers.
 3. In this scenario, you can use the least-connection scheduling algorithm and appropriately reduce the weight of the busy server, so that the CLB instance can allocate requests to real servers with fewer active connections, thereby achieving load balancing.
- **Scenario 6**:
 1. Suppose that you want subsequent requests from the client to be allocated to the same server. As weighted round-robin or weighted least-connection scheduling cannot ensure that requests from the same client are allocated to the same server,
 2. To satisfy the requirements of your specific application server and maintain the "stickiness" (or "continuity") of the client sessions, you can use ip_hash to distribute the traffic. This algorithm can ensure that all requests from the same client will be distributed to the same real server, unless the number of servers changes or the server becomes unavailable.
