## Scenario

This document describes how to change a public IP address. There are two different ways:
- [Replace public IP directly](#ReplacementPublicIP)
- [First convert to Elastic Public IP, and then unbind Elastic Public IP](#ReplacementEIP)

## Notes
If you choose to **replace public IP directly**, please note the following items:
- At most 3 times/day per account per region.
- One instance can **only replace a public IP one time**.
- **The previous public IP will be released after replacement.**

If you choose to **convert to Elastic Public IP first, and then unbind Elastic Public IP**, please note the following items:
- When an EIP is bound to a CVM instance, the current public IP address of the instance will be released.
- The Elastic Public IP quota per account per region is 20.
- In order to ensure the effective use of IP resources, EIPs that are not bound to CVMs will incur an idle fee, which is billed on hourly basis.
For details on EIP billing rules, see [Billing for Elastic Public IP](http://intl.cloud.tencent.com/document/product/213/17156).

## Prerequisites

- Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index).

## Directions

<span id="ReplacementPublicIP"></span>
### Method 1: Replace public IP directly

1. On the instance management page, select the CVM column of the IP you want replace and click **More** > **IP/ENI** > **Change Public IP**, as shown below:
![](https://main.qcloudimg.com/raw/4225bd84b4cf4d5346ddc77a1d7fd0df.png)
2. In the pop-up “Change IP” box, click  **Confirm** to complete the replacement of the IP.

<span id="ReplacementEIP"></span>
### Method 2: First convert to Elastic Public IP, and then unbind Elastic Public IP

#### Coverting to Elastic Public IP
1. On the instance management page, select the CVM column of the IP you want to replace and click <img src="https://main.qcloudimg.com/raw/25e8c0e37b73c12da900301f03e57dbc.png" style="margin: 0;"></img>, as shown below:
![](https://main.qcloudimg.com/raw/53b608b2bb0840920703e7f50957611a.jpg)
2. In the pop-up “Convert to EIP” box, click  **OK**.

#### Unbinding EIPs
1. After converting the EIP back to a public network IP, click **More**> **IP/ENI** > **Unbind Elastic IP** in the CVM column, as shown below.
![](https://main.qcloudimg.com/raw/dc5f3554b7b73bd554f596b9168839fc.png)
2. In the pop-up “Unbind EIP” box, tick **A free public IP will be assigned after unbinding (note: the public IP is randomly assigned and cannot be unbound from the instance)**, and click **OK**.
3. In the pop-up box, click **OK** to complete the replacement.

#### Releasing EIP (Optional)
> The unbound EIP is still kept under your account and incurs idle fees. To avoid such charges, we recommended you perform the following operations to release EIPs unbound from instances.
>
1. In the left sidebar, click **[EIP](https://console.cloud.tencent.com/cvm/eip)** to open the EIP management page.
2. Select the unbound EIP on the EIP management page, and click **More** > **Release**.
3. In the pop-up box, tick **Release the above EIPs** and click **Release** to release the EIP.


