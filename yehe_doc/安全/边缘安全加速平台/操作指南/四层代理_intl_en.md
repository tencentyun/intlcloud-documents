## Overview
Layer-4 proxy provides customer-grade anti-DDoS and layer-4 acceleration services for TCP/UDP applications. By leveraging widely distributed layer-4 proxy nodes, unique anti-DDoS module, and smart routing technology, EdgeOne implements nearby access for end users, edge traffic cleansing, and high-speed connection-based proxying and forwarding. It thus offers high-availability and low-latency security and acceleration services for layer-4 applications.
![](https://qcloudimg.tencent-cloud.cn/raw/3db86a3bbe4ece921d10b206cccc62fd.png)

>?
>- Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.
>- Layer-4 proxy provides customer-grade anti-DDoS and monitoring services by default, which cannot be disabled.
>- Layer-4 proxy currently doesn't support IPv6 origin servers.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Layer-4 proxy** on the left sidebar.
2. On the traffic analysis page, select the target site and click **Create service**.
3. On the layer-4 proxy service creation page, set **Service configuration** parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/8486449940ac85f2af3802548c9a0dae.png)

**Parameter description:**
 - Service name: Name of the layer-4 proxy instance. The number of instances that can be created is subject to the site package.
 - Scheduling mode: Select the method of connecting the layer-4 proxy service.

    - CNAME: A CNAME record is used as the connection address, which supports layer-4 acceleration, has more powerful anti-DDoS capabilities, and is thus recommended.
    - Anycast IP: An Anycast IP is used as the connection address, which supports anti-DDoS and layer-4 port forwarding but not layer-4 acceleration.
 - Client IP transfer: It specifies how real user IPs will be carried if you select layer-4 proxy node for origin-pull.
    - TOA: Client IPs will be transferred through `TCP Option (type 200)`.
    - Proxy Protocol V1 (recommended): Client IPs will be transferred through the TCP header of the PP protocol. V1 uses plaintext transfer and supports the TCP protocol. If the UDP protocol is used, IPs may fail to be transferred normally.
    - Proxy Protocol V2: Client IPs will be transferred through the header. V2 uses the binary format and supports both TCP and UDP protocols. Each data packet carries a PPv2 header for TCP, while only the first data packet carries the header for UDP.
    - Not transferred: Client IPs won't be transferred.

 - Layer-4 acceleration: You can enable layer-4 high-speed connection to greatly reduce the latency and jitters. **This feature incurs additional acceleration traffic fees**.
 - Session persistence: As long as an origin server IP remains unchanged, traffic from the same client IP will always be forwarded to it.

4. On the layer-4 proxy service creation page, click **Add rule** and configure **Forwarding rule** parameters.
>?You can add up to 100 forwarding rules for each layer-4 proxy service.

 ![](https://qcloudimg.tencent-cloud.cn/raw/9f872baa5431ef82e5eb7b34273c6b26.png)

**Parameter description:**
 - Forwarding protocol: TCP and UDP are supported.
 - Forwarding port: The supported port range is 1–64999, excluding 36000 and 56000. You can enter multiple ports separated with commas or use a hyphen to enter a port range. You can enter up to 20 ports in a forwarding rule.
 - Origin server type/information:
    - Add manually: You can enter multiple origin servers in the format of **origin server address:port** and separate them with commas.
    - Origin server group: Select origin servers from an existing [origin server group](https://intl.cloud.tencent.com/document/product/1145/46159). You can only select an origin server group with origin-pull port information or create a group here.
