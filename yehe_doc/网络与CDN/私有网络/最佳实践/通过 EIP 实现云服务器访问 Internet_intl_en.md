An EIP is a region-level static public IP. It can connect a VPC-based CVM instance to the public network. This document describes how to bind an EIP to a CVM instance for public network access.

## Overview
A VPC-base CVM instance, if you do not allocate a public IP when purchasing it, it cannot access to the public network. 
However you can bind an EIP to the CVM instance to access the public network.
![]()

## Directions
### Step 1. Apply for an EIP
>?If you already have an idle EIP, you can skip this step and proceed to [Step 2](#step2).
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/).
2. Click **IP and ENI** > **Public IP/EIP** to enter the public IP page.
3. At the top of the **Public IP/EIP** page, select the same region as the CVM instance and click **Apply**.
<img src="" width="50%">
4. In the **Apply for EIP** pop-up window, configure the parameters as needed and click **OK**. For more parameter descriptions, see [Applying for EIP]().
<img src="" width="50%">

### Step 2. Bind an EIP to the CVM instance[](id:step2)
1. On the **Public IP/EIP** page, select **More** > **Bind** on the right of the EIP.
 <img src="" width="70%">
2. In the **Bind resources** pop-up window, select **CVM instance**, select your CVM instance ID, and click **OK**.
 <img src="" width="70%">

### Step 3. Verify the public network access through the EIP
1. Go to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1), click **Login** on the right of the CVM instance, and enter the password to access the CVM UI.
2. Run `ping www.qq.com` to test the data connectivity. If data is returned, the CVM instance can access the public network.
    ![](https://main.qcloudimg.com/raw/40c8b66f305baac0a63858394ed88766.png)
