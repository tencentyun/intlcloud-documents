## Operation Scenarios
Tencent Cloud supports [basic network and VPC](https://intl.cloud.tencent.com/document/product/215/31807), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you manage network connectivity with ease.
- **Network switch**
  - Switch from basic network to VPC: a single TencentDB instance can be switched from basic network to VPC.
  - Switch from VPC A to VPC B: a single TencentDB instance can be switched from VPC A to VPC B.
- **Custom IP**

## Notes
- Switching the network may cause the change of instance's private IP. The original IP will become invalid after 24 hours by default. Please modify the instance IP on the client promptly. If the repossession time for the old IP address is set to 0 hours, the old IP address will be repossessed immediately after the network switch.
- To prevent abuse of IP resources, you can switch network once every 24 hours.
- Only VPCs and subnets in the region and AZ where the instance reside can be selected.
- The switch from basic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or basic network.
- Instances where the data replication mode is strong sync replication do not support the above-mentioned switches.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance name or **Manage** in the "Operation" column to enter the instance details page.
2. According to the type of network switch, click **Switch to VPC** or **Change Network** after "Network" in the basic instance information section.
3. In the pop-up dialog box, select a VPC and corresponding subnet and click **OK**.
>
>- If there is no IP address specified, one will be automatically assigned by the system.
>- You are recommended to select the VPC where the CVM instance resides; otherwise, the CVM instance will not be able to access TencentDB for MySQL over the private network, unless a [peering connection](https://intl.cloud.tencent.com/document/product/553/18827) or a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.
>
   - **Switch from basic network to VPC**
   - **Switch from VPC A to VPC B**
![](https://main.qcloudimg.com/raw/274c2057ec225eab9e16b1c18bafa94c.png)
4. Return to the instance details page where you can view the network of the instance.
![](https://main.qcloudimg.com/raw/5342a64814664fa784e256ecbd6f934f.png)
