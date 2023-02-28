<dx-tabs>
::: VPN Gateway

[](id:01)
### Why am I unable to delete a VPN gateway?
You can delete a VPN gateway only after you delete the VPN tunnel resources that are associated with the VPN gateway. For more information, see [Deleting SSL VPN Gateways](https://intl.cloud.tencent.com/document/product/1037/43912).

[](id:02)
### What does a 50 Mbps bandwidth cap mean?
A bandwidth cap for a VPN gateway is the maximum outbound bandwidth from the VPN gateway to the Internet.

[](id:03)
### Why is the data upload speed only 2 Mbps while the gateway bandwidth is 50 Mbps?
The data upload speed also varies based on your Internet access speed, in addition to the bandwidth specification that you purchased.

[](id:04)
## Can I change an IPsec VPN gateway to an SSL VPN gateway?
No, you cannot change the VPN gateway type.

[](id:05)
### Does a VPN gateway support bandwidth configuration adjustment?
Currently, you can adjust the bandwidth configuration only within some specifications, such as [20 Mbps, 100 Mbps] and [200 Mbps, 1000 Mbps]. For example, you can increase the bandwidth cap from 50 Mbps to 100 Mbps. If you want to increase the bandwidth cap from 100 Mbps to 200 Mbps, you must create a gateway that supports a bandwidth specification of 200 Mbps.

[](id:06)
### How do I check the traffic details of a gateway?
You can enable gateway traffic control. For more information, see [Enabling Gateway Traffic Monitoring](https://intl.cloud.tencent.com/document/product/1037/32702).



[](id:07)
### Why does the monitoring data displayed on the VPN gateway and VPN tunnel sometimes differ?
Currently, VPN gateway and VPN tunnel collect data at a different interval. The statistical granularity of the VPN gateway is 1 minute, and that of the VPN tunnel is 10 seconds. Therefore, the statistical data shown on the monitoring page of the VPN gateway may be different from that of the VPN tunnel.

[](id:08)
### How does a VPN gateway work? How about its availability?
A VPN gateway uses network functions virtualization (NFV) and an active-active hot backup mechanism. When one server fails, automatic switchover helps ensure the normal operation of your business.
A VPN tunnel runs in the public network. Therefore, congestion, jitter, or delay in the public network may affect the VPN network. If your business is sensitive to delay and jitter, we recommend using the [Direct Connect](https://www.tencentcloud.com/document/product/216).

[](id:09)
### How can I query the VPN gateway details?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to query the VPN gateway details as instructed in [Viewing IPSec VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/32700).




:::
::: VPN Tunnel
[](id:10)
### Why am I unable to ping a VPN tunnel that is in the connected state?
If the tunnel is in a normal status yet the private network cannot be connected, the possible causes are as follows:
- No routes directing to the private IP range in the IDC are added in the route table of the VPC subnet.
- The security policy on the VPC/IDC side does not allow access to the corresponding source and destination IPs.
- No tunnels directing to the private IP range in the IDC are added to the VPN gateway (route-based gateway).
- The firewall of the operating system of the private network server on the VPC/IDC side does not allow the IP addresses in the customer IP range to pass.
- The SPD policy on the VPC/IDC side does not contain the source and destination IPs.
- No routing policies are configured on the VPN gateway.

For more information, see [VPN Tunnel Connected Yet Private Network Unconnected](https://intl.cloud.tencent.com/document/product/1037/39782).

[](id:11)
### Why is a VPN tunnel in the unconnected state?
The possible causes are as follows:
- No traffic exists to activate the tunnel.
- The public IP address of the VPN gateway is not connected.
- The security policy is not correctly configured.
- Inconsistent negotiation parameters and modes exist.

For more information, see [VPN Tunnel Unconnected](https://intl.cloud.tencent.com/document/product/1037/39781).


[](id:13)
### Why does my gateway suddenly fail when it is in use?
The possible causes are as follows:
- The public IP address that you access is under Internet censorship and is blocked due to regulation compliance.
- You have modified the local settings, such as the protocol, or new protocol parameters are automatically enabled during local upgrade but the parameters are not configured on Tencent Cloud.
- Access to Tencent Cloud is prohibited by the local firewall.
- Negotiation parameter values, such as SA lifetime, are inconsistent.
- The VPN tunnel is deleted.

[](id:14)
### Why do I need to configure an SPD policy?
An SPD policy specifies the IP ranges in the network in which the VPN gateway resides and the IP ranges in the IDC that can communicate with each other.
>? The IP ranges specified in an SPD policy must not overlap with those specified in another SPD policy of the same VPN gateway.
>

[](id:15)
### How can I configure health check?
1. Ensure that the customer gateway is a routing gateway.
2. Configure health check in the Tencent Cloud console. For more information, see [Configuring Health Checks](https://intl.cloud.tencent.com/document/product/1037/46006).
>?
>- Create primary and secondary VPN tunnels before you configure health check, to avoid impacts on your business. We recommend that you do not configure health check without primary and secondary VPN tunnels.
>- Ensure that the IP addresses of the VPN gateway and the customer gateway do not conflict. If the two IP addresses belong to the same IP range, there is no need to configure a separate route to specify the customer gateway.
>
3. Configure the VPN gateway route and set its priority.

[](id:16)
### Why is the tunnel in the "unhealthy" status?
The ping test of IP that you configured for health check failed. Please check the configuration.




[](id:17)
### Do VPNs support the aggresive mode?
No.

[](id:18)
### How do I configure an SPD policy? Can I enter any peer IP range?
An SPD policy specifies the IP ranges in the network in which the VPN gateway resides and the IP ranges in the IDC that can communicate with each other. A peer IP range is a subset of accessible public IP ranges and cannot overlap with the IP ranges that are specified in other SPD policies of the same VPN gateway.





[](id:21)
### Do the local and peer IP ranges in an SPD policy for an SPD policy-based VPN tunnel need to follow specific sequence requirements?
No sequence requirements are imposed for the local and peer IP ranges in an SPD policy.

[](id:22)
### How can I modify the VPN tunnel configuration?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to modify the VPN tunnel configuration as instructed in [Modifying VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32701).


[](id:23)
### How can I create a VPN tunnel?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to create a VPN gateway as instructed in [Step 3: Create a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32692).

[](id:24)
### What are the mappings between the local and peer IP ranges in an SPD policy?
For more information, see SPD policy in [Creating a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/39635).
:::
</dx-tabs>

