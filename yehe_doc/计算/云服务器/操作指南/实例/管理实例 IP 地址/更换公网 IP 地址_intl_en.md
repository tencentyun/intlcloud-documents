## Scenario

This document describes how to replace a public IP address. This can be done in two ways:
- [Directly replacing a public IP address](#ReplacementPublicIP)
- [Changing to an EIP and then unbinding the EIP](#ReplacementEIP)

## Notes
If you choose to **directly replace a public IP address**, note that:
- The upper limit for a single account in a region is 3 times per day.
- One instance can **replace the public IP address only once**.
- **After replacement, the original public IP address will be released.**

If you choose to **change to an EIP and then unbind the EIP**, note that:
- When an EIP is bound to a CVM instance, the current public IP address of the instance will be released.
- The quota of EIPs for one account in a single region is 20.
- EIPs that are not bound to CVMs will incur an idle fee, which is billed on an hourly basis.
For information on EIP billing, see [EIP Billing](http://intl.cloud.tencent.com/document/product/213/17156).

## Prerequisites

You have logged in to the [CVM console](https://console.cloud.tencent.com/cvm/index).

## Directions

<span id="ReplacementPublicIP"></span>
### Method 1: Directly replacing a public IP address

1. On the instance management page, select the row of the CVM whose public IP address is to be changed, and choose **More** > **IP/ENI** > **Replace Public IP**.
2. In the "Replace IP" window that appears, click **OK** to finish the replacement.

<span id="ReplacementEIP"></span>
### Method 2: Changing to an EIP and then unbinding the EIP

#### Changing to an EIP
1. On the instance management page, select the row of the CVM whose public IP address is to be changed, and click <img src="https://main.qcloudimg.com/raw/25e8c0e37b73c12da900301f03e57dbc.png" style="margin: 0;"></img>.
2. In the "Convert to EIP" window that appears, click **Convert**.

#### Unbinding the EIP
1. After the conversion is completed, choose **More** > **IP/ENI** > **Unbind EIP** in the row for the CVM.
2. In the "Unbind EIP" window that appears, select **Assign Free Public IP After Unbinding** (note that the public IP address will be randomly assigned and cannot be unbound from the CVM), and click **OK**.
3. In the window that appears, click **OK** to finish the replacement.

#### (Optional) Releasing the EIP
> As unbound EIPs are retained under your account and incur idle fees, to avoid such fees, we recommend that you complete the following steps to release EIPs unbound from instances.
>
1. In the left sidebar, click **[EIP](https://console.cloud.tencent.com/cvm/eip)** to go to the EIP management page.
2. On the EIP management page, select the EIP you just unbound and choose **More** > **Release**.
3. In the "Are you sure you want to release the EIP?" window that appears, select **Confirm release of the above IP** and click **Release**.


