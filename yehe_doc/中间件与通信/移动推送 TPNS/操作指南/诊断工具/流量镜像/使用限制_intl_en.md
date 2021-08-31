Take the following information into consideration and maintain your business intact when you use traffic mirror.
- Traffic mirror is now in beta test. To apply for it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). We recommend saving the link to the Traffic Mirror Console, so you can log in to the Console without applying again.
- Traffic mirror consumes CVM resources such as CPU, memory and bandwidth pro rata.
  Mirrored traffic counts toward instance bandwidth. The impact depends on the volume and type of traffic. For example, if you mirror a network interface that has 1 Gbps of inbound traffic and 1 Gbps of outbound traffic. In this case, the instance needs to handle 1 Gbps of inbound traffic and 3 Gbps of outbound traffic (1 Gbps for the outbound traffic, 1 Gbps for the mirrored inbound traffic and 1 Gbps for the mirrored outbound traffic).
- Flow logs do not capture mirrored traffic.
- Limits regarding a security group:
 - Source: the mirrored traffic is not subject to security group policies. 
 - Target: the received traffic is subject to security group policies.
- Traffic mirror is not available for:
 - Address resolution protocol
 - DHCP
 - Instance metadata service
 - NTP
 - Windows activation

