You can directly switch the network of a TencentDB for MongoDB instance in the console to adjust the network status promptly.

## Background
Tencent Cloud supports classic network and VPC as described in [Overview](https://intl.cloud.tencent.com/document/product/215/31807), which are capable of offering a diversity of smooth services. On this basis, we provide more flexible services to help you manage network connectivity with ease.
- Switch from classic network to VPC: A single TencentDB primary instance can be switched from classic network to VPC.
- Switch from VPC A to VPC B: A single TencentDB primary instance can be switched from VPC A to VPC B.

## Version requirements
Currently, TencentDB for MongoDB 4.4, 4.2, 4.0, 3.6, and 3.2 support instance network switch.

## Billing
Switching the instance network doesn't incur additional fees.

## Notes
- Switching the network may cause the change of instance's private IP. The original IP will become invalid after the repossession time has elapsed. Modify the instance IP on the client promptly.
- The switch from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
- After you switch a primary instance's network, the networks of read-only replicas or disaster recovery instances associated with the primary instance won't be automatically switched, that is, you need to manually switch them.

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page and click **Change Network** on the right of **Network**.
6. In the **Change Network** pop-up window, select a VPC and subnet in the current region in the drop-down list next to **Network**.
    If existing networks can't meet your requirements, you can click **Create VPCs** or **Create Subnets** to create a network and select it.
    ![](https://qcloudimg.tencent-cloud.cn/raw/5d0fc6eea7973e5bac552d1181b6d356.png)
 - **New IP Assignment Method**: Select **Auto Assign** or **Designate address**.
    - **Auto Assign**: The system will automatically assign an available IP address based on the currently selected network environment.
    - **Designate address**: You can enter a specific IP address in the **New IPv4 Address** input box. The specified IP address must be unoccupied and within the IP range of the specified VPC.
> ?
> - You can only select a VPC in the region of the instance.
> - We recommend that the VPC where the CVM instance resides should be selected; otherwise, the CVM instance will not be able to access TencentDB for MongoDB over the private network, unless a [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) instance is created between the two VPCs.
 - **Old IP**: For a replica set instance, the old IP address can be released immediately. For a sharded cluster instance, you need to select the release time of the old IP address in the drop-down list, which can be **Release Now**, **Release after 1 day**, **Release after 2 days**, **Release after 3 days**, or **Release after 7 days**.
>! If you select **Release Now**, all network connections to the old IP will be closed immediately. Select a release time with caution.
>
7. Confirm the network switch and click **OK**. Return to the instance details page, where you can view the network of the instance.

