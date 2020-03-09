Communication of a web application is as follows: the client sends a request via the browser, the server receives the request, processes it, and returns the result to the client. The client's browser then displays the information. This mechanism better support applications with infrequent information change. However, it may be less effective for applications with high requirement for real-time transmission and high concurrence. Given the robust growth of mobile internet, web application frequently encounters high concurrence and demands for real-time response. This includes real-time information on financial securities, geographic information in web-based navigation apps, and real-time message push in social network.

To manage these business scenarios, web development based on request-response mode generally uses real-time communication method such as polling. When using polling, the client frequently sends requests to the server at certain intervals to keep data synced between the client and server. But when the client sends requests to the server at fixed intervals, data on the server may be outdated, generating a large number of unnecessary requests that waste bandwidth and reduce efficiency.

Adobe Flash uses its embedded Socket to implement data exchange and Flash to expose related APIs for JavaScript to call, achieving real-time communication. This method is more efficient than polling, because Flash is commonly installed and widely used. However, Flash is not well supported on mobile devices. iOS does not support Flash, while Android provides poor support for Flash with high requirements for hardware configuration. In 2012, Adobe announced that Flash no longer supported Android 4.1 and above, marking the end of Flash on mobile devices.

Traditional web modes would encounter difficulties when handling demands with high concurrence and real-time communication. A bi-directional communication mechanism with cost efficiency was required to facilitate real-time data transmission. WebSocket, known as "web TCP", was thereby developed based on HTML5. At the early stage, the industry had no unified HTML5 specification. Browser and application server vendors had different implementation methods, such as MQTT of IBM and Comet’s open-source framework. In 2014, HTML5 was established as a standard specification. Application server and browser vendors gradually unified their HTML5 implementation, and WebSocket protocol was implemented in Java EE 7. At this point, WebSocket for clients and servers is fully established. For more information on the new HTML protocol and WebSocket support, see [HTML5 Specification](http://www.jb51.net/w3school/html5/).

## WebSocket Mechanism
The following is an overview of the principle and operating mechanism of WebSocket.

WebSocket is a new HTML5 protocol, which implements full-duplex communication between browser and server. It supports real-time communication and reduces the consumption of server resources as well as bandwidth. Similar to HTTP, WebSocket uses an established TCP connection to transmit data. However, their biggest differences are:
- WebSocket is a bi-directional communication protocol. After a connection is established, WebSocket server and client can actively send or receive data to and from each other, which is similar to Socket.
- Like TCP, a connection should be established first with WebSocket before communication can be made.

The traditional HTTP request-response mode between server and client is as shown below:
![](https://main.qcloudimg.com/raw/44a1251733ad215969b14f66a0f2ec61.jpg)

The WebSocket client-server request-response mode is as shown below:
![](https://main.qcloudimg.com/raw/f62fa2415a9f8bdcbe6ea2053aca41ed.jpg)

In traditional HTTP mode, each request-response requires a new connection between the client and server. WebSocket, which is similar to Socket, is a communication mode based on persistent TCP connection. Once a WebSocket connection is established, subsequent data will be transmitted in the form of frame sequence. The client or server does not need to initiate a connection request again before WebSocket is disconnected. In scenarios with high concurrence or high volumes of load traffic on client and server, WebSocket significantly reduces consumption of network bandwidth resources and improves performance. In addition, the client sends and receives messages over a persistent connection, achieving real-time communication.

Compared to HTTP persistent connection, WebSocket has the following advanatges:
- It is a real full-duplex method. The client and server are completely equal after a connection is established. They can initiate requests proactively. In contrast, HTTP persistent connection is based on HTTP. It uses the traditional mode where the client initiates a request to the server.
- In addition to real data, a large number of HTTP headers are exchanged between the client and server in HTTP persistent connection, which reduces data exchange efficiency. In WebSocket protocol, data can be exchanged without HTTP headers after a TCP connection is established through the first request. Given this difference, WebSocket can be implemented after client and server upgrades (mainstream browsers already support HTML5). WebSocket also has distinct features such as multiplexing and reusable WebSocket connection by different URLs.


Below is a comparison between WebSocket and traditional HTTP based on messages exchanged between the client and the server:

The new WebSocket instantiates a new WebSocket client object on the client and requests a WebSocket URL similar to ws://yourdomain:port/path from the server. The client WebSocket object automatically parses and recognizes the WebSocket request, connects the server port, and implements handshake. The client sends data in the following format:

```
GET /webfin/websocket/ HTTP/1.1
Host: localhost
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: xqBt3ImNzJbYqRINxEFlkg==
Origin: http://localhost:8080
Sec-WebSocket-Version: 13
```

As can be seen above, the WebSocket connection message initiated by the client is similar to the traditional HTTP message. `Upgrade: websocket` indicates a WebSocket request, and `Sec-WebSocket-Key` indicates a Base64-encoded ciphertext sent by the WebSocket client. The server must return a corresponding encrypted `Sec-WebSocket-Accept` response. Otherwise, the client will throw an `Error during WebSocket handshake` error and close the connection.

After receiving the message, the server returns data in the following format:

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: K7DJLdLooIwIG/MOpvWFB3y3FE8=
```

The value of `Sec-WebSocket-Accept` is calculated by the server using the same key as that of the client and then returned to the client. `HTTP/1.1 101 Switching Protocols` indicates that the server accepts the connection from the client over WebSocket. After this request-response, WebSocket handshake between the client and server is completed. TCP communication can now be implemented. For more information on data exchange format between WebSocket client and server, see [WebSocket Protocol Stack](http://tools.ietf.org/html/rfc6455).

WebSocket API is easy to use in development. You only need to instantiate WebSocket and create a connection. The server and client can then send messages to each other and respond accordingly. For more information on WebSocket API and code implementation, see WebSocket implementation and case analysis sections.

Tencent Cloud offers Layer-7 public network CLB for daily rental whose forwarding module supports WebSocket. Multiple customers such as Heroes Evolved and Yinhan Games have connected to this service. If incompatibility occurs, modify the WebSocket configuration. The WebSocket server does not verify circled fields in the figure below:

![](https://main.qcloudimg.com/raw/bd313e9a949fb949256be37499354d4b.png)

To use WebSocket in your video business, follow the steps below:
- Use heartbeat to maintain WebSocket linkage and detect whether influencers or VJs on the client are online.
- Configure `proxy_read_timeout` of Layer-7 CLB instance to 60s.
- Configure the heartbeat to 50s, so WebSocket can be connected for the long term.

Custom configuration for WebSocket is coming soon.
