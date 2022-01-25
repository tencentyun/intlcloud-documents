You can directly switch the network of a TencentDB for MongoDB instance in the console to adjust the network status promptly.

## Background
Tencent Cloud supports [classic network and VPC](https://intl.cloud.tencent.com/document/product/215/31807), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services as shown below to help you manage network connectivity with ease.
- Switch from classic network to VPC: a single TencentDB source instance can be switched from classic network to VPC.
- Switch from VPC A to VPC B: a single TencentDB source instance can be switched from VPC A to VPC B.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support instance network switch.

## Billing Description
Switching the instance network doesn't incur additional fees.

## Notes
- Switching the network may cause the change of instance's private IP. The original IP will become invalid after the release time has elapsed. Therefore, modify the instance IP on the client promptly.
- The switch from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
- After you switch a primary instance's network, the networks of read-only or disaster recovery instances associated with the primary instance won't be automatically switched; therefore, you need to manually switch them.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. In the **Basic Info** section, click **Change Network** on the right of **Network**.
7. In the **Change Network** pop-up window, select a VPC and subnet in the drop-down list next to **Network**.
If existing networks can't meet your requirements, you can click **Create VPCs** or **Create Subnets** to create a network and select it.
8. Select **Auto Assign** or **Designate Address** for **New IP Assignment Method**.
  - **Auto Assign**: the system will automatically assign an available IP based on the currently selected network environment.
  - **Designate Address**: you can enter a specific IP address in the **New IPv4 Address** input box.
> ?
> - You can only select a VPC in the region of the TencentDB for MongoDB instance.
> - We recommend you select the VPC where the CVM instance resides; otherwise, the CVM instance will not be able to access TencentDB for MongoDB over the private network, unless a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.
9. In the drop-down list next to **Old IP**, select the release time of the old IP.
>! If you select **Release Now**, all network connections to the old IP will be closed immediately. Select a release time with caution.
>
![](https://qcloudimg.tencent-cloud.cn/raw/5d0fc6eea7973e5bac552d1181b6d356.png)
10. Confirm the network switch and click **OK**. Return to the instance details page, where you can view the network of the instance.


