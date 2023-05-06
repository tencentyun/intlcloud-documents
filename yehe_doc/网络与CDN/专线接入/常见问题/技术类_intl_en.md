### Does Direct Connect support 802.1Q VLAN encapsulation?
Yes.

### How do I use the connection of a connection provider?
>? In the answer, an exclusive dedicated tunnel is taken as an example. The method also applies to a shared dedicated tunnel.
>
The connection provider should first build a network-to-network interface (NNI) connection with the Direct Connect access point. To do this, the connection provider needs to apply for a connection in the Tencent Cloud [Direct Connect console](https://console.cloud.tencent.com/dc/dc). Tencent Cloud delivery engineers will assist in the line access and NNI connection. The connection provider will obtain a connection ID in the `dc-*******` format under its Tencent Cloud account.
Then, you can use the connection in the following method:
Shared connection:
  1. Obtain information such as the Tencent Cloud account ID of the connection provider, the connection ID (`dc-*******`), a unique VLAN ID, and an interconnection IP address from the connection provider.
  2. Go to the [Exclusive virtual interface page](https://console.cloud.tencent.com/dc/dcConn) of the Direct Connect console and click **+ New** to create a dedicated tunnel. On the **Basic configuration** tab, select **Shared connections** for **Connections**, and enter the account ID of the connection provider and the ID of the connection. On the **Advanced configuration** tab, enter the VLAN ID, complete the other configurations, and click **Submit**.
  3. Request the connection provider to go to the [Exclusive virtual interface page](https://console.cloud.tencent.com/dc/dcConn) of the Direct Connect console and click **Accept** on the right of the dedicated tunnel that you apply for.
  4. Wait until the tunnel is created, which takes several minutes.


### How do I choose a connection port type?
You need to confirm with your connection provider. The fiber optic port component supports long- and short-distance transmission. Make sure that you have selected the correct port type before submitting the connection application in the Tencent Cloud console.
>?When you use a 100 Gbps port for the connection, enable or disable the Forward Error Correction (FEC) mode based on the specifications of your device:
>- If you use a 100 Gbps optical module that supports a transmission distance of 40 km (QSFP-100G-ER4L-WDM1300, 40 KM), the FEC mode is enabled for the device port on Tencent Cloud by default. In this case, you must enable the FEC mode on your device.
>- If you use a 100 Gbps optical module that supports a transmission distance of 10 km (QSFP-100G-LR4-WDM1300, 10 KM), the FEC mode is disabled for the device port on Tencent Cloud by default because the module that you use does not support the FEC mode. In this case, we recommend you disable the FEC mode on your device.
>



### How do I obtain technical support from Tencent Cloud Direct Connect engineers?
Log in to the Tencent Cloud [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **+ New**. Then, enter the required information and submit the application. A Tencent Cloud Direct Connect delivery engineer will contact you within three business days and help you with the Direct Connect service.



### How do I obtain the addresses of Direct Connect access points?
Log in to the Tencent Cloud [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **+ New**. Then, enter the required information and submit the application. A Tencent Cloud Direct Connect delivery engineer will contact you within three business days and help you with the Direct Connect service.



### Does Direct Connect support the active-active or active-standby mode for connections?
Yes. The supported modes vary based on the following conditions:
- Traditional dedicated tunnels:
  - Border Gateway Protocol (BGP) routing:
    - Active-active mode: Regardless of whether the connections are connected to the same Direct Connect access point, traffic sent from the cloud to the local IDC will be balanced in active-active mode, as long as the local IDC distributes the equal-cost multi-path (ECMP) routes to the same direct connect gateway.
    - Active-standby mode: Regardless of whether the connections are connected to the same Direct Connect access point, users need to configure AS paths of different lengths for the standby connections on their customer-premises equipment (CPE) so that traffic can be balanced in active-standby mode.
  - Static routing:
    - Active-active mode: Regardless of whether the connections are connected to the same Direct Connect access point, traffic sent from the cloud to the local IDC will be balanced in active-active mode as long as the ECMP route is configured on the dedicated tunnel of connections.
    - Active-standby mode: Only connections to different Direct Connect access points can be configured in active-standby mode. This mode is not available to connections to the same Direct Connect access point.
- Cloud Connect Network (CCN) dedicated tunnel (the active-standby and active-active features will be launched soon):
  The active-standby and active-active relationships are defined by route priorities in CCN. You only need to set route priorities in CCN and configure health check to trigger route switching.



### Where is the interconnection IP address configured?
The interconnection IP address is configured on both sides of the connection: the device of the Direct Connect access point and the CPE of users.



### How do I use one VLAN connection to access multiple Tencent Cloud VPCs?
Add these VPCs to a [CCN](https://www.tencentcloud.com/products/ccn) instance.



### How does Tencent Cloud isolate tenants to ensure data security?
Tencent Cloud applies MPLS_VPN to the private network, with the Direct Connect access point serving as the provider edge (PE) of MPLS. The virtual routing and forwarding (VRF) technology is used in the VPC to isolate connections to cloud services and protect user data.


### How is switchover between redundant connections triggered?
  - For static routing, configure bidirectional forwarding detection (BFD) to achieve route convergence.
  - For BGP routing, switchover is triggered by the BGP convergence mechanism or a BFD configuration. Contact your Direct Connect delivery engineer to configure BFD for you.
IP SLA cannot be configured. This is because the device at the access point manages a large number of connections. IP SLA will downgrade the performance of the device, which may negatively affect all users of the access point.


### Does Tencent Cloud support the link aggregation control protocol (LACP)?
No, this protocol is not supported.


### Why does the connection performance test result fall short of expectations?
Double check the connection bandwidth you purchased.
Ping the interconnection IP address to check for packet loss and troubleshoot with Tencent Cloud after-sales team in case of serious packet loss. For a self-built connection, you also need to report the problem to the ISP.
Check whether your local router uses the full-duplex mode.
Use iperf or other tools to start multiple processes from both clients and CVMs for the traffic stress test. Troubleshoot application problems based on the test results.
If needed, contact Tencent Cloud after-sales team for assistance.


### What should I do if the connection to Tencent Cloud is interrupted?
- Confirm whether the connection is interrupted:
  Unable to ping the interconnection IP address or receive the MAC address of the CVM instance. Tencent Cloud after-sales team receives an alarm indicating the connection exception.
- The connection is interrupted:
   - For a Tencent Cloud connection, report the failure to Tencent Cloud after-sales team as soon as possible. Generally, the after-sales team will report the connection failure to the ISP immediately after receiving the alarm.
   - For a self-built connection, report the failure to the ISP. Contact the Tencent Cloud after-sales team for assistance if needed.


### What can I do if a specific IP range of the connection fails to be pinged?
- Check whether the IP range is new, and configure routes for the new IP range in the VPC.
- Confirm that the cloud route table is configured with different IP ranges pointing to the direct connect gateway, and that the client server has a route pointing to the connection.
- Check the security features. For example, check whether the CVM instance has associated with security groups or network ACLs, and the client server has configured iptables.
- If no problem is found, provide the after-sales team with troubleshooting information for subsequent operations.



### What information do I need to provide the customer service for troubleshooting?
To request troubleshooting, provide the following information:
- A description of the problem and whether the problem can be reproduced.
- The source IP address and the destination IP address.
- The location of the connection.
- The ID of the direct connect gateway.
- Screenshots of ping and traceroute commands.
- The iptables and NAT information.
- The access topology.
