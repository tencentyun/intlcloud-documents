## Overview

EdgeOne supports the WebSocket protocol that allows the server to proactively send data to the client.

#### What is WebSocket?
WebSocket is a TCP-based persistent protocol that implements full-duplex communication between the client and server and allows the server to proactively send information to the client. Before the emergence of WebSocket, to implement such duplex communication, web applications needed to consistently send HTTP request calls for inquiry, which increased service costs and reduced the efficiency.

Thanks to full-duplex, WebSocket is widely used in scenarios such as social networking subscription, online collaboration, market quotation push, interactive live streaming, online education, and Internet of Things. It can better save server resources and bandwidth and implement communication with higher real-timeliness.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Site Acceleration** > **Network Optimization** on the left sidebar.
2. On the network optimization page, select a site, and toggle the switch of the WebSocket module on/off. 
![](https://qcloudimg.tencent-cloud.cn/raw/3781219b61ab48f0f32588c1bee56869.png)
**Parameter description:**
 - Off (default): WebSocket is disabled.
 - On: WebSocket is enabled.
3. In the WebSocket maximum connection time window, set the maximum duration and click **Save**.
> ?
> - Maximum connection time: If there is no data transmissions within the period, the connection will be disconnected. 
> - The maximum connection duration varies with the following editions:
>   - Enterprise: 300s
>   - Standard: 120s
