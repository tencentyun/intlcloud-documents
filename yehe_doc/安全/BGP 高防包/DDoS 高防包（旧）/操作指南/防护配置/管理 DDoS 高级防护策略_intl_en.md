Anti-DDoS Pro provides advanced protection policies against DDoS attacks. You can adjust and optimize the DDoS protection policy as required through blocklists/allowlists, disabling protocols and ports, packet characteristic filtering, connection flood protection, and watermark protection.

## Configuration Item Overview
<style>
table th:first-of-type {
    width: 150px;
}
</style>
| Configuration Item       | Description                                                     | Effective Time                                 |
| ------------ | ------------------------------------------------------------ | ---------------------------------------- |
| Blocklist/Allowlist     | It is IP-based protection.<br/><ul><li>It always allows requests from IPs in the allowlist. </li><li>It always blocks requests from IPs in the blocklist.</li></ul> | It takes effect immediately when the protected IPs are under attack.                  |
| Disabled protocol     | It disables a protocol not used by the business.<br/>If attacks are detected, the Anti-DDoS Pro cluster will cleanse the traffic under the protocol. | It takes effect immediately when the protected IPs are under attack.            |
| Disabled port     | It disables a port not used by the business.<br/>If attacks are detected, the Anti-DDoS Pro cluster will cleanse traffic from the disabled ports. | It takes effect immediately when the protected IPs are under attack.    |
| Packet filter characteristic | It combines multiple criteria to set policy operations, such as the protocol, port range, packet range, whether to detect load, offset, detection depth, and whether to include characteristic strings based on the business or attack packets.<br/>If the packets match the policy criteria, operations such as direct forwarding, discarding, source IP blocking, or disconnecting can be executed. | It takes effect immediately when the protected IPs are under attack.                |
| Speed limit | It is IP-based protection and limits the speed of the access protocol. | It takes effect immediately when the protected IPs are under attack. |
| Reject traffic from outside China | It rejects TCP traffic requests from outside China (including Mainland China, Hong Kong, Macao, and Taiwan).      | It takes effect when the protected IPs are under attack. |
| Null session protection   | It protects against null session attacks.                                             | It takes effect when the protected IPs are under attack. |
| Connection flood protection | It is IP-based protection, which limits the speed, packet length, and other parameters of connections accessing the IPs protected by Anti-DDoS Pro to protect against light traffic connection attacks. | It takes effect immediately when the protected IPs are under attack. |
| Exceptional connection detection | When a source IP receives a TCP connection meeting the configured parameter characteristics, the connection will be regarded as exceptional. If the amount of exceptional connections received by the source IP exceeds the maximum allowable number, the IP will be added to the blocklist for a certain period and will not be accessible. | It takes effect immediately when the protected IPs are under attack. |
| Watermark protection   | It supports UDP and TCP packets. Watermark detection and stripping will be executed for the payloads within the configured port range. Watermark protection can protect against layer-4 CC attacks, such as forged business packet attacks and replay attacks.<br/><ul><li>Customer client and Tencent Cloud Anti-DDoS Pro system share the same watermark algorithm and key.<br/></li><li>Each packet sent by the client is embedded with watermark characteristic which attack packets do not have.<br/></li><li>The Anti-DDoS Pro system will identify and discard attack packets.                                             | It takes effect immediately when the protected IPs are under attack. |

## Adding Policies

> Configuration of advanced protection policy requires technical expertise. You are recommended to read the operation guide before configuring policies as needed.

Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Pro** > **Protection Configuration**. On the **Advanced DDoS Protection Policy** tab, click **Add Policy**. Configure the following parameters as needed and click **OK**.

**Policy Name**
Enter a policy name containing 1–32 characters of any type.

- **Blocklist/Allowlist**
 - If you need to set a blocklist, click **Add**, select **Blocklist**, enter IPs to block, and then click **OK**. Separate multiple IPs with carriage returns.
 - If you need to set a allowlist, click **Add**, select **Allowlist**, enter the IP to allow directly, and then click **OK**. Separate multiple IPs with carriage returns.
>You can add up to 100 IPs for the blocklist and allowlist. The number of IPs to be added in batches cannot exceed the current available quota.

- **Disabled Protocol**
  Select the protocol you want to disable.
- **Disabled Port**
  Select a protocol and port type, and then enter the ports to be disabled. If you only need to disable one port in an entry, enter the same number for the starting and ending ports. Click **Add** under the list to add more entries. Protocols include TCP and UDP. Port types include destination port, source port, and destination/source port.
- **Packet Filter Characteristic**
  Set conditions such as the protocol, port range, packet length, payload detection, offset, detection depth, and characteristic strings and configure the action to be taken for immediate effect.

 >
 >
 > - Offset: specifies the start position of the matched characteristics in the packet.
 >- Detection depth: specifies the packet length from the position set by the offset to the end of the matching content. It is used with the offset.
 > - Policy:
 >   - "Discard packet": discards the data packet matching the packet filter characteristic.
 >   - "Discard packet and block source IP": discards the data packet matching the packet filter characteristics and temporarily blocks the source IP.
 >   - "Discard packet and disconnect": discards the data packet matching the packet filter characteristics and closes the TCP connection.
 >   - **Discard packet, disconnect, and block source IP**: discards the data packet matching the packet filter characteristics, closes the TCP connection, and temporarily blocks the source IP.
 >   - **Directly forward**: directly forwards the data packets matching the packet filter characteristics.

-  **Speed Limit**
Click **Add**, select the protocol for speed limit, and then set the limit threshold. The speed of ICMP, TCP, UDP, and other protocols can be limited.
- **Reject Traffic from Outside China**
  Select "Enable" or "Disable". The protection engine of Anti-DDoS Pro is embedded with an IP library containing IPs from outside China. If you enable this feature, source IPs in the library will be rejected. The **Enable** operation takes effect when attacks occur. The **Disable** operation takes effect immediately.

-  **Connection Flood Protection**
 - **Null Session Protection**: select "Enable" or "Disable". The **Enable** operation takes effect when attacks occur. This feature is implemented based on TCP proxy and may affect the initial business access.
 - **Source New Connection Limit**: select "Enable" or "Disable". After selecting **Enable**, you need to set the rate threshold (unit: connection/sec) in the range of 0–∞. It specifies the number of new connections established by a source IP per second. New connections exceeding the upper limit will be discarded.
 - **Source Concurrent Connection Limit**: select "Enable" or "Disable". After selecting **Enable**, you need to set the quantity threshold in the range of 0–∞. It specifies the maximum allowed number of concurrent connections of a source IP. Concurrent connections exceeding the upper limit will be discarded.
 - **Destination New Connection Limit**: select "Enable" or "Disable". After selecting **Enable**, you need to set the rate threshold (unit: connection/sec) in the range of 0–∞. It specifies the maximum number of new connections established by a destination IP per second. New connections exceeding the upper limit will be discarded. Due to cluster-based deployment of the protection devices, deviation exists for the speed limit of new connections.
 - **Destination Concurrent Connection Limit**: select "Enable" or "Disable". After selecting **Enable**, you need to set the quantity threshold in the range of 0–∞. It specifies the maximum number of concurrent connections of a destination IP. Concurrent connections exceeding the upper limit will be discarded. Due to cluster-based deployment of the protection devices, deviation exists for the speed limit of concurrent connections.
- **Exceptional Connection Detection**
 -  **Maximum Exceptional Source IP Connections**: click **Enable** and enter the maximum allowed number of exceptional source IP connections in the range of 0–∞. It specifies the maximum number of exceptional connections allowed for a source IP. If the number exceeds the threshold, the source IP will be identified as exceptional and will be blocked for a while.
 >The following parameters can be configured only if **Maximum Number of Exceptional Source IP Connections** is enabled.
 -  **Syn Packet Ratio Detection**: select "Enable" or "Disable". After selecting **Enable**, you need to set the Syn packet ratio in the range of 0–100. It specifies the threshold ratio of Syn packets and Ack packets for a TCP connection to be identified as exceptional.
 -  **Syn Packet Number Detection**: select "Enable" or "Disable". After selecting **Enable**, you need to set the maximum allowed number of packets in the range of 0–65535. It specifies the threshold number of Syn packets for a TCP connection to be identified as exceptional.
 -  **Connection Timeout Detection**: select "Enable" or "Disable". After selecting **Enable**, you need to set the detection cycle (unit: second) in the range of 0–65535. It specifies the threshold period during which no packets are transmitted for an established TCP connection to be identified as exceptional.
 -  **Exceptional Null Session Detection**: select "Enable" or "Disable". It specifies that an established TCP connection will be identified as exceptional if it has no packets with payload.




- **Watermark Protection**
Click **Enable** to configure watermark protection. Enter a specified TCP protection port and UDP protection port, and then click **OK** to make the watermark protection take effect. Adding an advanced DDoS protection policy will automatically generate a key. You need to add the watermark configuration to the client offline.

- **TCP Protection Port and UDP Protection Port**
A TCP/UDP protection port can be configured with up to 5 port ranges. Different port ranges cannot overlap one another. If the starting and ending port numbers are the same, a range will be considered as one port. You need to configure at least one of the TCP or UDP port ranges.

## Binding and Unbinding Resources

Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Pro** > **Protection Configuration**. On the **Advanced DDoS Protection Policy** tab, click **Bind Resource** next to the target policy.

- Bind Resource: in the pop-up **Bind Resource** dialog box, select one or more resources as needed and click **OK**.
- Unbind Resource: in the pop-up **Bind Resource** dialog box, click <img src="https://main.qcloudimg.com/raw/f452deeefbca4c66f34b7db71ec0daca.png"  style="margin:0;"> to the right of a resource in the **Selected** section and click **OK**.

## **Adding Watermark to Client**
Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Pro** > **Protection Configuration**. On the **Advanced DDoS Protection Policy** tab, click **Download Client Watermark File** next to the target policy to add the watermark to the client offline.

## **Adding, Deleting, or Disabling/Enabling a Watermark Key**
Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Pro** > **Protection Configuration**. On the **Advanced DDoS Protection Policy** tab, click **Watermark Key Configuration** next to the target policy.
 - **Add Key**: in the pop-up **Key Information** dialog box, click **Add Key** to generate a key.
 - **Disable/Enable Key**: you can disable or enable a key. In the pop-up **Key Information** dialog box, click **Disable** next to the target key. If you need to enable it again, click **Enable**.
 - **Delete Key**: you can delete a disabled key. In the pop-up **Key Information** dialog box, click **Delete** next to the target key.
>At most 2 keys can exist at one time. If you need to add more keys, please delete an existing one first. If only one key is activated, you cannot disable or delete it.

## Configuring a Policy

Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Pro** > **Protection Configuration**. On the **Advanced DDoS Protection Policy** tab, click **Configuration** next to the target policy. Update the following parameters as required, and then click **OK**.
>You cannot modify a policy name in the "scenario name_policy_No." format.
>
- Policy Name
- Blocklist/Allowlist
- Disabled Protocol
- Disabled Port
- Packet Filter Characteristic
- Reject Traffic from Outside china
- Connection Flood Protection
- Exceptional Connection Detection
- Watermark Protection

## Deleting a Policy

>
- You can directly delete a policy without bound resources. To delete a policy with bound resources, unbind the resources first. A deleted policy cannot be recovered.
- **You cannot delete an advanced protection policy automatically generated for your created scenario.**

Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Pro** > **Protection Configuration**. On the **Advanced DDoS Protection Policy** tab, click **Delete** next to the target policy. In the pop-up dialog box, click **OK**.
