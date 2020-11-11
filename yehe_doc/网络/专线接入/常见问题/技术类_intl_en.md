### Does Direct Connect support 802.1Q VLAN encapsulation?

Yes.

### How do I use the line of a connection provider?

The connection provider should first build a NNI connection with the Direct Connect access point. To do this, the connection provider needs to apply for a connection in the Tencent Cloud [Direct Connect console](https://console.cloud.tencent.com/dc/dc). Then Tencent Cloud delivery engineer will assist the line access and NNI connection. The provider will have a connection ID in the `dc-*******` format under the Tencent Cloud account.
Once connected, you can use the connection in the following two methods:

- Shared connections
  1. Obtain the Tencent Cloud account ID, a connection ID (`dc-*******`), a unique VLAN ID, and an interconnection IP address from the connection provider.
  2. Log in to the [Dedicated Tunnels console](https://console.cloud.tencent.com/dc/dcConn) and click **+New** to create a dedicated tunnel. In the **Basic Configuration** tab, select **Shared Connections** for **Connection Type**, and fill in **Provider Account ID** and **Shared Connection ID**. In the **Advanced Configuration** tab, enter the **VLAN ID**, complete the other configurations , and click **Submit**.
  3. Request the connection provider to log in to the [Dedicated Tunnels console](https://console.cloud.tencent.com/dc/dcConn) and click **Accept** on the right of the dedicated tunnel you apply for.
  4. Tencent Cloud will create the tunnel automatically in a few minutes.
- Hosted connections (to be launched soon):
  1. The connection provider needs to log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc), and click the name/ID of the connection for which a bandwidth will be assigned. Select the **Assign Hosted Connection** tab, enter your account ID, VLAN, bandwidth, and interconnection IP address to assign the specified bandwidth to you.
  2. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and select **Connections** to access the connection list. Locate the assigned connection, verify information, and click **Accept**.
  3. Tencent Cloud will create the tunnel automatically in a few minutes.
>! In this process, Tencent Cloud only creates a tunnel to connect network both in and off the cloud after receiving the creation request. Tencent Cloud will not review the information.

### How do I choose a connection port type?

Please confirm with your connection provider. The fiber optic port component supports long- and short- distance transmissions. Make sure that you have selected the correct port type before submitting the connection application in the Tencent Cloud console.

### How do I obtain technical support from Tencent Cloud Direct Connect engineers?

Log in to the Tencent Cloud [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **+New** to complete the information and submit the application. Then Tencent Cloud Direct Connect delivery engineer will contact you within 3 business days and suggest you on the Direct Connect service.

### How do I obtain the location of the Direct Connect access points?

Log in to the Tencent Cloud [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **+New** to complete the information and submit the application. Then Tencent Cloud Direct Connect delivery engineer will contact you within 3 business days and help you with the Direct Connect service.

## Does the dedicated tunnel support the active-active or active-standby mode among connections?

Yes. Situations include:

- Traditional dedicated tunnels:
  - BGP route:
    - Active-active: regardless of whether the connections are connected to the same Direct Connect access point, traffic sent from the cloud to the local IDC will be balanced in an active-active mode, as long as the local IDC distributes the equal-cost multi-path (ECMP) routes to the same direct connect gateway.
    - Active-standby: regardless of whether the connections are connected to the same Direct Connect access point, users need to configure AS paths of different lengths for the standby connections on their customer-premises equipment (CPE) so that traffic can be balanced in an active-standby mode.
  - Static route:
    - Active-active: regardless of whether the connections are connected to the same Direct Connect access point, traffic sent from the cloud to the local IDC will be balanced in an active-active mode as long as the ECMP route is configured on the dedicated tunnel of connections.
    - Active-standby: only connections to different Direct Connect access points can be configured in an active-standby mode. This mode is not available to connections to the same Direct Connect access point.
- Cloud Connect Network (CCN) dedicated tunnel (the active-standby and active-active features will be launched soon):
  The active-standby and active-active relationships are defined by route priorities in the CCN. You only need to set route priorities in the CCN and configure health check to trigger the route switching.

### Where is the interconnection IP address actually configured?

The interconnection IP address is configured on both sides of the connection: the device of the Direct Connect access point and the CPE of users.

### How do I use one VLAN connection to access multiple Tencent Cloud VPCs?

Add these VPCs to a [CCN](https://intl.cloud.tencent.com/product/ccn).

## How does Tencent Cloud isolate tenants to ensure data security?

Tencent Cloud applies MPLS_VPN to the private network, with the Direct Connect access point serving as the provider edge (PE) of MPLS. The virtual routing and forwarding (VRF) technology is used in the VPC to isolate connections to cloud services and protect user data.

### How is switchover between redundant connections triggered?
  - For static routes, configure bidirectional forwarding detection (BFD) to achieve route convergence.
  - For BGP routes, switchover is triggered by the BGP convergence mechanism or a BFD configuration. Contact your Direct Connect delivery engineer to configure BFD for you.
The IP SLA cannot be configured, because this may degrade the performance of the access point device and restrict user access considering the large number of connections to the access point.

### Does Tencent Cloud support the link aggregation control protocol (LACP)?

No. This feature is currently not supported.

### Why does the connection performance test result fall short of expectations?

Double check the connection bandwidth you purchased.
Ping the interconnection IP address to check for packet loss and troubleshoot with Tencent Cloud after-sales team in case of serious packet loss. For a self-built connection, you need to also report the problem to the carrier.
Check whether your local router uses the full-duplex mode.
Use iperf or other tools to start multiple processes from both clients and CVMs for the traffic stress test. Troubleshoot application problems based on the test results.
If needed, contact Tencent Cloud after-sales team for assistance.

### What should I do if the connection to Tencent Cloud is interrupted?

- Confirm that the connection is interrupted:
  Unable to ping the interconnection IP address or receive the MAC address of the CVM instance. Tencent Cloud after-sales team receives an alarm indicating the connection exception.
After confirmation:
   - For a Tencent Cloud connection, report the failure to Tencent Cloud after-sales team as soon as possible. Generally, the after-sales team will report the connection failure to the carrier immediately after receiving the alarm.
   - For a self-built connection, report the failure to the carrier. Contact the Tencent Cloud after-sales team for assistance if needed.

### What can I do if a specific IP range of the connection fails to be pinged?

- Check whether the IP range is new, and configure routes for the new IP range in the VPC.
- Confirm that the route table for the VPC subnets is configured with different IP ranges pointing to the direct connect gateway, and that the client server has a route pointing to the connection.
- Check the security features: the CVM instance has associated with security groups or network ACLs, and the client server has configured iptables.
- If no problem is found, provide the after-sales team with troubleshooting information for subsequent operations.

### What information do I need to provide the customer service for the troubleshooting?

To request a troubleshooting, provide the following information:

- A description of the problem and whether the problem can be reproduced.
- The source IP address and the destination IP address.
- The location of the connection.
- Direct connect gateway ID.
- Screenshots of ping and traceroute commands.
- The iptables and NAT information.
- The access topology.
