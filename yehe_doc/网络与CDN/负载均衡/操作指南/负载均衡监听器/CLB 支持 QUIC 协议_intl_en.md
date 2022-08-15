The [QUIC](https://www.chromium.org/quic) protocol helps you access applications faster and achieves multiplexing with no reconnection required in scenarios such as weak network or frequent switch between Wi-Fi and 4G. This document introduces how to configure QUIC protocol in the CLB console.
## QUIC Overview
Quick UDP Internet Connection (QUIC) is a transport layer network protocol designed by Google, multiplexing concurrent data streams using UDP. Compared with the popular TCP+TLS+HTTP2 protocol, QUIC has the following advantages:
- Establish a connection faster
- Improve congestion control.
- Adopt multiplex to avoid head-of-line (HOL) blocking.
- Suppotrt connection migration.

After QUIC is enabled, the client can establish a QUIC connection with a CLB instance. If the QUIC connection fails due to negotiation between the client and the CLB instance, HTTPS or HTTP/2 will be used. However, the CLB instance and the real server still use the HTTP1.x protocol.

## Usage Limits
- Only CLB instances supports the QUIC protocol.
- Only IPv4 and IPv6 NAT64 CLB supports the QUIC protocol.
- Only public network CLB with layer-7 HTTPS listeners supports the QUIC protocol.
- The QUIC protocol is only available for single-AZ CLB instances.
- Supported QUIC versions: Q050, Q046, Q043, h3-29 and h3-27.


## Directions[](id:making)
1. Create a CLB instance as needed. For more information, see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
>?When creating a CLB instance, select “Beijing”, “Shanghai” or “Mumbai” for **Region**, and “Public Network” for **Network Type**.
>
2. Log in to the [CLB console](https://console.cloud.tencent.com/clb), and click **CLB Instance List** on the left sidebar.
3. On the **CLB Instance List** page, select the **Cloud Load Balancer** tab.
4. Locate the public network CLB instance created in Beijing, Shanghai or Mumbai region, and click **Configure Listener** under the **Operation** column.
![]()
5. On the **Listener Management** page, click **Create** under **HTTP/HTTPS Listener**.
![]()
6. On the **Create Listener** page, choose “HTTPS” as the protocol of the listening port. Complete other configurations, and click **Submit**.
![]()
7. On the **Listener Management** tab, click **+** on the right of the created listener.
![]()
8. On the **CreateForwarding rules** page, enable **QUIC** and create a layer-7 rule. Fill in relevant fields and click **Next** to complete the basic configuration.
>?
>- If you enabled the QUIC protocol when creating an HTTPS forwarding rule, you can enable or disable the QUIC protocol later as needed. If you did not enable the QUIC protocol when creating an HTTPS forwarding rule, you cannot enable it later.
>- Based on the UDP protocol, QUIC will use the UDP port of a CLB instance. If you enable QUIC for a HTTPS listener, UDP and TCP ports will be used. For example, you enable QUIC for the HTTPS:443 listener, both TCP:443 and UDP:443 ports are used, and you cannot create the TCP:443 or UDP:443 listener.
>
![]()

## Related Operations
After the basic configuration is completed, you can configure [health check](https://intl.cloud.tencent.com/document/product/214/6097) and [session persistence](https://intl.cloud.tencent.com/document/product/214/6154).

