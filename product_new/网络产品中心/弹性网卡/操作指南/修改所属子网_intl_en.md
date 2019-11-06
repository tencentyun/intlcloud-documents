This document describes how to change the subnet of an ENI.
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **IP and ENI** -> **ENI** in the left sidebar to enter the ENI list page.
![](https://main.qcloudimg.com/raw/946e2598d0bccd3be9826479d3443ec7.png)
3. Click the ID of the ENI to enter its details page.
4. Click **Change Subnet** for the subnet.
![](https://main.qcloudimg.com/raw/ca5b927d392d58ffa7ff9a31dc04b809.png)
5. Select the subnet to be changed and specify a new primary IP in the pop-up window.
![](https://main.qcloudimg.com/raw/c2fea2757e7d418a00001b8751911c14.png)
6. Click **OK**.

>!
>- You can only change the subnet of the primary ENI.
>- You must unbind all secondary IPs before you change the subnet of an ENI.
>- You can only change the subnet of an ENI to another subnet within the same availability zone.
