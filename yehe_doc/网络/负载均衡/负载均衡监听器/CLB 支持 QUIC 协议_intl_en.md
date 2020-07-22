The QUIC protocol helps you access applications much faster and achieves multiplex without a reconnection in scenarios such as frequent switch among weak network, Wi-Fi and 4G. This document introduces how to configure the QUIC protocol in the CLB Console.
## QUIC Overview
Quick UDP Internet Connection ([QUIC](https://www.chromium.org/quic)) is a protocol proposed by Google, which achieves the multiplexed concurrent transmission using UDP. Compared with the popular TCP+TLS+HTTP2 protocol, QUIC has the following advantages:
- Reduced time to establish a connection.
- Improved congestion control.
- Multiplex without the head of line (HOL) blocking.
- Connection migration.

After QUIC is enabled, the client can establish a QUIC connection with a CLB instance. If the QUIC connection fails through negotiation between the client and the CLB instance, HTTPS or HTTP/2 will be used. However, the CLB instance and the real server still use the HTTP1.x protocol.
>?Currently, CLB supports QUIC Q044 and earlier versions.

## Use Limits
- The QUIC protocol in CLB is currently in beta test. If you want to use it, please [submit an application](https://intl.cloud.tencent.com/apply/p/o18084f2opi).
- The QUIC protocol is now available in Beijing, Shanghai, and Mumbai regions.
- Currently, only public network CLB with HTTPS listeners supports the QUIC protocol.

<span id="making"></span>
## Directions
1. Create a CLB instance as needed. For more information, see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
>?When creating a CLB instance, select “Beijing”, “Shanghai” or “Mumbai” for the **Region**, and “Public network” for the **Network type**.
2. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and click **Instance Management** on the left sidebar.
2. On the **Instance Management** page, select the **Cloud Load Balancer** tab.
3. Locate the public network CLB instance created in Beijing, Shanghai or Mumbai region, and click **Configure listener** under the **Operation** column.

4. On the **Listener Management** page, click **Create** under **HTTP/HTTPS Listener**.

5. On the **CreateListener** page, choose “HTTPS” for **Listen Protocol Ports**. Complete other configurations, and click **Submit**.

6. On the **Listener Management** page, click the **+** symbol next to the listener you just created.

7. On the **CreateForwarding rules** page, enable **QUIC** and create a layer-7 rule. Enter information in other fields, and click **Next** to complete the basic configuration.
>?
>- Currently, a HTTPS listener can only enable the QUIC protocol for one domain name.
>- If you enable the QUIC protocol when creating a HTTPS listener, later you can disable the QUIC protocol and enable it again. However, if you choose not to enable the QUIC protocol when creating a HTTPS listener, you cannot enable it later.
>- Based on the UDP protocol, QUIC will use the UDP port of a CLB instance. If you enable QUIC for a HTTPS listener, the UDP and TCP ports will be used. For example, you enable QUIC for the HTTPS:443 listener, both the TCP:443 and UDP:443 ports are used, and you cannot create the TCP:443 or UDP:443 listener.
>


## Next Steps
After the basic configuration is completed, you can continue to configure [health check](https://intl.cloud.tencent.com/document/product/214/6097) and [session persistence](https://intl.cloud.tencent.com/document/product/214/6154).
