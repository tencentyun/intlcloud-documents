## Overview
Tencent Cloud supports [classic network and VPC](https://intl.cloud.tencent.com/document/product/215/31807), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you manage network connectivity with ease.
- The network of a TencentDB for MongoDB primary instance can be switched from classic network to VPC.
- The network of a TencentDB for MongoDB primary instance can be switched from VPC A to VPC B.

## Notes
- Switching the network may cause the change of instance's private IP. The original IP will become invalid after the repossession time has elapsed. Please modify the instance IP on the client promptly.
- The switch from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
- After you switch a primary instance's network, the networks of read-only replicas or disaster recovery instances associated with the primary instance won’t be automatically switched, that is, you need to manually switch them.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb/instance), click an instance ID in the instance list, and enter the instance details page.
2. Click **Change Network** next to **Network** in the **Basic Info** section.
3. In the pop-up dialog box, select a VPC and a subnet and click **OK**.
>?
>- If there is no IP address specified, one will be automatically assigned by the system.
>- You can only select a VPC in the region of the instance.
>- We recommend you select the VPC where the CVM instance resides; otherwise, the CVM instance will not be able to access TencentDB for MongoDB over the private network, unless a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.
>
   - **Switch from classic network to VPC**
![](https://main.qcloudimg.com/raw/2ce132b20ce34b40c107f76cec068264.png)
   - **Switch from VPC A to VPC B**![](https://main.qcloudimg.com/raw/88776655b51932bc6680ffa01de1e33a.png)
4. Return to the instance details page where you can view the network of the instance.

