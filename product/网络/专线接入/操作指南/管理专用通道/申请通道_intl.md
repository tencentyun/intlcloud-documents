1. Open [Tencent Cloud Direct Connect Console - Direct Connect Tunnel](https://console.cloud.tencent.com/vpc/dcConn);
2. Click **+ New** to initiate the application for Direct Connect tunnel. You need to enter the following information to create a Direct Connect tunnel:
<style>
table th:first-of-type {
    width: 150px;
}
</style>
If you would use the Connection under your own Tencent account, steps as below:

| Parameter | Description | Remarks |
| --------- | ---------------- | -------- |
| Dedicated Tunnel name | Create your Dedicated Tunnel name | -------- |
| Connection Type | Select My Connection, which means the Connection under your account. Or shared Connection, which is under other accounts |-------- |
| Connection ID | Select the ID of the Connection by which you want to setup a tunnel | -------- |
| Target Network | VPC and CCN network are available in Tencent Cloud International station |-------- |
| VPC | Select the ID of the network accessed via the Dedicated tunnel |-------- |
| DC Gateway | The gateway type is displayed on the left of the gateway name. Check if it meets you need |-------- |
| VLANID  | Specify the non-conflicted VLANID, 0 indicates that the sub-interface is not enabled for the Connection and only one tunnel can be created |-------- |
| Peer IP | "Specific" means the peering IP should be specified on your own. "Random" means Tencent Cloud will allocate the non-conflict Peer IP for you. You can find it in tunnel details after you create it. |-------- |
| Routing Method | BPG and static. Routing information is required for static route |-------- |
| BGP ASN   | Optional, automatically assigned if not specified. |-------- |
| BGP Key | Optional, "Tencent" is displayed at frontend by default. Leave it empty means no key needed. |-------- |
| IDC Routes | Enter the user's IDC IP address range, which cannot conflict with that of VPC except in NAT mode | Only valid for static route |-------- |


If you would use the Connection under other Tencent account, steps as below:

| Parameter | Description | Remarks |
| --------- | ------------- | -------- |
| Dedicated Tunnel name | Create your Dedicated Tunnel name | -------- |
| Connection Type | Select shared Connection, which is under other accounts | -------- |
| Provider Account ID | You should ask the Connection provider for his Tencent Cloud ID. | Only valid for shared Connection |-------- |
| Connection ID | Enter the ID of the Shared Connection for which you want to setup a tunnel | Only valid for shared Connection |
| Target Network | VPC and CCN network are available in Tencent Cloud International station | -------- |
| VPC | Select the ID of the network accessed via the Dedicated tunnel | -------- |
| DC Gateway | The gateway type(standard or NAT) is displayed on the left of the gateway name. Please double check if it meets you need|-------- |
| VLANID | Specify the non-conflicted VLANID, 0 indicates that the sub-interface is not enabled for the Connection and only one tunnel can be created |-------- |
| Peer IP | "Specific" means the peering IP should be specified on your own. "Random" means Tencent Cloud will allocate the non-conflict Peer IP for you. You can find it in tunnel details after you create it. |-------- |
| Routing Method | BPG and static. Routing information is required for static route |-------- |
| BGP ASN   | Optional, automatically assigned if not specified. | -------- |
| BGP Key | Optional, "Tencent" is displayed at frontend by default. Leave it empty means no key needed. | -------- |
| IDC Routes | Enter the user's IDC IP address range, which cannot conflict with that of VPC except in NAT mode | Only valid for static route | -------- |

>**Note:**
-The following CIDR will be rejected by Tencent Cloud, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 and 100.64.0.0/10, due to the restriction of Tencent Cloud Network.
-You can divide the CIDR into 2 subnets of them and broadcast:

10.0.0.0/8 = 10.0.0.0/9 + 10.128.0.0/9；
172.16.0.0/12 = 172.16.0.0/13 + 172.24.0.0/13；
192.168.0.0/16 = 192.168.0.0/17 + 192.168.128.0/17；
100.64.0.0/10 = 100.64.0.0/11 + 100.96.0.0/11。

