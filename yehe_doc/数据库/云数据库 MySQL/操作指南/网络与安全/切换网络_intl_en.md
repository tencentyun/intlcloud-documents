## Overview
Tencent Cloud supports classic network and VPC as described in [Overview](https://intl.cloud.tencent.com/document/product/215/31807), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you manage network connectivity with ease.
- **Network switch**
  - Switch from classic network to VPC: A single TencentDB source instance can be switched from classic network to VPC.
  - Switch from VPC A to VPC B: A single TencentDB source instance can be switched from VPC A to VPC B.
- **Custom IP and port**
  - Custom source instance IP and port: The IP and port of a source instance can be customized on the instance details page in the console.
  - Custom read-only instance IP and port: The IP and port of a read-only instance can be customized on the instance details page in the console.

## Notes
- After the switch from classic network to VPC, only clients in the same VPC can interconnect with each other. You can [configure](https://intl.cloud.tencent.com/document/product/215/31805) a VPC IP range to keep the VPC IP the same as the classic network IP.
- The repossession time for the old IP is 24 hours by default and can be up to 168 hours. If "Valid Hours of Old IP" is set to 0 hours, the IP is released immediately after the network is changed.
- The switch from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
- The network switch of a primary instance doesn't apply to its associated read-only instances or disaster recovery instances, you need to manually switch the network for these instances.

## Subnet Description
- A subnet is a logical network space in a VPC. You can create subnets in different AZs in the same VPC, which communicate with each other over the private network by default.
- After you select a network, the subnet IPs in the AZ of the selected instance are displayed by default. You can also select subnet IPs in other AZs in the region of the instance. Business connections adopt nearby access, so the network latency will not be increased.

## Directions
### Switching the network
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Click **Switch to VPC** or **Change Network** after **Network** in the **Basic Info** section.
3. In the pop-up window, select a VPC and a subnet and click **OK**.
>?
>- If there is no IP address specified, one will be automatically assigned by the system.
>- You can only select a VPC in the region of the instance, but you can choose a subnet in any AZ and view its IP range.
>- We recommend that you select a VPC in the region where the CVM instance resides; otherwise, the CVM instance will not be able to access TencentDB for MySQL over the private network, unless a [peering connection](https://intl.cloud.tencent.com/document/product/553/18827) or a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.
>
   - **Switch from classic network to VPC**
![](https://main.qcloudimg.com/raw/ba78ed608b83c2f553cb72350b726491.png)
   - **Switch from VPC A to VPC B**
![](https://qcloudimg.tencent-cloud.cn/raw/82c30b3269695e6428de87d2c2c06cc0.png)
4. Return to the instance details page where you can view the network of the instance.

### Switching the RO group network
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **RO Group Info** of a read-only instance, click **Change Subnet** or **Switch to VPC** according to the network switch type (classic network to VPC or VPC to VPC).
3. In the pop-up window, select a VPC and a subnet and click **OK**.
>?
>- If there is no IP address specified, one will be automatically assigned by the system.
>- You can only select a VPC in the region of the instance, but you can choose a subnet in any AZ and view its IP range.
>- We recommend you select a VPC in the region where the CVM instance resides; otherwise, the CVM instance will not be able to access TencentDB for MySQL over the private network, unless a [peering connection](https://intl.cloud.tencent.com/document/product/553/18827) or a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.

### Customizing the IP and port
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> after **Private Network Address** and **Private Port** in the **Basic Info** section.
>!Modifying the private network address and port affects the database business being accessed.
3. In the pop-up window, specify the IP and port and click **OK**.
