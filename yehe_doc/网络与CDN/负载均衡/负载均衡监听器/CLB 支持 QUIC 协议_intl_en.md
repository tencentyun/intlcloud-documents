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
- The QUIC protocol in CLB is currently in beta test. To use it, please [submit an application](https://cloud.tencent.com/apply/p/9e084vdqdw).
- The QUIC protocol is now available in Beijing, Shanghai, and Mumbai regions.
- Currently, only public network CLB with Layer-7 HTTPS listeners supports the QUIC protocol.

<span id="making"></span>
## Directions
1. Create a CLB instance as needed. For more information, see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
>?When creating a CLB instance, select “Beijing”, “Shanghai” or “Mumbai” for **Region**, and “Public network” for **Network type**.
2. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and click **CLB Instance List** on the left sidebar.
2. On the **Instance Management** page, select the **Cloud Load Balancer** tab.
3. Locate the public network CLB instance created in Beijing, Shanghai or Mumbai region, and click **Configure listener** under the **Operation** column.
![](https://main.qcloudimg.com/raw/75be8dabe196036bd401a3f874fbf194.png)
4. On the **Listener Management** page, click **Create** under **HTTP/HTTPS Listener**.
![](https://main.qcloudimg.com/raw/c84fbc4b37c063b8c13625d87e332df0.png)
5. On the **CreateListener** page, choose “HTTPS” for **Listen Protocol Ports**. Complete other configurations, and click **Submit**.
![](https://main.qcloudimg.com/raw/c1e32add2ab92d9f7866934784179923.png)
6. On the **Listener Management** page, click the **+** symbol next to the listener you just created.
![](https://main.qcloudimg.com/raw/9fdb02a7a98cddbf6eafa1c95c36b93a.png)
7. On the **CreateForwarding rules** page, enable **QUIC** and create a Layer-7 rule. Fill in relevant fields and click **Next** to complete the basic configuration.
>?
>- Currently, a HTTPS listener can only enable the QUIC protocol for one domain name.
>- If you enabled the QUIC protocol when creating a HTTPS listener, you can enable or disable the QUIC protocol later as needed. If you did not enable the QUIC protocol when creating a HTTPS listener, you cannot enable it later.
>- Based on the UDP protocol, QUIC will use the UDP port of a CLB instance. If you enable QUIC for a HTTPS listener, UDP and TCP ports will be used. For example, you enable QUIC for the HTTPS:443 listener, both TCP:443 and UDP:443 ports are used, and you cannot create the TCP:443 or UDP:443 listener.
>
![](https://main.qcloudimg.com/raw/53dae3e54d774586d7e3ac31d7431b6c.png)

## Subsequent Operations
After the basic configuration is completed, you can configure [health check](https://intl.cloud.tencent.com/document/product/214/6097) and [session persistence](https://intl.cloud.tencent.com/document/product/214/6154).
