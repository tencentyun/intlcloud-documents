This document describes how to switch the instance network from classic network to VPC in the TencentDB for SQL Server console.

## Network types
There are two types of TencentDB network environments: classic network and VPC.
- Classic network: It is the public network resource pool for all Tencent Cloud users. All your Tencent Cloud resources will be centrally managed by Tencent Cloud.
- VPC: It is a logically isolated network space that can be customized in Tencent Cloud. Even in the same region, different VPCs cannot communicate with each other by default. Similar to the traditional network in an IDC, a VPC is where your Tencent Cloud service resources are managed.

## Overview
Tencent Cloud supports classic network and VPC, which are capable of offering a diversity of smooth services. On this basis, we provide the classic network to VPC switch feature to help you manage network connectivity with ease.

## Supported instance types
Primary and read-only instances on all versions.

## Notes
- Currently, you can only switch from classic network to VPC but not vice versa.
- After the switch, VPC access will take effect immediately. The original classic network access will be retained for 24 hours; therefore, other instances associated to the instance should be migrated to VPC within 24 hours so as to guarantee uninterrupted access.
- If **Valid Hours of Old IP** is set to 0, the IP will be released immediately after the network is changed. Then, you can only access the instance over the VPC.
- After you switch the primary instance's network, the networks of read-only instances associated with the primary instance won't be automatically switched, that is, you need to manually switch them.

## Subnet description
A subnet is a logical network space in a VPC. You can create subnets in different AZs in the same VPC, which communicate with each other over the private network by default. Even if you select a subnet in another AZ in the same region, the network latency will not be increased because the actual business connection adopts nearby access.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region, and click **Instance ID/Name** of the target instance.
![](https://qcloudimg.tencent-cloud.cn/raw/7d4769e9b89d112b3218b4109eba9655.png)
2. On the **Instance Details** page, click **Switch to VPC** in **Basic Info** > **Network**.
![](https://qcloudimg.tencent-cloud.cn/raw/1b847be83a4ceb510ef3f1b0a655cfe5.png)
3. In the pop-up window, select a VPC, set **Valid Hours of Old IP**, select **Auto-Assign IP** or **Specify IP**, and click **OK**.
 - Select Network: After a VPC is selected, only servers in it can access the database.
 - Valid Hours of Old IP: You can select 0–168 hours. If it is set to 0, the old IP will be repossessed immediately.
 - Auto-Assign IP: The system automatically assigns the new IP address.
 - Specify IP: You can customize the subnet IP address.
 ![](https://qcloudimg.tencent-cloud.cn/raw/56d32d9782b379a2e7e2d3e66fc1a42c.png)
4. The classic network is successfully switched to VPC when the instance status becomes **Running**.
