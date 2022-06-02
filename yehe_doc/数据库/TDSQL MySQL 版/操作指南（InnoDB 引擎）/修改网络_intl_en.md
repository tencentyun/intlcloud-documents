
This document describes how to change the instance network type and modify the instance access address.

>!Modifying the network configurations of an instance is highly risky. Do so only during off-peak hours. After modification, unless the original IP is assigned to another service or a custom IP repossession time is set, the original IP will remain valid for another 24 hours by default. We recommend you modify your business configuration accordingly as soon as possible.

## Modifying Private Network Address
You can modify the private network address of a TencentDB instance in VPC.
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld) and click an instance ID in the instance list to enter the instance details page.
2. On the instance details page, click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> next to **Private Network Address** to modify it. You can do so only when the current subnet has available IPs.
![](https://main.qcloudimg.com/raw/25931632d09fe7f90719db45bdaad8b5.png)
3. In the pop-up window, modify the private network address and click **OK**.

## Switching Between VPC Subnets
You can switch a TDSQL for MySQL instance's network between VPC subnets.
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld) and click an instance ID in the instance list to enter the instance details page.
2. On the instance details page, click **Change Network** in the **Network** section.
3. In the pop-up window, select the subnet to switch to under the VPC, select **Auto-Assign IP** or **Specify IP**, set **Valid Hours of Old IP**, and click **OK**.
>?
>- The original IP address remains valid for another 24 hours by default after the network is changed. Change your business IP address accordingly within 24 hours.
>- You can also set **Valid Hours of Old IP** to 0–168 hours. If it is set to 0 hours, the IP is released immediately after the network is changed. This may affect your business.
>- As the product supports an intra-region active-active architecture, we recommend you choose a VPC subnet in the same region as your business server or the source node.
>
![](https://main.qcloudimg.com/raw/c228774130d9932505ae8661d5a7e4fe.png)

## Switching Between VPCs
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld) and click an instance ID in the instance list to enter the instance details page.
2. On the instance details page, click **Change Network** in the **Network** section.
3. In the pop-up window, select the VPC to switch to, select **Auto-Assign IP** or **Specify IP**, set **Valid Hours of Old IP**, and click **OK**.
>?
>- The original VIP address remains valid for another 24 hours by default after the network is changed. Change your business IP address accordingly within 24 hours.
>- You can also set **Valid Hours of Old IP** to 0–168 hours. If it is set to 0 hours, the IP is released immediately after the network is changed. This may affect your business.
>- As the product supports an intra-region active-active architecture, we recommend you choose a VPC subnet in the same region as your business server or the source node.
>

## Switching from Classic Network to VPC
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld) and click an instance ID in the instance list to enter the instance details page.
2. On the instance details page, click **Switch to VPC** next to **Network**.
![](https://main.qcloudimg.com/raw/5d7751c75d3d8109b33f4676e414e42c.png)
3. In the pop-up window, select a VPC, select **Auto-Assign IP** or **Specify IP**, and click **OK**.
>!
>- The switch from classic network to VPC is irreversible.
>- After the switch, VPC access will take effect immediately. The original classic network access will be retained for 24 hours; therefore, other instances associated to the instance should be migrated to VPC within 24 hours so as to guarantee uninterrupted access.
>- As the product supports an intra-region active-active architecture, we recommend you choose a VPC subnet in the same region as your business server or the source node.
>

