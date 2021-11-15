This document describes how to change the instance network type and modify the instance access address.

>!Modifying the network configurations of an instance is highly risky. Please do so only during off-peak hours. After modification, unless assigned to another service, the original IP will remain valid for another 24 hours. We recommend modifying your business configuration accordingly as soon as possible.

## Modifying the Private IP
You can modify the private IP of a TencentDB instance in VPC.
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> next to **Private IP** to modify it. You can do so only when the current subnet has available IPs.
![](https://main.qcloudimg.com/raw/5a433d6cb4da6d698127e833a0030682.png)
3. In the pop-up dialog box, modify the private IP and click **Confirm**.

## Switching between VPC Subnets
You can switch an instance between VPC subnets.
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Change Subnet** next to **Network**.
3. In the pop-up dialog box, select a subnet, select **Auto-assign IP** or **Specify IP**, and click **Comfirm**.
>?
>- The original VIP address remains valid for another 24 hours after the VPC is modified. Please modify your business IP address accordingly within 24 hours.
>- Because the product supports an intra-city active-active architecture, you are recommended to choose a VPC subnet in the same region as your business server or primary node.
>
![](https://main.qcloudimg.com/raw/afd3097e7843720ea4233baf90ea195c.png)

## Switching between VPCs
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Change Subnet** next to **Network**.
3. In the pop-up dialog box, select a VPC, select **Auto-assign IP** or **Specify IP**, and click **Comfirm**.
>?
>- The original VIP address remains valid for another 24 hours after the VPC is modified. Please modify your business IP address accordingly within 24 hours.
>- Because the product supports an intra-city active-active architecture, you are recommended to choose a VPC subnet in the same region as your business server or primary node.

## Switching from a Classic Network to a VPC
You can switch an instance from classic network to VPC.
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Switch to VPC** next to **Network**.
![](https://main.qcloudimg.com/raw/ac63e63a44a39dcaf23e4d40865c2c1a.png)
3. In the pop-up dialog box, select a VPC, select **Auto-assign IP** or **Specify IP**, and click **Comfirm**.
>!
>- The switch from classic network to VPC is irreversible.
>- After the switch, VPC access will take effect immediately. The original classic network access will be retained for 24 hours; therefore, other instances associated to the TencentDB for MySQL instance should be migrated to VPC within 24 hours so as to guarantee uninterrupted access.
>- Because the product supports an intra-city active-active architecture, you are recommended to choose a VPC subnet in the same region as your business server or primary node.
>
