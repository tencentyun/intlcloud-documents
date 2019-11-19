## Operation Scenario
Tencent Cloud supports [basic network and VPC](https://intl.cloud.tencent.com/document/product/215/31787), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you manage network connectivity with ease.
- **Network switch**
  - Switch from basic network to VPC: A single TencentDB instance can be switched from basic network to VPC.
  - Switch from VPC A to VPC B: A single TencentDB instance can be switched from VPC A to VPC B.
- **Custom IP**

## Notes
- Switching the network may cause the change of instance IP. The original IP will become invalid after 24 hours. Please modify the instance IP on the client in a timely manner.
- To prevent abuse of IP resources, you can switch network once every 24 hours.
- Only VPCs and subnets in the region and AZ where the instance reside can be selected.
- The switch from basic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or basic network.
- Instances where the data replication mode is strong sync replication do not support the above-mentioned switches.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, select the instance for which to switch the network and click the instance name or **Manage** in the **Action** column to enter the instance details page.
3. According to the type of network switch, click **Switch to VPC** or **Change Network** after **Network** in the basic instance information section.
4. In the pop-up dialog box, select a VPC and corresponding subnet and click **OK**.
<!--
   - **Switch from basic network to VPC**
![]()
-->
   - **Switch from VPC A to VPC B**
![](https://main.qcloudimg.com/raw/274c2057ec225eab9e16b1c18bafa94c.png)
>If there is no IP address specified, one will be automatically assigned by the system.
4. Return to the instance details page where you can view the network of the instance.
![](https://main.qcloudimg.com/raw/5342a64814664fa784e256ecbd6f934f.png)
