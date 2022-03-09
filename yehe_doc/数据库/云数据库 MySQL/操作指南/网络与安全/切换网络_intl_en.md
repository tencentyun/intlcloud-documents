## Overview
Tencent Cloud supports [classic network and VPC](https://intl.cloud.tencent.com/document/product/215/31807), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you manage network connectivity with ease.
- **Network switch**
  - The network of a TencentDB for MongoDB primary instance can be switched from classic network to VPC.
  - The network of a TencentDB for MongoDB primary instance can be switched from VPC A to VPC B.
- **Custom IP and port**
 - Custom source instance IP and port: the IP and port of a source instance can be customized on the instance details page in the console.
 - Custom read-only instance IP and port: the IP and port of a read-only instance can be customized on the instance details page in the console.

## Note
- Switching the network may cause the change of instance's private IP. The original IP will become invalid after the repossession time has elapsed. Modify the instance IP on the client promptly.
The default repossession time for the original IP is 24 hours and the longest repossession time can be 168 hours. If "Valid Hours of Old IP" are set to 0 hours, the IP is released immediately after the network is changed.
- The switch from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
- After you switch a primary instance's network, the networks of read-only instances or disaster recovery instances associated with the primary instance won’t be automatically switched, that is, you need to manually switch them.

## Directions
### Switching network
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Click **Switch to VPC** or **Change Network** after **Network** in the **Basic Info** section.
3. In the pop-up dialog box, select a VPC and a subnet and click **OK**.
>?
>- If there is no IP address specified, one will be automatically assigned by the system.
>- You can only select a VPC in the region of the instance, but you can choose a subnet in any AZ and view its IP range.
>- We recommend you select a VPC in the region where the CVM instance resides; otherwise, the CVM instance will not be able to access TencentDB for MySQL over the private network, unless a [peering connection](https://intl.cloud.tencent.com/document/product/553/18827) or a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.
>
   - **Switch from classic network to VPC**
![](https://main.qcloudimg.com/raw/ba78ed608b83c2f553cb72350b726491.png)
   - **Switch from VPC A to VPC B**
![](https://qcloudimg.tencent-cloud.cn/raw/82c30b3269695e6428de87d2c2c06cc0.png)
4. Return to the instance details page where you can view the network of the instance.


### Customizing IP and port
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> after **Private Network Address** and **Private Port** in the **Basic Info** section.
>!Modifying the private IP and port affects the database business being accessed.
3. In the pop-up dialog box, specify the IP and port, and click **OK**.
