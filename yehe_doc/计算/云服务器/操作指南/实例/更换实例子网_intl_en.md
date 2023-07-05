## Overview
This document describes how to change the subnet of a CVM instance in VPC via the console.

## Limits

- The associated CVM restarts automatically after its subnet is changed.
- The subnet of secondary ENI cannot be changed.

## Directions

1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In **Instances**, select the region where the instance whose subnet needs to be changed belongs.
3. Locate the instance whose subnet needs to be changed, click its ID/Name and enter the instance details page.
4. Select the **ENI** tab, click the ID of the primary ENI, 
and enter the ENI management page, as shown below:
![](https://main.qcloudimg.com/raw/feeec3ecd76a2f5710d1b775b9f7f1d9.png)
5. Click **Change Subnet**, as shown below:
![](https://main.qcloudimg.com/raw/713d6383b128a66ae25f5342a7387631.jpg)
6. Select a new subnet in the pop-up box. Enter a new IP, and click **OK**, as shown below:
The configuration will take effect after the instance is restarted.
>! 
> - Create a subnet if no subnet can be found in this availability zone.
> - Only the private IP address of the current subnet CIDR can be used as the new IP.
>
![](https://main.qcloudimg.com/raw/58c3534b2d6c9da255c5a32bbde8a4c1.png)
