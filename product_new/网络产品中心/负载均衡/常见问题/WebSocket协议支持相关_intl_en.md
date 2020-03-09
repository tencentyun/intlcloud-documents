## Product Content
### What is WS/WSS?
WebSocket (WS) is a protocol that provides full-duplex communication channels over a single TCP connection.
WebSocket facilitates data exchange between the client and server, and allows active data push from the server to client. In WebSocket API, only one handshake is required between the browser and server to create a persistent connection and carry out bi-directional data transmission.

### Why should WS/WSS be used?
Without WebSocket, the client has to pull data from the server through polling.
There are two shortcomings in this data exchange method:
1. Low efficiency. To pull real-time data, the client has to frequently initiate the Ajax request.
2. The server cannot push data proactively.
WebSocket is designed to solve these problems. As a new protocol released when HTML5 was launched, WebSocket achieves full-duplex communication between the browser and server. It can transmit message-based text and binary data, solving HTTP problems at the protocol level.

Key advantages of WebSocket:
1. Less overhead. After the connection is established, the packet header used for control is small. Compared to a HTTP request that requires a complete header, WebSocket helps reduce the overhead.
2. Real-time push. As a full-duplex protocol, WebSocket can achieve real-time data push from server to client.
3. Persistent connection.

## Product Purchase
### How is WS/WSS billed?
CLB supports WS/WSS by default and no additional fees will be charged.

## Product Implementation
### How to enable WS/WSS on CLB?
**WS/WSS is enabled by default and no additional configuration is required.**
If the listener listens to HTTP, WS is supported by default. If it listens to HTTPS, WSS is supported by default.
When WSS is used, CLB will carry out SSL offloading.

### Which regions support WS/WSS?
Currently, WS/WSS protocols are supported in **all regions**.

