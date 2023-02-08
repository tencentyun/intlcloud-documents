CVM is a scalable cloud computing service that frees you from estimation of resource usage and upfront investment. You can start CVM instances and deploy applications immediately.

This document describes how to purchase and configure a Linux CVM instance from scratch in the simplest way. For more information on how to create a Windows CVM instance, see [Quickly Configuring Windows CVM Instance](https://www.tencentcloud.com/document/product/1098/52633).

## Prerequisites
You have registered a Tencent Cloud account as instructed in [Account Registration](https://www.tencentcloud.com/document/product/1098/50173).

## Configuring a Linux CVM Instance
>!To ensure successful connection to TDSQL-C for MySQL, the purchased CVM and TDSQL-C for MySQL instances must be:
>- Under the same Tencent Cloud root account.
>- In the same region.
>- In the same VPC.
>

### Step 1. Purchase a Linux CVM instance
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
<td>Select the CVM operating system as needed, which is "CentOS 8.2 64-bit" here for example.</td></tr>
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

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index) and select a region at the top.
2. Find the CVM instance you purchased in the instance list and click **Log In** in the **Operation** column on the right.
3. In the **Standard Login | Linux Instance** window, enter the username (which is `root` by default) and password of the **CVM instance** and click **Log In**.
4. After successful login, the UI is as shown below:
