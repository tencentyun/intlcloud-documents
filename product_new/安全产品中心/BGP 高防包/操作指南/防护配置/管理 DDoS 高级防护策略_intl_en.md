Anti-DDoS Pro provides advanced protection policies against DDoS attacks. You can adjust and optimize the anti-DDoS protection policy as required through blacklists/whitelists, disabling protocols and ports, packet attribute filtering, connection flood protection, and watermark protection.

## Configuration Item Overview

| Configuration Item       | Description                                                     | Effective Time                                 |
| ------------ | ------------------------------------------------------------ | ---------------------------------------- |
| Blacklist/Whitelist     | IP-based protection.<br/><ul><li>Always allow requests from IPs in the whitelist </li><li>Always blocks requests from IPs in the blacklist</li></ul> | The configuration takes effect immediately.                  |
| Restricted Protocol     | Disables a protocol not used by the service.<br/>If attacks are detected, the Anti-DDoS Pro cluster will cleanse the protocol’s traffic. | The configuration takes effect immediately.             |
| Restricted Port     | Disables a port not used by the business.<br/>If attacks are detected, the Anti-DDoS Pro cluster will cleanse traffic from the restricted ports. | The configuration takes effect immediately.    |
| Packet Filter Attribute | Combines criteria to set policy operations, such as the protocol, port range, packet range, whether to detect load, offset, detection depth, and whether to include feature strings based on the business or attack packets.<br/>If the packets match the policy criteria, operations such as direct forwarding, discarding, source IP blocking, or disconnecting can be executed. | The configuration takes effect immediately.                 |
|Speed Limit|Destination IP–based protection which limits the speed of the access protocol.|The configuration takes effect immediately.|
| Block traffic from outside China | Rejects TCP traffic requests from outside China (including mainland China, Hong Kong, Macao, and Taiwan).      | It takes effect when the protected IPs are under attack. |
| Null Session Protection   | Protects against null session attacks.                                             | It takes effect when the protected IPs are under attack. |
|Connection Flood Protection | IP-based protection which limits the speed, packet length, and other parameters of connections accessing the IPs protected by Anti-DDoS Pro to protect against light traffic connection attacks.|The configuration takes effect immediately.|
| Exceptional Connection Detection | When a source IP receives a TCP connection meeting the configured parameter features, the connection is treated as exceptional. If the amount of exceptional connections received by the source IP exceeds the maximum allowable number, the connection will be added to the blacklist for a certain period and will not be accessible.|The configuration takes effect immediately after saving.|
| Watermark Protection   | Supports UDP and TCP packets. Watermark detection and stripping will be executed for the payloads within the configured port range. Watermark protection can protect against Layer-4 CC attacks, such as mimicking business packet attacks and replay attacks.<br/><ul><li>Customer client and Tencent Cloud Anti-DDoS Pro system share the same watermark algorithm and key.<br/></li><li>Each packet sent by the client is embedded with watermark features. However, attack packets do not have watermark features.<br/></li><li>The Anti-DDoS Pro system will identify and discard attack packets.                                             | The configuration takes effect immediately after saving. |

## Adding Policies

> Configuration of advanced protection policy requires techical expertise. You are advised to read the operation guide and then configure the policy as required.

Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **DDoS Advanced Protection Policy** tab, click **Adding Policy**. Configure the following parameters as required and click **OK**.
![](https://main.qcloudimg.com/raw/c2a87e41474ccab53db928e7c0776037.png)

- **Policy Name**
  Enter a policy name with 1-32 characters.
- **Blacklist/Whitelist**
 - If you need to set a blacklist, click **Add**, select **Blacklist**, enter IPs to block, and then click **OK**. Separate multiple IPs with carriage returns.
 - If you need to set a whitelist, click **Add**, select **Whitelist**, enter the IP to pass directly, and then click **OK**. Separate multiple IPs with carriage returns.
>You can add up to 100 IPs for the blacklist and whitelist. The number of IPs to add in a batch cannot exceed the current available quota.

 ![](https://main.qcloudimg.com/raw/033a07a945ddfc12c9fdf3238f81b03a.png)

- **Restricted Protocol**
  Select the protocol you want to disable.
- **Restricted Ports**
  Select a protocol, and then enter the ports to disable. If you only need to disable one port in an entry, enter the same number for the starting and ending ports. Click **Add** under the list to add more entries.
- **Packet Filter Attribute**
  Set conditions such as the protocol, port range, packet length, payload detection, offset, detection depth, and featured strings 

 > - Offset: Specifies the start position of the matched features in the packets.
 >- Detection depth: Specifies the packet length from the position set by the offset to the end of the matching content. It is used with the offset.
 > - Policy:
 >   - **Discard packet**: Discards the data packet matching the packet filtering attributes.
 >   - **Discard and block the source IP**: Discards the data packet matching the packet filtering attributes and temporarily blocks the source IP.
 >   - **Discard and disconnect**: Discards the data packet matching the packet filtering attributes and disconnects the TCP connection.
 >   - **Discard, disconnect, and block the source IP**: Discards the data packet matching the packet filtering attributes, disconnects the TCP connection, and temporarily blocks the source IP.
 >   - **Directly forward**: Directly forwards the data packets matching the packet filtering attributes.

-  **Speed Limit**
Click **Add**, select the protocol to limit the speed, and then set the limit threshold. The speed of ICMP, TCP, UDP and other protocols can be limited.
- **Block traffic from outside China**
  Select to enable or disable it. The protection engine of Anti-DDoS Pro is embedded with an IP library containing IPs from outside Mainland China. If you enable this function, source IPs in the library will be blocked. The **Enable** operation takes effect when attacks occur. The **Disable** operation takes effect immediately.

![Block traffic from outside China](https://main.qcloudimg.com/raw/5ec4afd4449365ea63cb4b0a4272f331.png)
-  **Connection Flood Protection**
 - **Null Session Protection**: Select to enable or disable it. The **Enable** operation takes effect when attacks occur. This function is implemented based on TCP proxy and may influence the initial business access.
 - **Source New Connection Limit**: Select to enable or disable it. After selecting **Enable**, you need to set the rate threshold (unit: connection/sec). The range is 0-∞. It specifies the number of new connections established by a source IP per second. New connections exceeding the upper limit will be discarded.
 - **Source Concurrent Connection Limit**: Select to enable or disable it. After selecting **Enable**, you need to set the threshold of connection. The range is 0-∞. It specifies the max allowed number of concurrent connections of a source IP. Concurrent connections exceeding the upper limit will be discarded.
 - **Destination New Connection Limit**: Select to enable or disable it. After selecting **Enable**, you need to set the rate threshold (unit: connection/sec). The range is 0-∞. It specifies the maximum number of new connections established by a destination IP per second. New connections exceeding the upper limit will be discarded. Due to clusterize deployment of the protection devices, deviation exists for the speed limit of new connections.
 - **Destination Concurrent Connection Limit**: Select to enable or disable it. After selecting **Enable**, you need to set the restraint number (unit: connection). The range is 0-∞. It specifies the maximum number of concurrent connections of a destination IP. Concurrent connections exceeding the upper limit will be discarded. Due to cluster-based deployment of the protection devices, deviation exists for the speed limit of concurrent connections.
- **Exceptional Connection Detection**
 -  **Max Exceptional Source IP Connections**: Click **Enable** and enter the maximum number of exceptional source IP connections. The range is 0-∞ (unit: connection). It specifies the max number of exceptional connections allowed for a source IP. If the number exceeds the threshold, the source IP will be identified as exceptional and will be blocked for a while.
 >The following parameters can be configured only when **Maximum Number of Exceptional Source IP Connections** is enabled.
 -  **Syn Packet Ratio Detection**: Select to enable or disable it. After selecting **Enable**, you need to set the Syn packet ratio. The range is 0-100. It specifies the threshold ratio of Syn packets and Ack packets for a TCP connection to be identified as exceptional.
 -  **Syn Packet Number Detection**: Select to enable or disable it. After selecting **Enable**, you need to set the maximum number of packets. The range is 0-65535, it specifies the threshold number of Syn packets for a TCP connection to be identified as exceptional.
 -  **Connection Timeout Detection**: Select to enable or disable it. After selecting **Enable**, you need to set the detection cycle (unit: second). The range is 0-65535. Specifies the threshold period during which no packets are transmitted for an established TCP connection to be identified as exceptional.
 -  **Exceptional Null Session Detection**: Select to enable or disable it. It specifies the threshold period during which no packets with loads are transmitted for an established TCP connection to be identified as exceptional.




- **Watermark Protection**
Click **Enable** to configure watermark protection. Enter a specified TCP protection port and UDP protection port, and then click **OK** to make the watermark protection take effect. Adding a DDoS advanced protection policy will automatically generate a key. You need to add the watermark configuration to the client offline.
![](https://main.qcloudimg.com/raw/cddc22b44a5eb2fb61e5cb84fadee5bc.png)

- **TCP Protection Port and UDP Protection Port**
A TCP/UDP protection port can be configured with a maximum of 5 ports or port segments. Different port segments cannot overlap each other. An entry with the same starting port and ending port is consider to be one port. At least one of the TCP or UDP port segments should be configured.

## Binding and Unbinding Resources

Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **DDoS Advanced Protection Policy** tab, click **Bind Resource** next to the target policy.

- Bind Resource: In the displayed **Bind Resource** dialog box, select one or more resources as required and click **OK**.
- Unbind Resource: In the displayed **Unbind Resource** dialog box, click **X** next to the selected resource in the **Selected** area as required and click **OK**.
![Unbind Resource](https://main.qcloudimg.com/raw/f103ba60c94ffe4fe276e221272a3aab.png)

##  **Adding Watermarks to the Client**
Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **DDoS Advanced Protection Policy** tab, click **Download Watermark Client File** next to the target policy to add the watermark to the client offline.

## **Adding, Deleting, or Disabling/Enabling a Watermark Key**
Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **DDoS Advanced Protection Policy** tab, click **Watermark Key Configuration** next to the target policy.
 - **Add Key**: In the displayed **Key Information** dialog box, click **Add Key** to generate a key.
 - **Disable/Enable Key**: Disables or enables a key. In the displayed **Key Information** dialog box, click **Disable** next to the target key. If you need to enable the key again, click **Enable**.
 - **Delete Key**: Deletes a disabled key. In the displayed **Key Information** dialog box, click **Delete** next to the target key.
>At most 2 keys can exist at one time. If you need to add a key, please delete an existing one. If only one key is activated, you cannot disable or delete the key.

![Key](https://main.qcloudimg.com/raw/dc5eca147e864542c88884eeb0172cdf.png)

## Configuring a Policy

Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **DDoS Advanced Protection Policy** tab, click **Configuration** next to the target policy. Update the following parameters as required, and then click **OK**.
>You cannot modify a policy name in the **scenario_policy_No.** format.
>
- Policy Name
- Blacklist/Whitelist
- Restricted Protocols
- Restricted Ports
- Packet Filtering Attributes
- Block Traffic from Outside China
- Connection Flood Protection
- Exceptional Connection Detection
- Watermark Protection

## Deleting a Policy

>- You can directly delete a policy without resources. To delete a policy with resources, unbind the resources and then delete it. A deleted policy cannot be recovered.
>- **You cannot delete an advanced protection policy automatically generated according to your scenarios.**

Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **DDoS Advanced Protection Policy** tab, click **Delete** next to the target policy. In the displayed dialog box, click **OK**.
![](https://main.qcloudimg.com/raw/478391dfb33cb9b1ea92c0def4544c76.png)
