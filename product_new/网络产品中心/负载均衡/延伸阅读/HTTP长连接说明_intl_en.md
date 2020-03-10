Currently, HTTP persistent connection for Layer-7 CLB can be configured to the default value of 75s. You can customize the configuration for different CLB instances. The following describes HTTP persistent connection and non-persistent connection.

## Relationship between HTTP protocol and TCP/IP protocol
HTTP persistent and non-persistent connections are essentially TCP persistent and non-persistent connections. HTTP is an application layer protocol. TCP is used at the transport layer, and IP is used at the network layer. IP protocol mainly solves network routing and addressing problems. TCP protocol mainly solves how to reliably transfer data packets at the IP layer, so all packets can be received in the order they are sent. TCP protocol is reliable and connection-oriented.
 
## What does stateless HTTP protocol mean?
HTTP protocol is stateless, meaning the protocol has no memory for transaction processing, and the server does not know the state of the client. In other words, opening a webpage on a server has nothing to do with the previous opening of a webpage on the same server. HTTP is a stateless and connection-oriented protocol. It does not mean HTTP cannot maintain TCP connections, or it uses the UDP protocol (no connection).
 
## What are persistent and non-persistent connections?
Non-persistent connection is used by default in HTTP/1.0. A connection is established each time the client and server perform an HTTP operation, while terminated when the task ends. If a client browser accesses a webpage of HTML or other formats that contains web resources (such as JavaScript, image, or CSS files), the browser will create an HTTP session each time it encounters such a web resource.

Starting from HTTP/1.1, persistent connection is used by default to maintain the connection. The following code is added in the response header when using HTTP persistent connection:

```
Connection:keep-alive
```

When persistent connection is used, TCP connection used to transfer HTTP data between the client and the server will not be closed after a webpage is opened. When the client accesses the server again, the established connection will be used. `Keep-Alive` does not keep the connection permanently alive, but the time can be configured in different server softwares (such as Apache). To implement persistent connection, both the client and the server should support persistent connection.

HTTP persistent connection and non-persistent connection are essentially TCP persistent connection and non-persistent connection.

### TCP Connection
If TCP protocol is used for network communication, a connection must be established between the client and the server before an actual read/write operation is performed. After the operation is completed, the connection can be released if no longer needed by the two parties. The establishment of a connection relies on a "three-way handshake", while the release requires a "four-way handshake". The establishment of each connection consumes resource and time.

Diagram of connection establishment via three-way handshake:
![](https://main.qcloudimg.com/raw/5cb0bc4a4bef77cef257f2f7055a3529.png)

Diagram of connection close via four-way handshake:
![](https://main.qcloudimg.com/raw/b9a052de2859256d91b43fe99218ab0f.png)

### TCP non-persistent connection
Below is a simulation of TCP non-persistent connection. The client initiates a connection request to the server, the server receives the request, and a connection is established. The client sends a message to the server, the server responds to the client, and a request is completed. Either party can now initiate a close operation, which is usually initiated by the client first. In general, non-persistent connection only passes one single request between the client and the server.

Non-persistent connections are easy to manage, and all existing ones are useful connections that do not require additional control.

### TCP persistent connection
Below is a simulation of persistent connection. The client initiates a connection request to the server, the server accepts the request, and a connection is established. After a request between the client and the server is completed, the connection will not be closed but used for subsequent read and write operations.

TCP keep-alive feature is mainly provided for server applications. If the client has disappeared but the connection is not closed, a half-open connection will be retained on the server, which will wait for data from the client. In this case, the server will keep waiting for data from the client. The keep-alive feature detects half-open connections on the server.

If a given connection has not taken any actions within two hours, the server will send a probe message segment to the client to detect the following four client statuses based on responses from the server host:
- The client host is still running and the server is reachable. TCP response from the client is normal, and the server will reset the keep-alive timer.
- The client host has crashed and shut down or is restarting. The client cannot respond to TCP, and the server will not receive the client’s response to the probe. The server will send a total of 10 probes at an interval of 75 seconds. If the server does not receive any response, it assumes the client has closed and terminated the connection.
- The client has crashed and restarted. The server will receive a response to its keep-alive probe. This response is a reset for the server to terminate the connection.
- The client is running normally but the server is unreachable. This status is similar to the second one.
 
## Pros and cons of persistent and non-persistent connection
Persistent connection can reduce the number of TCP connection establishment and closing, saving time and resources. Persistent connection is suitable for clients that frequently request resources. When persistent connection is used, the client generally does not close the connection. As the number of client connections increases, however, the server will maintain too many connections. In this case, the server may need to close connections that have no requests for a long time, in order to prevent malicious connections from damaging the server. If possible, you can limit the maximum number of persistent connections for each client to avoid malicious clients from damaging the real server.

Non-persistent connections are relatively easy for the server to manage. All existing connections are useful and do not require additional control. However, if client requests are frequent, time and bandwidth will be wasted on the establishment and closing of TCP connections.

Persistent and non-persistent connections are generated based on closing policies adopted by the client and server. The optimal policy varies by use case.
