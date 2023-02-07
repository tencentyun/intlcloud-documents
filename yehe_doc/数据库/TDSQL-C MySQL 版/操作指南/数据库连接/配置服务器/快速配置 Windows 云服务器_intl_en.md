CVM is a scalable cloud computing service that frees you from estimation of resource usage and upfront investment. You can start CVM instances and deploy applications immediately.

This document describes how to purchase and configure a Windows CVM instance from scratch in the simplest way. For more information on how to create a Linux CVM instance, see [Quickly Configuring Linux CVM Instance](https://www.tencentcloud.com/document/product/1098/52632).

## Prerequisites
You have registered a Tencent Cloud account as instructed in [Account Registration](https://www.tencentcloud.com/document/product/1098/50173).

## Configuring a Windows CVM Instance
>!To ensure successful connection to TDSQL-C for MySQL, the purchased CVM and TDSQL-C for MySQL instances must be:
>- Under the same Tencent Cloud root account.
>- In the same region.
>- In the same VPC.
>

### Step 1. Purchase a Windows CVM instance
1. Go to the [quick purchase page](https://buy.cloud.tencent.com/cvm?tab=lite&ltCreateMode=createLt).
2. On the purchase page, select the **Quick Configuration** tab, configure the CVM instance, and click **Buy Now**.
The configuration is as described below:
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tr>
<td>Region</td>
<td>Select the same region as your TDSQL-C for MySQL cluster.</td></tr>
<tr>
<td>Instance</td>
<td>Select the CVM model configuration as needed, which is "General (2-core, 4 GB)" here for example.</td></tr>
<tr>
<td>Operating System</td>
<td>Select the CVM operating system as needed, which is "Windows Server 2012 R2 Datacenter Edition 64-bit" here for example.</td></tr>
<tr>
<td>Public IP</td>
<td>After this option is selected, a public IP will be assigned to your instance. The default public network bandwidth is "1 Mbps", which can be adjusted as needed. </td></tr>
<tr>
<td>Login Methods</td>
<td>After creating a CVM instance, you can obtain the random password in the <a href="https://console.cloud.tencent.com/message">Message Center</a>.</td></tr>
<tr>
<td>Default configuration</td>
<td>Six default configuration items can be expanded, such as AZ and security group.</td></tr>
<tr>
<td>Auto-renewal</td>
<td>After this option is selected, if your account balance is sufficient, the CVM instance will be automatically renewed by month upon expiration.</td></tr>
<tr>
<td>Agreements</td>
<td>Read and indicate your consent to the relevant agreements.</td></tr>
<tr>
<td>Period</td>
<td>Select the purchase period, which is "1 month" by default.</td></tr>
<tr>
<td>Quantity</td>
<td>Select the quantity, which is "1" by default.</td></tr>
</table>

After you make the payment, the CVM instance will be successfully purchased. It can be used as a personal virtual machine or website server. Next, you can log in to it.

### Step 2. Log in to the CVM instance
>!After you purchase a quickly configured CVM instance, the system will automatically generate a login password and sent it to you in the [Message Center](https://console.cloud.tencent.com/message). This password is the credential for logging in to the CVM instance.

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, proceed according to the actually used view mode:
<dx-tabs>
::: List view
Locate the Windows CVM instance you want to log in to and click **Log In** on the right as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Y63K562_12.png)

:::
::: Tab view
Locate the Windows CVM instance you want to log in to and click **Log In** as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ejMN656_13.png)

:::
</dx-tabs>
3. In the **Standard Login | Windows Instance** window that is opened, enter the login information according to the actual situation.
 - **Port**: The default port is 3389. Enter a value as needed.
 - **Username**: The default username of Windows instances is `Administrator`. Enter a value as needed.
 - **Password**: Enter the login password obtained in the [Message Center](https://console.cloud.tencent.com/message).
5. Click **Log In** to log in to the Windows instance.
This document uses logging in to a CVM instance on Windows Server 2016 Datacenter Edition 64-bit as an example. If the login is successful, a page similar to the following will appear:

