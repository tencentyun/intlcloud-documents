Dedicated tunnels are network linkage segmentation of a connection. You can create dedicated tunnels that connect to different Direct Connect gateways to enable communication between your local IDC and multiple VPCs.

<span id ="background"></span>

## Background

A new dedicated tunnel no longer supports the shared connection feature since August 1, 2020 00:00:00. However, you can continue using this feature on existing dedicated tunnels. If you delete the tunnel, you cannot apply for a new one with the shared connection after August 1, 2020 00:00:00.

## Use Limits on a Large IP Range

To ensure the fine-grained scheduling capability of your network, do not publish the following routes:
10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 100.64.0.0/10.
You can split the preceding extensive routes as follows for distribution:

- 10.0.0.0/8            
  split into 10.0.0.0/9 + 10.128.0.0/9.
- 172.16.0.0/12      
  split into 172.16.0.0/13 + 172.24.0.0/13.
- 192.168.0.0/16    
  split into 192.168.0.0/17 + 192.168.128.0/17.
- 100.64.0.0/10      
  split into 100.64.0.0/11 + 100.96.0.0/11.


## Directions

1. Log in to the [Direct Connect - Dedicated Tunnels](https://console.cloud.tencent.com/dc/dcConn) console.
2. On the **Dedicated Tunnels** page, click **+New** and complete the following configurations.
3. In the **Basic Configuration** tab, configure the name, connection type, access network, gateway region, and Direct Connect gateway.  

| Parameter | Description | Remarks |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Name | Enter the name of your dedicated tunnel. | - |
| Connection Type | <ul> <li>Connections: indicates the connection that uses your account</li><li>Shared Connections: indicates the connection that uses an account rather than yours. By using a shared connection, you do not share the bandwidth of the connection, but share the Tencent Cloud connection port. Tenants are isolated by using 802.1q VLANs technology.</li></ul> | If you want to use **Shared Connection**, take notice of the [background](#background), select **Shared Connection** in the **Basic Configuration** tab, and enter **Provider Account ID** and **Shared Connection ID**. |
| Access Network | [VPC](https://intl.cloud.tencent.com/document/product/215), BM Network, and [CCN](https://intl.cloud.tencent.com/document/product/1003) are supported. | With CCN, you can connect to multiple VPCs through one dedicated tunnel. |
| VPC/BM Network | Select the ID of the network to which the dedicated tunnel will connect. | Currently, BM network only supports standard Direct Connect gateways. |
| Gateway Region | For **CCN**, gateway region is the CCN Direct Connect gateway region, which is the same as the public cloud region to which the connection access point belongs. | For shared connection, you need to ask the connection owner for information on the region of the connection access point. |
| Direct Connect Gateway | VPC Direct Connect gateway and the VPC are in the same region. CCN Direct Connect gateway and the connection access point are in the same public cloud region. | Currently, CCN Direct Connect gateways do not support the NAT feature. |

4. In the **Advanced Configuration** tab, complete the following configurations.

| Parameter | Description | Remarks |
| -------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| VLAN ID | VLAN ID = 0: the connection does not enable subinterface and only one dedicated tunnel can be created. | To enable a MSTP connection to pass through multiple VLANs, you need to enable the Trunk mode for your ISP line. |
| Bandwidth | Bandwidth indicates the maximum rate, which can be changed later in "Change Tunnel". In the monthly 95th percentile billing mode, this parameter does not represent the billable bandwidth. | - |
| Peer IP | This IP can be user-defined or randomly assigned by Tencent Cloud. After submitting a ticket for tunnel creation, you can go to the details page of the tunnel to get the peer IP.<ul><li>"Cloud Peer IP" is the IPs for interconnection on Tencent Cloud.</li><li>"CPE Peer IP" is the IPs for interconnection on the user (or ISP) side, which must be manually configured.</li></ul> | If you choose to publish the peer IP to Direct Connect gateway, plan your IPs in advance to avoid any IP conflicts. |
| Routing Mode | BGP and static routes are supported.                                     | Tencent Cloud ASN: 45090                                          |
| BGP ASN | For **BGP**, this parameter is optional. Enter the AS number of the BGP neighbor on the CPE side, otherwise a random one will be assigned. | - |
| BGP Key | For **BGP**, this parameter is optional. Enter the MD5 of the BGP neighbor. The default value is “tencent". If this parameter is left empty, it indicates that no BGP key is required.| - |

5. Configure IDC devices.
    You can download the CPE configuration guide which provides common configuration methods.

| Parameter | Description | Remarks |
| ----------- | ---------------------------------------- | --------------------------------- |
| CPE IP Range | For **Static**, enter the IP range of the user-side CPE. Note that it cannot be conflict with the VPC IP range for non-NAT Direct Connect gateway | You can update the IP range later in the "Change Tunnel" page on the console. |



## Connection Status

A dedicated channel may have the following status:

- **Applying**
  The system has received your application for a new dedicated channel and is ready to start the creation.
- **Pending accepted**
  The connection owner is reviewing the application. Once the application is “accepted” to the connection owner, the dedicated tunnel can be created without Tencent Cloud’s approval.
- **Configuring**
  The system is delivering the configuration. If the status has been stuck at "Configuring" for a long time, the configuration delivery encountered a problem. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
  The system has completed the configuration based on the specified parameters, but has not been able to ping through your IDC. A dedicated channel in this status can be deleted.
- **Connected**
  The system pings to your IDC device successfully. However, this does not mean that your business is connected. Instead, you must go to the [route table](https://console.cloud.tencent.com/vpc/route?rid=1) of the VPC or CCN instance to complete the configuration and connection.
- **Deleting**
  The system is deleting your application. If the status has been stuck at "Deleting" for a long time, the system encountered a problem when deleting the configuration. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

