When the system-assigned IP addresses are insufficient, you can apply for a public IP range in the console for Internet tunnel to meet your business requirements. This document describes how to apply for and manage public IP ranges.

## Public IP Range Lifecycle
![](https://main.qcloudimg.com/raw/ebb4ee3321c34679d0970b95c6247dfb.svg)
1. [Apply for a public IP range](#creat): after your application is submitted in the console, a public IP range will be automatically assigned. The status of this public IP range will become “In use”.
2. A public IP range in use can be split or disabled.
   - [Split an IP range](#wdcf): applicable to the scenario requiring a refined IP range. The public IP range is still in use.
   - [Disable a public IP range](#tygw): the public IP range is disabled.
3. A disabled public IP range can be enabled or released.
   - [Enable a public IP range](#qygw): the public IP range reverts to the “In use” status.
   - [Release a public IP range](#thgw): the public IP range is released.
4. [Recover a public IP range](#refound): a public IP range that has been released in the last eight days can be recovered, which will be reassigned and resumed the “In use” status.

## Prerequisites
You have applied for an Internet tunnel as instructed in [Creating an Internet Tunnel](https://intl.cloud.tencent.com/document/product/216/39107).

<span id ="creat"></span>
## Applying for a Public IP Range
The public IP range will be automatically bound to the Internet tunnels in the same region.
1. Choose **Internet Tunnels** > **Public IP Range** on the left sidebar.
2. Select a region at the top of the page and click **Apply**.
3. In the pop-up dialog box, configure the following parameters.

<table>
<tr>
<th width="10%">Field</th>
<th>Description</th>
</tr>
<tr>
<td>Protocol type</td>
<td>Select either <b>IPv4</b> or <b>IPv6</b>. To apply for an IPv6 address, the Internet tunnel should have IPv6 enabled.</td>
</tr>
<tr>
<td>IP address type</td>
<td><ul><li>For IPv4: select either <b>BGP</b> or <b>Static</b>. You also need to select a provider from <b>CTCC</b>, <b>CUCC</b>, and <b>CMCC</b> for <b>Static</b>.</li><li>For IPv6: only <b>BGP</b> is supported.</li></td>
</tr>
<tr>
<td>Quantity</td>
<td>Specify the number (at least four) of IP addresses you want to apply for. Each Tencent Cloud account can have up to 512 addresses.</td>
</tr>
<tr>
<td>Mask</td>
<td>Customize a mask length, which cannot exceed 64 bits.</td>
</tr>
</table>

4. Click **OK**.

<span id ="wdcf"></span>
## Splitting IP Ranges
You can split IP ranges as follows if a refined IP range is required. To split IP ranges, ensure the mask of an IPv4 address is less than 30, and that of an IPv6 address is less than 64.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and choose **Internet Tunnels** > **Public IP Range** on the left sidebar.
2. Select a region at the top of the page
3. Locate the public IP range to be split, and click **Split IP Range** under the **Operation** column.

4. Specify the number of IP ranges to split into, check **Confirm to split IP range**, and click **Split**.
    >! Change the published IP range to split CIDR block; otherwise, the network may be interrupted.
    >


<span id ="tygw"></span>
## Disabling a Public IP Range
After disabling a public IP range, the associated four IPs cannot access the public network.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and choose **Internet Tunnels** > **Public IP Range** on the left sidebar.
2. Select a region at the top of the page.
3. Locate the public IP range to be disabled, and click **Disable** under the **Operation** column.

4. In the pop-up dialog box, check **Confirm to disable the above IP addresses**, and click **Disable** to disable the four addresses of the IP range.
		

<span id ="qygw"></span>
## Enabling a Public IP Range
Follow the steps below to enable a public IP range.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and choose **Internet Tunnels** > **Public IP Range** on the left sidebar.
2. Select a region at the top of the page.
3. Locate the public IP range to be enabled, and click **Enable** under the **Operation** column.

4. In the pop-up dialog box, check **Confirm to enable the above IP addresses**, and click **Enable** to enable the four addresses of the IP range.

<span id ="thgw"></span>
## Releasing a Public IP Range
Only a disabled public IP range can be released.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and choose **Internet Tunnels** > **Public IP Range** on the left sidebar.
2. Select a region at the top of the page.
3. Locate the public IP to be released, and click **Release** under the **Operation** column.

4. In the pop-up dialog box, check **Confirm to release the above IP addresses**, and click **Release**.

<span id ="refound"></span>
## Recovering a Public IP Range
A public IP range released within 8 calendar days is recoverable. The recovered public IP range is enabled by default.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and choose **Internet Tunnels** > **Public IP Range** on the left sidebar.
2. Select a region at the top of the page.
3. Locate the public IP to be recovered, and click **Recover** under the **Operation** column.

4. In the pop-up dialog box, check **Confirm to recover the above IP addresses**, and click **Recover**.
