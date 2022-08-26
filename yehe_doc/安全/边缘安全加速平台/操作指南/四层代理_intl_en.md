## Overview
L4 proxy provides customer-grade DDoS protection and layer-4 acceleration services for TCP/UDP applications. By leveraging widely distributed layer-4 proxy nodes, unique DDoS module, and smart routing technology, EdgeOne implements nearby access for end users, edge traffic cleansing, and port monitoring and forwarding. It thus offers high-availability and low-latency security and acceleration services for layer-4 applications.
![](https://qcloudimg.tencent-cloud.cn/raw/3db86a3bbe4ece921d10b206cccc62fd.png)
>?
>- The EdgeOne console is not yet fully available. To access the console, please [contact us](https://intl.cloud.tencent.com/contact-us) for activation.
>- Only one L4 proxy can be created for each site. To create multiple proxies, please [contact us](https://intl.cloud.tencent.com/contact-us).
>- L4 proxy provides customer-grade DDoS protection capability by default, which cannot be disabled.
>- L4 proxy currently doesn't support IPv6 origin servers.

## Creating a L4 proxy
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **L4 Proxy** on the left sidebar.
2. On the page that appears, select the target site and click **Create L4 proxy**.
3. On the L4 proxy creation page, set **Service configurations** parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/8486449940ac85f2af3802548c9a0dae.png)

**Parameter description:**
 - Service name: Name of the layer-4 proxy instance. The number of instances that can be created is subject to the site package.
 - Scheduling mode: Select the method of connecting the layer-4 proxy service.
    - CNAME (recommended): A CNAME record is used as the connection address, which supports stronger DDoS protection, nearby access and acceleration as well as L4 forwarding and acceleration.
    - Anycast IP: An Anycast IP is used as the connection address, which supports DDoS protection and L4 forwarding and acceleration.
>?If site acceleration is also enabled for the host, the scheduling mode can only be set to "CNAME".

 - Proxy mode: Configure the layer-4 proxy mode.
    - DDoS protection: Enable layer-3 and layer-4 DDoS protection by default. To disable it, you can go to [DDoS Protection](https://console.cloud.tencent.com/edgeone/security/ddos) to modify the default DDoS policy.
    - L4 acceleration: Provide L4 acceleration and reduce network transmission delay. You can choose to enable or disable it.
4. On the L4 proxy service creation page, click **Add rule** and configure **Forwarding rules** parameters.
>?You can add up to 100 forwarding rules for each L4 proxy.

 ![](https://qcloudimg.tencent-cloud.cn/raw/9f872baa5431ef82e5eb7b34273c6b26.png)

**Parameter description:**
 - Forwarding protocol: TCP and UDP are supported.
 - Forwarding port: The supported port range is 1–64999, excluding 36000 and 56000. You can enter multiple ports separated with commas or use a hyphen to enter a port range. You can enter up to 20 ports in a forwarding rule.
>?If site acceleration is also enabled for the host, forwarding ports 80 and 443 are not supported.

 - Origin server type/information:
    - Single origin: You can enter one or more origin servers in the format of **origin server address:port** and separate them with commas.
    - Origin group: Select origin servers from an existing [origin group](https://intl.cloud.tencent.com/document/product/1145/46159). You can only select an origin group with origin-pull port information or create one here.
 - Pass client IP: Specify how real client IPs will be carried when layer-4 proxy nodes are used for origin-pull.
     - TOA: Pass client IPs via TCP Option (type 200), which only supports TCP protocols.
     - Proxy Protocol V1 (recommended): Pass client IPs as plaintext via the TCP header, which only supports TCP protocols.
     - Proxy Protocol V2: Client IPs will be transferred through the header. V2 uses the binary format and supports both TCP and UDP protocols. Each data packet carries a PPv2 header for TCP, while only the first data packet carries the header for UDP.
     - Not passed: Real client IPs will not be transferred.
  - Session persistence: As long as an origin server IP remains unchanged, traffic from the same client IP will always be forwarded to it.


## Importing Forwarding Rules in Batches[](id:batch)
When you create or view a L4 proxy, forwarding rules can be imported in batches.
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **L4 Proxy** on the left sidebar.
2. On the page that appears, select the target site and click **Create L4 proxy**.
3. In the forwarding rules module of the L4 proxy creation page, click **Batch import**.
![](https://qcloudimg.tencent-cloud.cn/raw/1fc717b9c79c057b1fddd1d8dddb93a3.png)
4. In the batch import window, enter the required rules and click **Submit**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f71aa062bb33e7a1343b88fe75017d18.png" style="zoom:80%;" />

 - Batch import format description:
     - Up to 100 forwarding rules can be entered, one rule per line.
     - Each line contains 4 fields that are space-separated and case-insensitive.
     - The fields from left to right are listed as below:
      - Forwarding protocol:Port: For example, `tcp:123`.
      - Origin server: Enter a single origin server in the format of `test.origin.com:456`, or an origin group in the format of `og:OriginGroupName`.
      - Session persistence status: `on` or `off`.
      - IP passing method: `TOA`, `PPv1`, `PPv2`, or `off`.
 - Sample request: 
```js.
tcp:123 test.origin.com:456 on ppv1
udp:2330 og:l4testkb off ppv2
```
The configuration is shown as below:
![](https://qcloudimg.tencent-cloud.cn/raw/e7e3556cd049a0f328d49687b0863a99.png)
