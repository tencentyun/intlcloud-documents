## Application Procedure
1. Log in to the [Direct Connect - Dedicated Tunnel](https://console.cloud.tencent.com/dc/dcConn) console.
2. Start your dedicated tunnel application by clicking **+Create**. Provide the following information to create a dedicated tunnel. For more information on the parameters, see [Parameter Description](#shuoming).
 1. Basic configuration:
 If your account has an available connection, the application page looks like this:

 If your account does not have an available connection, the application page looks like this:

 2. Advanced configuration:
 3. IDC device configuration:
To do this, you can download the CPE configuration guide, which provides the configuration methods of several common vendors.

<span id='shuoming'></span>
## Parameter Description
<style>
table th:first-of-type {
    width: 150px;
}
    table th:nth-of-type(3)  {
    width: 250px; 
}
</style>

| Parameter | Description | Notes |
| ----------- | ---------------------------------------- | --------------------------------- |
| Dedicated tunnel name | Specify a name for your dedicated tunnel. | - |
| Connection type | <li>My connection: indicates the connection that uses your account.</li><li>Hosted connection: (to be available soon) indicates the connection that is assigned to you by the connection owner with an exclusive bandwidth.</li><li>Shared connection: indicates the connection that uses an account different than your account. By using shared connection, you do not share the bandwidth of the connection, but the Tencent Cloud connection port. Tenants are isolated by using 802.1q VLAN technology.</li> | Shared connection only requires the approval of the connection owner, but not the approval by Tencent Cloud. |
| Connection | For **My Connection** and **Hosted Connection**, select the ID of the connection for which you want to establish the dedicated tunnel. | - |
| Connection provider | For **Shared Connection**, enter the account to which the shared connection belongs. | - |
| Shared connection ID | For **Shared Connection**, enter the ID of the connection for which you want to establish the dedicated tunnel. | - |
| Access network | [VPC](https://intl.cloud.tencent.com/document/product/215), BM network, and [CCN](https://intl.cloud.tencent.com/document/product/1003) are supported. | With CCN, you can connect to multiple VPC instances through one dedicated tunnel. |
| VPC/BM network | For **VPC** and **BM Network**, select the ID of the network to which the dedicated tunnel will connect. | Currently, BM network only supports standard Direct Connect gateways. |
| Gateway region | For **CCN**, the gateway region is the CCN Direct Connect gateway region, which is the same as the public cloud region to which the connection access point belongs. | For shared connection, you need to consult the connection owner for information on the region of the connection access point. |
| Direct Connect gateway | The VPC Direct Connect gateway and the VPC belong to the same region. The CCN Direct connect gateway and the connection access point belong to the same public cloud region. | Currently, CCN Direct connect gateways do not support the NAT feature. |
| VLAN ID | VLAN ID = 0: the connection does not enable subinterfaces and only one dedicated tunnel can be created. | To enable an MSTP connection to pass through multiple VLANs, you need to enable the Trunk mode for your ISP connection. |
| Bandwidth | The bandwidth indicates the maximum rate, which can be changed later in "Modify Tunnel". In the postpaid monthly 95th percentile billing method, the "bandwidth" parameter does not represent the billable bandwidth. | - |
| Interconnect IP | This IP address can be customized by the user or provided randomly by Tencent Cloud. You can obtain the randomly assigned interconnect IP address in tunnel details after your application is submitted and approved.<li>"Tencent Cloud perimeter IP" indicates the perimeter interconnect IP address of the connection at the Tencent Cloud side.</li><li>"User perimeter IP" indicates the interconnect IP address of the connection at the user (or ISP) side, which must be configured by yourself.</li> | If you choose to publish the interconnect IP to the Direct Connect gateway, plan your IP addresses in advance to avoid any IP conflicts. |
| Routing mode | BGP routing and static routing are supported. | Tencent Cloud ASN: 45090 |
| BGP ASN | For **BGP Routing**, this parameter is optional. Enter the BGP neighbor AS number at the CPE side. If this parameter is left empty, the system randomly assigns a number for it. | - |
| BGP key | For **BGP Routing**, this parameter is optional. Enter the MD5 hash of the BGP neighbor. The default value of this parameter is "tencent". If this parameter is left blank, it indicates that no BGP key is required. | - |
| User IDC IP range | For **Static Routing**, enter the IP range of the user-side CPE. Note that it must not conflict with the VPC IP range when in non-NAT mode. | You can update the IP range later in the "Modify Tunnel" section in the console. |

## Connection States
The possible states of a connection are as follows:
- **Applying**
The system has received your application for a new dedicated tunnel and is ready to start a creation job.
- **Pending Approval**
The connection owner is reviewing the application. Once the application is "approved" by the connection owner, the dedicated tunnel can be created without Tencent Cloud approval.
- **Configuring**
The system is delivering the configuration. If the state has been stuck at "Configuring" for a long time, the configuration delivery might encountered a problem. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
The system has completed the configuration based on the specified parameters, but has not been able to ping through your IDC interconnect address.
- **Connected**
The system is able to ping through the interconnect address of your IDC device. However, this does not mean that your service is connected. Instead, you must go to the [route table](https://console.cloud.tencent.com/vpc/route?rid=1) of the VPC or CCN instance to complete the configuration and connection.
- **Deleting**
The system is deleting your application. If the state has been stuck at "Deleting" for a long time, the system encountered a problem when deleting the configuration. In this case, you can contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Use Limits on a Large IP Range
To ensure the fine-grained scheduling capability of your network, do not publish the following routes:
10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 100.64.0.0/10.
You can split the preceding extensive routes as follows for distribution:
- 10.0.0.0/8            
is split into 10.0.0.0/9 + 10.128.0.0/9.
- 172.16.0.0/12      
is split into 172.16.0.0/13 + 172.24.0.0/13.
- 192.168.0.0/16    
is split into 192.168.0.0/17 + 192.168.128.0/17.
- 100.64.0.0/10      
is split into 100.64.0.0/11 + 100.96.0.0/11.
