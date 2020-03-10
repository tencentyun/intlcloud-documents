## What is session persistence?
Session persistence is a common and rather complex topic in CLB. Sometimes, session persistence is referred to as sticky session. It is a mechanism that can identify client-server affinity and guarantee that associated access requests will be allocated to the same server during load balancing.


## When is session persistence needed?
First, we need to understand some concepts: connection, session and their differences. Note that connection and session mean the same if we only talk about load balancing.

To put it simple, it is a session if users need login. Otherwise, it is a connection.

For data packets in the same connection, CLB will perform network address translation (NAT) on them and forward them to a fixed real server for further processing. A table in CLB system records information about the connection status, such as **source IP: port**, **target IP: port**, **server IP: port**, and idle timeout period (`Idle Timeout`). Because the table used to record connection status consumes system memory resources, its size cannot be infinite. All traditional vendors will have certain limits on its size, which is called the maximum number of concurrent connections, i.e., the maximum number of connections that the system can sustain at the same time. In CLB’s current connection status table, an `Idle Timeout` parameter is provided. When a connection has no traffic within the idle timeout period, CLB will automatically delete it and release system resources.

After the connection is deleted, client requests may not be sent to the same real server. Instead, the traffic distribution policy of CLB prevails.

In some scenarios where login is necessary, a session is required between the client and server to record client information.
For example, in most ecommerce application systems or online systems that require identity verification, a transaction or request can be completed after several rounds of interactions between the client and server. As these interactions are closely related, the server needs to know the results of the last one or several interactions before performing a new one. This requires that all these interactions are completed on the same server, instead of being distributed to different servers by CLB. Otherwise, the following exceptions may occur:
- The client enters the correct username and password but is repeatedly redirected to the login page.
- The client enters the correct verification code but repeatedly receives a verification code error notification.
- Items added to the shopping cart in the client are lost.

Session persistence is required to ensure that requests from the same client will be forwarded to the same real server for processing in certain situations. In other words, multiple connections established between the client and servers are sent to the same server for processing. If load balancer is deployed between the client and servers, these connections will likely be forwarded to different servers for processing. If there is no session information synchronization mechanism between servers, other servers cannot authenticate the user and exceptions may occur when the user interacts with the application system.

CLB forwards requests and connections from clients evenly to multiple servers to avoid overload on a single server. The session persistence mechanism requires certain requests to be forwarded to the same server for processing. In actual deployment environment, an appropriate session persistence mechanism needs to be selected based on the application environment.

## Session persistence types
### Session persistence based on source address (Layer-4 session persistence)
Session persistence based on source address (also called IP-based session persistence or simple session persistence) is when CLB uses the source address of the access request as the basis to evaluate the associated session. All access requests from the same IP address will be forwarded to the same server during load balancing.

An important parameter in simple session persistence is connection timeout period, which is a time value configured by CLB for each connected session. If the time interval between the last completion of the session and the next is less than this value, CLB will persist the session for the new connection. Otherwise, CLB will consider the new connection as a new session and perform load balancing.

Simple session persistence can be easily implemented based on Layer-3 and Layer-4 information of data packets, improving efficiency.
![](http://mc.qcloudimg.com/static/img/946088003aa5a23d21b12de69cc23ad3/image.png)

However, the problem with this method is when multiple clients access servers through proxy or address translation, requests from the same source address will be allocated to the same server, resulting in severe load imbalance between servers.

In another situation, a client generates a large number of concurrent requests that need to be allocated to multiple servers for processing while persisting the session. In this case, session persistence based on source client address will cause load balancing to fail.

If the above problems occur, you must consider using other types of session persistence.

### Cookie-based session persistence (Layer-7 session persistence)
In cookie-based session persistence, the client and load balancer process the cookie, which is transparent to the real server.
#### Processing logic for initial client request
1. When the client initiates a request for the first time, the request header does not have the session persistence cookie. CLB receives the request and finds that the request header has no session persistence cookie, so it will select a server based on the polling algorithm.
2. The real server processes the request and returns the response header and content to the CLB instance.
3. CLB generates a cookie and stores it in the memory.
4. CLB returns the request response to the client.

#### Processing logic for subsequent client requests during the session persistence period
1. When the client sends a new request, the request must carry a session persistence cookie.
2. CLB receives the cookie, finds through the algorithm the real server that processes the previous request, and forwards the request to that server.

![](https://main.qcloudimg.com/raw/dbf107c8a09531bd8bd1fa598dcfb9fb.png)

### Session Persistence
This method implements session persistence simultaneously with load balancing by sharing a session among multiple real servers.
1. Stored in database
The session information can be stored in a database table for sharing among application servers. This method is suitable for websites with low database access requests.
 - Advantage: easy to implement.
 - Disadvantage: compared to an application server, database server is harder to scale out and its resources are more valuable. In web applications with high concurrence, the performance of database server is usually affected. If sessions are stored in database tables, frequent database operations will affect the business.
2. Stored in file system
A file system such as NFS can be used to share sessions among multiple servers. This method is suitable for websites with low concurrence.
 - Advantage: only disks that store sessions need to be mounted to servers, which is easy to implement.
 - Disadvantage: NFS cannot provide high performance for high-concurrence reads/writes. Its disadvantages are in hard disk I/O performance and network bandwidth, especially for frequent reads/writes on small files such as sessions.
3. Stored in Memcached
Memcached can be used to store session data, which is read directly from the memory.
 - Advantage: high efficiency and faster session reads/writes compared to when stored in file system. Sharing sessions among servers is also more convenient, as servers can be simply configured to use the same group of Memcached servers to reduce additional workload.
 - Disadvantage: once Memcached is down, data in the memory will be lost, even though it is not a serious issue for session data. If the number of access requests to a website is high and there are too many sessions, Memcached will delete those that are not commonly used. If the user resumes use after a certain period of time, however, the session will fail to be read.
