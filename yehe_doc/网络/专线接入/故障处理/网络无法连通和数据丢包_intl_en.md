## Error Description
Your business is unable to connect to the network and encounters packet loss, resulting in exceptions.

## Possible Reasons
The reasons are as follows:
-[Connection interruption](#1): the connection is damaged. For example, the cable is cut off.
-[Bandwidth exhaustion](#2): the dedicated tunnel’s bandwidth is insufficient to meet business requirements.
-[Security policy misconfiguration](#3): the IDC route to and from VPC is different
- [Static route failure](#4): the static route has no Bidirectional Forwarding Detection (BFD) configured, which causes business access exception.
- [BGP route failure](#5): the BGP routes exceed the limit.
- [IP address conflict](#6): the local IP address is overlapped with VPC IP.

## Solutions

<span id="1"></span>
### Connection interruption
**A connection to one access point**
Your IDC connects to one Tencent Cloud access point using a connection, and then accesses Tencent Cloud VPCs. The disconnection will directly cause business interruption.
![](https://main.qcloudimg.com/raw/59177b6fa264d350d948562a90d39309.png)
**Solution**
Report the failure to the carrier and provide the connection ID. This mode is incapable of disaster recovery. We recommend that you plan connections to improve the stability and high availability of the Direct Connect network architecture. For more information, see [Network Planning](https://intl.cloud.tencent.com/document/product/216/38527).

**Two connections to one access point
Your IDC connects to one Tencent Cloud access point using two connections, and then accesses Tencent Cloud VPCs. When one connection interrupts, disaster recovery starts.
![](https://main.qcloudimg.com/raw/424b684e55ad9f2eb059143f4682bea7.png)
**Solution**
1. Check for business damage on your business monitoring system.
2. Collect the access latency and route change caused by traffic switch after disaster recovery, and judge whether the secondary connection works.
3. If the secondary connection fails to work, locate faults based on information collected from the ping and traceroute tests.

<span id="2"></span>
### Bandwidth exhaustion
**A connection to one access point**
Your IDC connects to one Tencent Cloud access point using a connection, and then accesses Tencent Cloud VPCs. When the dedicated tunnel bandwidth is used up, packet will be lost, resulting in data loss.
![](https://main.qcloudimg.com/raw/a4bd7f183a041965747422863e9eeb2e.png)
**Solution**
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/dc) console and go to the **Dedicated Tunnels** page. Locate the dedicated tunnel and adjust its bandwidth on the **Change Tunnel** page as instructed in [Changing Tunnel](https://intl.cloud.tencent.com/document/product/216/19251).
2. If the connection bandwidth cap is reached, first perform the disaster recovery switchover for your business and contact the Direct Connect representative for expansion.
3. Analyze the causes of bandwidth exhaustion while prioritizing the business recovery.

**Two connections to two access points**
Your IDC connects to two intra-region Tencent Cloud access points using one connection respectively, and then accesses Tencent Cloud VPCs.
- Primary/secondary mode
When the primary connection bandwidth is used up, packet will be lost, resulting in data loss. Change to the load-balancing mode to share traffic and resume service data.
![](https://main.qcloudimg.com/raw/cc8afa125dc11d04fa52513e34520069.png)
- Load-balancing mode
When both connections are full-loaded, packet will be lost, resulting in data loss.
  ![](https://main.qcloudimg.com/raw/51eca2bb50730177abda0f509323f56c.png)
**Solution**
 1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/dc) console and go to the **Dedicated Tunnels** page. Locate the dedicated tunnel and adjust its bandwidth on the **Change Tunnel** page as instructed in [Changing Tunnel](https://intl.cloud.tencent.com/document/product/216/19251).
 2. If your connection bandwidth cap is reached:
   - Primary/secondary mode: change to the load-balancing mode to share traffic and resume service data.
   - Load-balancing mode: first perform disaster recovery switchover for your business and contact the Direct Connect representative for expansion.
 3. Analyze the causes of bandwidth exhaustion while prioritizing the business recovery.

<span id="3"></span>
### Security policy misconfiguration
Your IDC connects to two intra-region Tencent Cloud access points using one connection respectively, and then accesses Tencent Cloud VPCs. If your IDC accesses Tencent Cloud VPC via the primary connection and is accessed by Tencent Cloud VPC via the secondary connection, different routes will cause inaccessibility.
![](https://main.qcloudimg.com/raw/8f0e2af4639de6d2db4d1ecfeffd4586.png)
**Solution**
1. Check whether different security devices (such as firewall) are configured on the primary and secondary connections. If so, ensure that their security policies are the same and allow incoming and outgoing messages to pass.
2. Configure an IDC IP (an idle IP or test IP as confirmed by the owner) on IDC access devices, and use this IP to access the in-cloud business IP to test communication.
3. If the problem persists, troubleshoot the issue inside your IDC.

<span id="4"></span>
### Static route failures
Your IDC connects to two intra-region Tencent Cloud access points using one connection respectively, and then accesses Tencent Cloud VPCs.
If the primary connection cascades a layer-3 device, the IDC server port exception or abnormal link from the layer-3 device to IDC is imperceptible to the access point A, and no alarm will be triggered. In this case, the dedicated tunnel still sends static route to the direct connect gateway and forward traffic to the faulty connection, causing service suspension.
![](https://main.qcloudimg.com/raw/50f64c39bd2646138024a88faa99db26.png)
**Solution**
We recommend that configure BFD on access devices at IDC and access point for the static route to periodically send a detection packet. If there is no reply within a specified period, the opposite end is determined to be faulty and the associated route will become invalid without forwarding to the direct connect gateway.

Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable the BFD feature of the dedicated tunnel and the configuration will be provided.
 > ? The default Tencent Cloud BFD is dynamic BFD. The local TX Interval is equal to VPC’s Desired Min TX Interval or IDC’s Required Min RX Interval, whichever is larger.
 >- For 1.0 dedicated tunnel:
 >- If you applied for the dedicated tunnel before October 1, 2019, both Desired Min TX Interval and Required Min RX Interval are 100 ms, and Detect Mult is 3.
>- If you applied for the dedicated tunnel on or after October 1, 2019, both Desired Min TX Interval and Required Min RX Interval are 300 ms, and Detect Mult is 3.
>- For 2.0 dedicated tunnel:
>- The minimum values of both Desired Min TX Interval and Required Min RX Interval are 1000 ms, and Detect Mult is 3.
>  

<span id="5"></span>
### BGP route failures
Each dedicated tunnel supports up to 100 BGP routes. If this limit is exceeded, your business may fail.
**Solution**
Plan network addresses and merge CIDR block subnet to reduce IDC routes to Tencent Cloud VPC.

<span id="6"></span>
### IP address conflicts
Both VPC and IDC follow the TCP/IP protocol that has layer-3 addressing based on the destination IP and layer-2 addressing based on destination MAC. In a hybrid-cloud scenario, the overlap of the IDC and VPC address space may cause IP address conflicts and limit business access.
**Solution**
1. Implement a network planning.
	1. Plan Tencent Cloud VPC and IDC addresses uniformly.
	2. Plan IP and other interconnection addresses globally.
2. Use the NAT-type direct connect gateway to translate and mask the local VPC address and peer IDC address when the business scenario does not allow network splitting and re-planning. For detailed directions, see [Configuring the Network Address Translation (NAT)](https://intl.cloud.tencent.com/document/product/216/19257).
>? A NAT-type direct connect gateway supports up to 100 rules for local IP translation and peer IP translation each.
