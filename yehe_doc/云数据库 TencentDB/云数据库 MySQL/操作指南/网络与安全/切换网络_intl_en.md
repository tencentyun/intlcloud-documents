## Overview
Tencent Cloud supports [classic network and VPC](https://intl.cloud.tencent.com/document/product/215/31807), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you manage network connectivity with ease.
- **Network switch**
  - Switch from classic network to VPC: a single TencentDB instance can be switched from classic network to VPC.
  - Switch from VPC A to VPC B: a single TencentDB instance can be switched from VPC A to VPC B.
- **Custom IP**

## Notes
- Switching the network may cause the change of instance's private IP. The original IP will become invalid after the repossession time has elapsed. Please modify the instance IP on the client promptly.
The default repossession time for the original IP is 24 hours and the longest repossession time can be 168 hours. If the repossession time is set to 0 hours, the original IP address will be repossessed immediately after the network switch.
- The switch from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
- After you switch a source instance's network, the networks of read-only or disaster recovery instances mounted to the source instance won’t be automatically switched, that is, you need to manually switch them.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance details page.
2. According to the type of network switch, click **Switch to VPC** or **Change Network** after **Network** in the basic instance information section.
3. In the pop-up dialog box, select a VPC and corresponding subnet and click **OK**.
>?
>- If there is no IP address specified, one will be automatically assigned by the system.
>- You can only select a VPC in the region of the instance.
>- You are recommended to select the VPC where the CVM instance resides; otherwise, the CVM instance will not be able to access TencentDB for MySQL over the private network, unless a [peering connection](https://intl.cloud.tencent.com/document/product/553/18827) or a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.
>

4. Return to the instance details page where you can view the network of the instance.
![](https://main.qcloudimg.com/raw/5342a64814664fa784e256ecbd6f934f.png)
