

Aegis Anti-DDoS provides a basic security policy by default, which can effectively cope with common DDoS attacks based on algorithms such as AI engine, IP profiling and behavior pattern analysis. It also provides advanced policies that can be customized based on business characteristics or attacking behaviors in case of certain special or masquerading attacks, which can achieve more targeted protection against specific attacks.

Advanced policies can be bound to protective IPs and IPs protected by protection packs. Based on your own needs, you can configure [Advanced security policies](https://intl.cloud.tencent.com/document/product/685/18807), [HTTP anti-CC defense policies](https://intl.cloud.tencent.com/document/product/685/18806) and [watermark protection](https://intl.cloud.tencent.com/document/product/685/18804). When an attacking behavior contained in the current business request is detected, the attack traffic will be cleansed according to the configuration of the advanced policy.

## Custom Advanced Security Policy
| Advanced security policy | Anti-CC defense policy |
|--|--|
| Protocol disabling | HTTP QPS request threshold |
| Port disabling | Blacklist/whitelist configuration (URL, IP) |
| IP blacklist/whitelist | Custom anti-CC defense |
| Message characteristic filtering | Match mode: blocking, human-machine verification |
| Overseas traffic disabling | Speed limit mode: source IP access speed |
| Null session protection |-|

## Advanced Security Policy

- Protocol or port disabling
You can disable protocols or ports that are not used by the business. When an attack is detected, the protection system will cleanse the traffic of the disabled protocols or ports.
- IP blacklist/whitelist configuring
Business traffic from IPs in the whitelist will not be detected for attacks or cleansed by the protection system, while traffic from IPs in the blacklist will be cleansed. Up to 50 IP addresses can be added to the IP blacklist/whitelist.
- Message characteristic filtering
You can configure a policy with message length or message length + payload as conditions for characteristics of business or attack messages. When the system detects that a message matches the policy condition, it can perform operations such as discarding, blacklisting the source IP or disconnecting.
- Null session protection
This addresses null session attacks. If null session protection is required for the IPs protected by protection packs, it can be enabled accordingly.
- Rejecting traffic from outside China
TCP traffic requests from outside China (Mainland China, Hong Kong (China), Macau (China) and Taiwan (China)) can be rejected.

**Case description:**
The following is a normal business message.
![1](https://main.qcloudimg.com/raw/c52a92b15c4c99d0a581462b40ca536b.png)

After analysis, its characteristics are as follows:
- The destination port is 80.
- The packet length is 1000 bytes or below.
- The payload starts with "GET" and carries a "Host" field.

You can configure a message characteristic filtering policy to block messages that don't meet the normal business characteristics.
Messages that meet the following conditions:
- The destination port is 80.
- The packet length is 1000 bytes or above.
- The payload doesn't start with "GET" and doesn't carry a "Host" field.

**Executed operation:**
If a message meets all the conditions above at the same time, it will be blocked.

![2](https://main.qcloudimg.com/raw/e47e7ffb5af1ce6c63dcd0e884776401.png)

## CC Protection Policy

- HTTP request threshold
CC protection is triggered when the number of HTTP requests exceeds the set QPS value.
- URL whitelist
The protection system doesn't perform CC attack detection and protection on whitelisted URLs.
- IP blacklist/whitelist
HTTP access requests from IPs in the whitelist will not be detected for CC attacks or prevented by the protection system, while those from IPs in the blacklist will be rejected. Up to 50 IP addresses can be added to the IP blacklist/whitelist.
- Custom anti-CC defense
This mainly blocks or requires human-machine verification for HTTP requests that have specific fields in the header.
 - Match mode: If an HTTP request with the specified field header is detected, it will be blocked or processed for human-machine verification.
 - Speed limit mode: The speed of access requests from the source IP will be limited. It supports configuring speed limit globally or for source IPs of specified URLs. After configured, when all the source IPs access the protective IP (or IP of a protection pack) bound to this policy, the access frequency will be controlled for speed limit by the configured value. If configured as 0, it is not enabled. A policy for speed limit for specified URLs has a higher priority than a global speed limit policy.


## Watermark Protection
- Protected IP
The business traffic accessing this IP and the specified port is detected for watermark, and the attack messages are discarded.
- TCP protection port and UDP protection port
A TCP/UDP protection port can be configured with up to five port ranges. Different port ranges cannot overlap one another. If the starting and ending port numbers are the same, a range will be considered as one port. You need to configure at least one of the TCP or UDP port ranges.
- UDP watermark stripping
Select "Automatically strip watermark from UDP message". After the data message passes through the security protection system, the watermark in a UDP message is automatically stripped and then transferred to the real server. You can also configure the offset (0-100) of the specified watermark tag in the UDP message. Note: If the protection system is not required to strip the UDP watermark, the server side needs to be modified for watermark stripping.
- Whitelist
Select "Enable source IP whitelist" to add an IP. Watermark detection is not performed for messages from the IPs in the whitelist.

You can efficiently and comprehensively protect against layer 4 CC attacks such as masquerading and replay attacks by accessing watermark protection.
- The watermark algorithm and key are shared between the business side and the Aegis protection system.
- A watermark is embedded in every message sent by the client, while the attack messages have no watermark.
- The protection system can easily identify and discard the attack messages.


