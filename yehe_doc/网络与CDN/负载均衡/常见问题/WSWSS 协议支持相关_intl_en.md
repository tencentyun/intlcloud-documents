<span id="1"></span>
**Product Introduction**
- [What is WS/WSS?](#2)
- [Why should WS/WSS be used?](#3)

**Product Purchase**
- [How is WS/WSS billed?](#4)

**Product Implementation**
- [How do I enable WS/WSS for CLB?](#5)
- [Which regions support WS/WSS?](#6)




[](id:2)
### What is WS/WSS?
WebSocket (WS) is a protocol that provides full-duplex communication channels over a single TCP connection.
WebSocket facilitates data exchange between the client and server, and allows active data push from the server to client. In WebSocket API, only one handshake is required between the browser and server to create a persistent connection and carry out bi-directional data transmission.

[[Back to Top]](#1)


[](id:3)
### Why should WS/WSS be used?
Without WebSocket, the client has to pull data from the server through polling.
There are two shortcomings in this data exchange method:
1. Low efficiency. To pull real-time data, the client has to frequently initiate the Ajax request.
2. The server cannot push data proactively.
WebSocket is designed to solve these problems. As a new protocol released when HTML5 was launched, WebSocket achieves full-duplex communication between the browser and server. It can transmit message-based text and binary data, solving HTTP problems at the protocol level.

Key advantages of WebSocket:
1. Less overhead. After the connection is established, the packet header used for control is small. Compared to an HTTP request that requires a complete header, WebSocket helps reduce the overhead.
2. Real-time push. As a full-duplex protocol, WebSocket can achieve real-time data push from server to client.
3. Persistent connection.

[[Back to Top]](#1)



[](id:4)
### How is WS/WSS billed?
CLB supports WS/WSS by default and no additional fees will be charged.

[[Back to Top]](#1)



[](id:5)
### How do I enable WS/WSS for CLB?
**WS/WSS is enabled for CLB by default.** If a connection is idle for more than 60s, you need to customize the `proxy_read_timeout` parameter, which should be less than 900s preferably. For more information, see [Layer-7 Custom Configuration](https://intl.cloud.tencent.com/document/product/214/32427).
If the listener listens to HTTP, WS is supported by default. If it listens to HTTPS, WSS is supported by default.
When WSS is used, CLB will carry out SSL offloading.
[[Back to Top]](#1)



[](id:6)
### Which regions support WS/WSS?
Currently, WS/WSS protocols are supported in **all regions**.

[[Back to Top]](#1)

