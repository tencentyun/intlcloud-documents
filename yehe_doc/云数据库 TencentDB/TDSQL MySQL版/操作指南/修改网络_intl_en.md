
This document describes how to change the instance network type and modify the instance access address.

>!Modifying the network configurations of an instance is highly risky. Please do so only during off-peak hours. After modification, unless assigned to another service, the original IP will remain valid for another 24 hours. We recommend modifying your business configuration accordingly as soon as possible.

## Modifying the Private IP
You can modify the private IP of a TencentDB instance in VPC.
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> next to **Private IP** to modify it. You can do so only when the current subnet has available IPs.
![](https://main.qcloudimg.com/raw/25931632d09fe7f90719db45bdaad8b5.png)
3. In the pop-up dialog box, modify the private IP and click **OK**.

## Switching between VPC Subnets
You can switch an instance between VPC subnets.
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Change Subnet** next to **Network**.
3. In the pop-up dialog box, select a subnet, select **Auto-assign IP** or **Specify IP**, and click **OK**.
>?
>- The original VIP address remains valid for another 24 hours after the VPC is modified. Please modify your business IP address accordingly within 24 hours.
>- As TDSQL for MySQL supports an intra-region active-active architecture, we recommend that you choose a VPC subnet in the same region as your business server or the primary database node.
>
![](https://main.qcloudimg.com/raw/c228774130d9932505ae8661d5a7e4fe.png)

## Switching between VPCs
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Change Subnet** next to **Network**.
3. In the pop-up dialog box, select a VPC and a subnet, select **Auto-assign IP** or **Specify IP**, and click **OK**.
>?
>- The original VIP address remains valid for another 24 hours after the VPC is modified. Please modify your business IP address accordingly within 24 hours.
>- As TDSQL for MySQL supports an intra-region active-active architecture, we recommend that you choose a VPC subnet in the same region as your business server or the primary database node.


## Switching from a Classic Network to a VPC
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Switch to VPC** next to **Network**.
![](https://main.qcloudimg.com/raw/5d7751c75d3d8109b33f4676e414e42c.png)
3. In the pop-up dialog box, select a VPC and a subnet, select **Auto-assign IP** or **Specify IP**, and click **OK**.
>!
>- The switch from classic network to VPC is irreversible.
>- After the switch, VPC access will take effect immediately. The original classic network access will be retained for 24 hours; therefore, other instances associated to the TDSQL for MySQL instance should be migrated to VPC within 24 hours so as to guarantee uninterrupted access.
>- As TDSQL for MySQL supports an intra-region active-active architecture, we recommend that you choose a VPC subnet in the same region as your business server or the primary database node.
>
