This document describes how to change the instance network in the TencentDB for SQL Server console.

## Network types
TencentDB instances reside in VPCs.
 
- VPC: It is a logically isolated network space that can be customized in Tencent Cloud. Even in the same region, different VPCs cannot communicate with each other by default. Similar to the traditional network in an IDC, a VPC is where your Tencent Cloud service resources are managed.

## Scenario
Tencent Cloud supports VPC, which is capable of offering a diversity of smooth services. On this basis, we provide the VPC change feature to help you manage network connectivity with ease.

## Supported instance types
Primary and read-only instances on all versions.

## Limits
- Changing the network will change the instance IP. The original IP will become invalid after 24 hours by default. Modify the instance IP on the client promptly.
- If **Valid Hours of Old IP** is set to 0, the IP will be released immediately after the network is changed.

## Subnet description
A subnet is a logical network space in a VPC. You can create subnets in different AZs in the same VPC, which communicate with each other over the private network by default. Even if you select a subnet in another AZ in the same region, the network latency will not be increased because the actual business connection adopts nearby access.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region, and click **Instance ID/Name** of the target instance or **Manage** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/866d9a510b3c29fe0e02c355a8fec4a8.png)
2. On the **Instance Details** page, click **Change Network** in **Basic Info** > **Network**.
![](https://qcloudimg.tencent-cloud.cn/raw/cc1828ab8d229c2b5c3e9b51fdb10781.png)
3. In the pop-up window, select a VPC, set **Valid Hours of Old IP**, select **Auto-Assign IP** or **Specify IP**, and click **OK**.
 - Select Network: After a VPC is selected, only servers in it can access the database.
 - Valid Hours of Old IP: You can select 0–168 hours. If it is set to 0, the old IP will be repossessed immediately.
 - Auto-Assign IP: The system automatically assigns the new IP address.
 - Specify IP: You can customize the subnet IP address.
![](https://qcloudimg.tencent-cloud.cn/raw/af34150095f99c849cffceb47576df22.png)
4. The VPC is changed successfully when the instance status becomes **Running**.
