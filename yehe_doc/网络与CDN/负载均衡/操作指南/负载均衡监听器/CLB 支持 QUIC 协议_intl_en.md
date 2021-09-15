The QUIC protocol helps you access applications faster and achieves multiplexing with no reconnection required in scenarios such as weak network or frequent switch between Wi-Fi and 4G. This document introduces how to configure QUIC protocol in the CLB Console.
## QUIC Overview
Quick UDP Internet Connection ([QUIC](https://www.chromium.org/quic) is a transport layer network protocol designed by Google, multiplexing concurrent data streams using UDP. Compared with the popular TCP+TLS+HTTP2 protocol, QUIC has the following advantages:
- Reduce the time to establish a connection.
- Improve congestion control.
- Multiplex without head-of-line (HOL) blocking.
- Connection migration.

After QUIC is enabled, the client can establish a QUIC connection with a CLB instance. If the QUIC connection fails due to negotiation between the client and the CLB instance, HTTPS or HTTP/2 will be used. However, the CLB instance and the real server still use the HTTP1.x protocol.
>?Currently, CLB supports QUIC Q044 and earlier versions.

## Use Limits
- The QUIC protocol in CLB is currently in beta test. To use it, please submit an application.
- The QUIC protocol is now available in Beijing, Shanghai, and Mumbai.
- Currently, only public network CLB with layer-7 HTTPS listeners supports the QUIC protocol.
- The current QUIC protocol only supports single-AZ CLB instances.

## Directions[](id:making)
1. Create a CLB instance as needed. For more information, see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
>?When creating a CLB instance, select “Beijing”, “Shanghai” or “Mumbai” for **Region**, and “Public Network” for **Network Type**.
2. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and click **Instance Management** on the left sidebar.
2. On the **Instance Management** page, select the **Cloud Load Balancer** tab.
3. Locate the public network CLB instance created in Beijing, Shanghai or Mumbai region, and click **Configure Listener** under the **Operation** column.
4. On the **Listener Management** page, click **Create** under **HTTP/HTTPS Listener**.
5. On the **Create Listener** page, choose “HTTPS” as the protocol of the listening port. Complete other configurations, and click **Submit**.
6. On the **Listener Management** page, click the **+** symbol next to the listener you just created.
7. On the **CreateForwarding rules** page, enable **QUIC** and create a layer-7 rule. Fill in relevant fields and click **Next** to complete the basic configuration.
>?
>- If you enabled the QUIC protocol when creating a HTTPS fowarding rule, you can enable or disable the QUIC protocol later as needed. If you did not enable the QUIC protocol when creating a HTTPS forwarding rule, you cannot enable it later.
>- Based on the UDP protocol, QUIC will use the UDP port of a CLB instance. If you enable QUIC for a HTTPS listener, UDP and TCP ports will be used. For example, you enable QUIC for the HTTPS:443 listener, both TCP:443 and UDP:443 ports are used, and you cannot create the TCP:443 or UDP:443 listener.
>

## Subsequent Operations
After the basic configuration is completed, you can configure [health check](https://intl.cloud.tencent.com/document/product/214/6097) and [session persistence](https://intl.cloud.tencent.com/document/product/214/6154).

