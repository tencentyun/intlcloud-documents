
This document describes how to modify the private IP used by your business to access the TencentDB instances and how to change the network type.

>!Modifying the private IP of an instance is highly risky. Please do so only during off-peak hours. After modification, unless assigned to another service, the original IP will remain valid for another 24 hours. We recommend modifying your business configuration as soon as possible.

## Modifying the Private IP
You can modify the private IP of a TencentDB instance in VPC.
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID/name in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> next to **Private IP** to modify it. You can do so only when the current subnet has available IPs.
![](https://main.qcloudimg.com/raw/5a433d6cb4da6d698127e833a0030682.png)

## Switching from Classic Network to VPC
You can switch an instance from classic network to VPC.
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID/name in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Switch to VPC** next to **Network**. You can do so only when the target VPC subnet has available IPs.
>!Because the product supports an intra-city active-active architecture, you are recommended to choose a VPC subnet in the same region as your business server or primary node.

## Switching between VPC Subnets
You can switch an instance between VPC subnets.
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID/name in the instance list, and enter the instance details page.
2. In the **Basic Info** section, click **Change Subnet** next to **Network**. You can do so only when the target VPC subnet has available IPs.

