## Overview
Security group is a virtual firewall for filtering packets and is used to set the network access controls for one or multiple CVMs. It is an important network security isolation method provided by Tencent Cloud. When creating a CVM instance, you must configure a security group for it. Tencent Cloud allows you to configure a new security group for the CVM instance after it is created.

<dx-alert infotype="notice" title="">
To configure a new security group for the instance, create a security group first. For more information, please see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/213/34271).
</dx-alert>



## Prerequisites
You have logged in to [CVM Console](https://console.cloud.tencent.com/cvm/index).

## Directions
### Change the configured security group
On the instance management page, proceed according to the actually used view mode:
<dx-tabs>
::: List mode
1. On the instance management page, select a CVM instance for which a new security group needs to be configured. Click **More** > **Security Group** > **Configure Security Group**, as shown below:
![](https://main.qcloudimg.com/raw/68a30faac347446e57d87e8a1c30ef11.png)
2. In the pop-up window, check the name of the new security group (multiple names can be selected) and click **Confirm** to change the security group.

:::
::: Tab mode
1. On the instance management page, select a tab of the CVM instance for which a new security group needs to be configured.
2. On the instance details page, click **More** > **Security Group** > **Configure Security Group**, as shown below:
![](https://main.qcloudimg.com/raw/c7a1d76159feaa66f52eb16c7787432d.png)
3. In the pop-up window, check the name of the new security group (multiple names can be selected) and click **Confirm**.

:::
</dx-tabs>

### Change the bound security group

1. On the instance management page, click the CVM instance ID/name for which you want to bind the security group and enter the instance details page.
2. On the instance details page, select the **Security Groups** tab and click **Bind** on the "Bound to security group" column, as shown below:
![](https://main.qcloudimg.com/raw/2ea553a1f2f589c6202245addfd62523.png)
3. In the pop-up window, check the name of the security group (multiple names can be selected) to be bound based on your actual needs and click **OK** to bind the security group, as shown below:
![](https://main.qcloudimg.com/raw/ac58322e8b11db8497d79eb54ecc67f6.png)

