## Overview
An L4 proxy provides DDoS protection and layer-4 acceleration services for TCP/UDP applications for a customer. By leveraging widely distributed layer-4 proxy nodes, unique DDoS module, and smart routing technology, EdgeOne implements nearby access for end users, edge traffic cleansing, and port monitoring and forwarding. It thus offers high-availability and low-latency security and acceleration services for layer-4 applications.
![](https://qcloudimg.tencent-cloud.cn/raw/3db86a3bbe4ece921d10b206cccc62fd.png)
>?
>- The EdgeOne console is now only available to beta users. [Contact us](https://intl.cloud.tencent.com/contact-us) to join the beta.
>- Only one L4 proxy can be created for each site. To create multiple proxies, please [contact us](https://intl.cloud.tencent.com/contact-us).
>- An L4 proxy provides DDoS protection capability for the customer and cannot be disabled.
>- An L4 proxy doesn't support IPv6 origin servers.

## Creating an L4 proxy
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **L4 Proxy** on the left sidebar.
2. On the L4 proxy page, select the target site and click **Create L4 proxy**.
3. On the L4 proxy creation page, set **Service configurations** parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/8486449940ac85f2af3802548c9a0dae.png)

**Parameter description:**
 - **Service name**: Name of the layer-4 proxy instance. The number of instances that can be created is subject to the site package.
 - **Scheduling mode**: Select the method of connecting the layer-4 proxy service.
    - **CNAME** (recommended): A CNAME record is used as the connection address, which supports stronger DDoS protection, nearby access and acceleration as well as L4 forwarding and acceleration.
    - **Anycast IP**: Use an Anycast IP as the access point. In this mode, , which supports DDoS protection and L4 forwarding and acceleration.
>?If site acceleration is also enabled for the host, the scheduling mode can only be set to **CNAME**.
>
 - **Proxy**: Configure the layer-4 proxy mode.
    - **DDoS protection**: Layer-3 and layer-4 DDoS protection is enabled by default and cannot be disabled. You can go to [DDoS Protection](https://console.cloud.tencent.com/edgeone/security/ddos) to modify the default DDoS policies.
    - **L4 acceleration**: Provide L4 acceleration and reduce network transmission delay. 
4. On the L4 proxy service creation page, click **Add rule** and configure **Forwarding rules** parameters.
>?You can add up to 100 forwarding rules for each L4 proxy.

 ![](https://qcloudimg.tencent-cloud.cn/raw/9f872baa5431ef82e5eb7b34273c6b26.png)

**Parameter description:**
 - **Forwarding protocol**: TCP and UDP are supported.
 - **Forwarding port**: The supported port range is 1–64999, excluding 36000 and 56000. You can enter multiple ports separated with commas or use a hyphen to enter a port range. You can enter up to 20 ports in a forwarding rule.
>?If site acceleration is also enabled for the host, forwarding ports 80 and 443 are not supported.
>
 - **Origin type**/**Origin server**:
    - **Single origin**: You can enter multiple origin servers in the format of **origin server address:port** and separate them with commas.
    - **Origin group**: Select an existing [origin group](https://intl.cloud.tencent.com/document/product/1145/46159) with the forwarding port, or create a new origin group.
 - **Pass client IP**: Specify how real client IPs are passed for layer-4 proxy nodes.
     - **TOA**: Pass client IPs via TCP Option (type 200), which only supports TCP protocols.
     - **Proxy Protocol V1** (recommended): Pass client IPs as plaintext via the TCP header, which only supports TCP protocols.
     - **Proxy Protocol V2**: Client IPs will be transferred through the header. V2 uses the binary format and supports both TCP and UDP protocols. Each data packet carries a PPv2 header for TCP, while only the first data packet carries the header for UDP.
     - **Session persistence**: As long as an origin server IP remains unchanged, traffic from the same client IP will always be forwarded to it.
  - **Not passed**: Real client IPs will not be transferred.


## Batch Importing Forwarding Rules[](id:batch)
You can batch import forwarding rules when creating the proxy or batch import rules later in the proxy details page.
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **L4 Proxy** on the left sidebar.
2. On the traffic analysis page, select the target site and click **Create L4 proxy**.
3. In the forwarding rules module of the L4 proxy creation page, click **Batch import**.
![](https://qcloudimg.tencent-cloud.cn/raw/1fc717b9c79c057b1fddd1d8dddb93a3.png)
4. In the batch import window, enter the rules to import and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/f71aa062bb33e7a1343b88fe75017d18.png)
 - Batch import format description:
     - Up to 100 forwarding rules can be entered, one rule per line.
     - Each line contains 4 fields that are space-separated and case-insensitive.
     - The fields from left to right are listed as below:
      - Forwarding protocol:Port: For example, `tcp:123`.
      - Origin server: You can enter origins (`test.origin.com:456`) or origin groups (`og:OriginGroupName`).
      - IP passing method: `TOA`, `PPv1`, `PPv2`, or `off`.
      - Session persistence: `on` or `off`.
 - Sample request: 
```js.
tcp:123 test.origin.com:456 on ppv1
udp:2330 og:l4testkb off ppv2
```
The result of the batch import is the same as the following configuration:
![](https://qcloudimg.tencent-cloud.cn/raw/e7e3556cd049a0f328d49687b0863a99.png)
