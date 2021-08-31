## Operation Scenario

Security group is a virtual firewall for filtering packets and is used to set the network access controls for one or multiple CVMs. It is an important network security isolation method provided by Tencent Cloud. When creating a CVM instance, you must configure a security group for it. Tencent Cloud allows you to configure a new security group for the CVM instance after it is created.
> To configure a new security group for the instance, create a security group first. For more information, please see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/213/34271).

## Prerequisites

Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).

## Directions

### Change the configured security group

To improve your experience on the CVM Console, security group can be configured on the instance management page or on the instance details page.

#### Configuring a security group on the instance management page

1. Select a CVM to be reassigned to a new security group on the instance management page and click **More** > **Security Groups** > **Configure Security Groups**, as shown below:
![](https://main.qcloudimg.com/raw/68a30faac347446e57d87e8a1c30ef11.png)
2. On the “Configure Security Group” pop-up window, check the name of the new security group (multiple names can be selected) and click **Confirm** to change the security group.
 
#### Configuring a security group on the instance details page
 
1. On the instance management page, click the CVM instance ID/name for which you want to change the security group and enter the instance details page.
2. Click **More Actions** > **Security Groups** > **Configure Security Groups** on the upper right corner of the instance details page, as shown below:
![](https://main.qcloudimg.com/raw/c7a1d76159feaa66f52eb16c7787432d.png)
3. On the “Configure Security Group” pop-up window, check the name of the new security group (multiple names can be selected) and click **Confirm**.

### Change the bound security group

1. On the instance management page, click the CVM instance ID/name for which you want to bind the security group and enter the instance details page.
2. On the instance details page, select the **Security Groups** tab and click **Bind** on the “Bound to security group” column, as shown below:
![](https://main.qcloudimg.com/raw/2ea553a1f2f589c6202245addfd62523.png)
3. On the “Security Groups” pop-up window, check the name of the security group (multiple names can be selected) to be bound based on your actual needs and click **OK** to bind the security group.
![](https://main.qcloudimg.com/raw/ac58322e8b11db8497d79eb54ecc67f6.png)
