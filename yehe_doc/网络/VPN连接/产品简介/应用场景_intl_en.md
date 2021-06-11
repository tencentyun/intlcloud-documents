Tencent Cloud VPN Connections provides Internet-based remote network connection services. As an important component of a VPN connection, a VPN gateway can enable secure site-to-site access by creating a secure encrypted IPsec tunnel with the customer IDC. Featuring flexible configuration, VPN can meet your various communication requirements.

VPN has two routing and forwarding methods:
+ Matching the source and destination IP ranges of data flow based on the SPD policy-based routing, and forwarding according to the set forwarding policy. Routing cannot be realized through this method, so traffic cannot be forwarded, but the first, fourth and sixth communication scenarios can be realized.
+ By configuring the VPN route table, you can route and forward data packets based on the destination IP range. This method is called destination routing, and all the following communication scenarios can be realized with this method. The sixth scenario can not only be realized through SPD policy-based routing alone but also through SPD policy-based routing and destination routing at the same time.
   >?
   >- The VPN route table is currently in a beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
   >- The “customer gateway” in the following figures means the logical object that records the public IP address of the IPsec VPN device on the IDC side. Each customer gateway corresponds to the IPsec VPN device on the IDC side.
   >

## Scenario 1: communication between VPC and IDC
VPN Connections enables the communication between VPC and IDC
<img src="https://main.qcloudimg.com/raw/9d0966ac096e8900e1c8cbe10e4cf761.png" width="90%" />

## Scenario 2: traffic interconnection between a single VPC and multiple IDCs
Multiple IDCs connect to each other in the VPN connection-based migration-to-cloud scenario.
**Scenario description**: the customer IDC-1, IDC-2, and IDC-3 are connected to Tencent Cloud VPN gateway for VPC via their respective IPsec VPN device. They can not only access various resources in the VPC of the VPN gateway but also connect to each other through Tencent Cloud VPN gateway, thus enabling secure communication between VPC and the customer IDC-1, IDC-2, and IDC-3.
<img src="https://main.qcloudimg.com/raw/aecb4d8393a5893570eb965559c1a4ec.png" width="90%" />


## Scenario 3: communication among multiple IDCs via a VPN gateway
Multiple IDCs can communicate with each other via the VPN for Cloud Connect Network (CCN) if they don’t need to access cloud resources.
**Scenario description**: the customer IDC-1, IDC-2, and IDC-3 are connected to Tencent Cloud VPN gateway for CCN via their respective IPsec VPN device. They communicate with each other only via Tencent Cloud VPN gateway without the need to access the public cloud resources of Tencent Cloud. In this case, customers can create a VPN gateway for CCN which is not associated with CCN.
<img src="https://main.qcloudimg.com/raw/dd9d7fca3731bfcf7f1b237b16025960.png"  width="90%" />

## Scenario 4: traffic interconnection between multiple IDCs and multiple cloud networks
**Scenario description**: the customer IDC-1, IDC-2, and IDC-3 are connected to Tencent Cloud VPN gateway for CCN via their respective IPsec VPN device. They can communicate with each other via Tencent Cloud VPN gateway and access CCN-associated VPC and direct connect networks via CCN. In this case, customers can create a VPN gateway for CCN and associate it with CCN to realize traffic interconnection.
<img src="https://main.qcloudimg.com/raw/92c456d7769d228c3ae0a8db3dd2d484.png" width="90%" />

## Scenario 5: IDC realizes active/standby cloud disaster recovery through active/standby VPN tunnels
If the customer IDC migrates to cloud via active/standby VPN tunnels, when the active tunnel fails, the business will be automatically switched over to the standby tunnel, thus ensuring business sustainability and reliability.
**Scenario description 1**: The customer IDC only needs to connect to a single Tencent Cloud VPC. On the customer IDC side, the customer can deploy 2 IPsec VPN devices that respectively create IPSec VPN tunnels with Tencent Cloud VPN gateway for VPC. The VPN gateway route table configures 2 routes that share the same destination port, and the active/standby tunnel mechanism will be effective through priority control. In case of failure, the routes can be switched over automatically.
<img src="https://main.qcloudimg.com/raw/6ca796b0fd9cb2dec035a85b2576f2f4.png" width="90%"/>
**Scenario description 2**: The customer IDC needs to connect to multiple Tencent Cloud VPCs (which can be in the same region or different regions) and direct connect networks. On the customer IDC side, the customer can deploy 2 IPsec VPN devices that respectively create IPSec VPN tunnels with Tencent Cloud VPN gateway for CCN. The VPN gateway route table can configure 2 routes that share the same destination port, and the active/standby tunnel mechanism will be effective through priority control. In case of failure, the routes can be switched over automatically.
<img src="https://main.qcloudimg.com/raw/ffcf86f6bd3dc7766f2eab6c844c295e.png" width="90%"/>


## Scenario 6: communication between a single VPC and multiple IDCs via multiple VPN tunnels
This communication scenario is similar to the second scenario. The difference between them is that in this scenario, the customer IDC-1, IDC-2, and IDC-3 only need to communicate with VPC and don’t need to communicate with each other.
+ In terms of this scenario, we recommend that SPD policy-based routing method be used to create the VPC->IDC1, VPC->IDC2, and VPC->IDC3 rules.
+ If the destination routing method is used alone, IDC-1, IDC-2, and IDC-3 can communicate with each other, which does not conform to the communication scenario. You can configure the VPC->IDC1 and VPC->IDC2 rules when using the SPD policy-based routing method, and then configure in the route table a routing policy whose destination IP range is IDC3. As SPD policy-based routing has higher priority over destination routing, this communication scenario can also be realized.
<img src="https://main.qcloudimg.com/raw/3dc127f8c0dfb3ef21ad85bc4eba4edb.png" width="90%"/>
