 Communications between two VPCs or between a VPC and an IDC can be implemented through CCN. This document describes how to use a CCN instance to interconnect VPCs in the Guangzhou and Shanghai regions under the same account.

## Background
You can create a pay-as-you-go CCN instance billed by monthly 95 percentile.
![](https://main.qcloudimg.com/raw/23e11b65f008292a6803ffe53fc786d1.png)
This document guides you through how to interconnect a VPC in Guangzhou with a VPC in Shanghai under the same account.
## Prerequisites

You have created VPCs, subnets and CVMs in the Shanghai and Guangzhou regions. The two subnets have no duplicate IP ranges, and CVMs reside in the subnets. For the step-by-step instructions, see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).


## Step 1. Create a CCN Instance[](id:1)
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn).
2. Click **Create** at the top of the CCN management page.
3. In the **Create CCN instance** dialog box, complete the following configurations, and click **OK**.
![](https://main.qcloudimg.com/raw/67e42dd8cb0f3c2d509e59bcfc24df0a.png)
 <table>
 <thead>
 <tr>
  <th width="15%">Field</th>
  <th >Subfield</th>
  <th >Description</th>
 </tr>
  </thead>
 <tr>
  <td align="center">Name</td>
   <td   align="center">-</td>
  <td >Name of the CCN instance.</td>
 </tr>
 <tr>
  <td  align="center" >Billing mode</td>
  <td align="center" style='white-space:nowrap'>Pay-as-you-go by monthly 95 percentile</td>
  <td>Bill the actual bandwidth usage of the current month on 95th percentile basis. It's applicable to business with fluctuating bandwidth demands.</td>
 </tr>
 <tr>
  <td rowspan=3 align="center">Service level</td>
  <td align="center">Platinum</td>
  <td>It’s ideal for key businesses that require extremely high communication quality. Gold service is suitable for businesses that require high communication quality, such as payment and game acceleration.</td>
 </tr>
 <tr>
  <td align="center" white-space="nowrap">Gold</td>
  <td >It’s suitable for businesses that require transmission of key business data, such as enterprise business data and ERP.</td>
 </tr>
 <tr>
  <td align="center">Silver</td>
  <td >It’s suitable for cost-sensitive and jitter-insensitive businesses that require high security.</td>
 </tr>
 <tr>
  <td>Limit method</td>
   <td align="center" style='white-space:nowrap'>Inter-region bandwidth cap</td>
  <td>The inbound and outbound bandwidth cap between two regions.</td>
 </tr>
 <tr>
  <td   align="center">Associated instances</td>
  <td   align="center">-</td>
  <td >The options include VPC, direct connect gateway, BM virtual private cloud, and VPN gateway.
  In this example, we choose to associate with a VPC in the Shanghai region.</td>
 </tr>
</table>

## Step 2. Associate Instances[](id:2)
To associate a VPC in the Guangzhou region with CCN, perform the following steps.
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn), and click the ID/Name of the target CCN instance to open its details page.
2. Select the **Associated instances** tab, and click **Add an instance**. 
3. In the **Associated instances** dialog box, choose to associate the VPC instance in the Guangzhou region.
>?If you need to associate another network instance, click **Add**.
>
![](https://main.qcloudimg.com/raw/02cb17c3741827d4f01cecda590dd381.png)
4. Click **OK** to add the selected network instance to CCN.


## Step 3. Check the Route Table[](id:3)
Check and confirm that routing policies of all subnets in the VPC associated with the CCN instance are valid. Any IP range conflicts between associated network instances will invalidate routes.
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn), and click the ID/Name of the target CCN instance.
2. Select the **Route table** tab on the details page of the CCN instance to view its route tables.
3. Check if there is any **invalid** routing policy. If so, modify the route table according to [route limits](https://intl.cloud.tencent.com/document/product/1003/30052), and then [enable it](https://intl.cloud.tencent.com/document/product/1003/30069).
![](https://main.qcloudimg.com/raw/30e2fa3a3d0948d3dad64045040fff9f.png)

## Step 4. Configure Bandwidth
- **Setting the cross-region bandwidth cap (only for pay-as-you-go CCN instances billed by monthly 95th percentile)**
For pay-as-you-go CCN instances billed by monthly 95 percentile, you can configure a cross-region bandwidth cap as needed, including inter-region bandwidth limit and region outbound bandwidth limit.
>?
>- The pay-as-you-go by monthly 95 percentile mode is currently in beta. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- The default bandwidth cap is 1 Gbps. To increase the bandwidth, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
 1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn), and click the ID/Name of the target CCN instance.
 2. Select the **Bandwidth management** tab on the details page of the CCN instance.
 3. (Optional) Click **Change**, and select the bandwidth limit mode as needed.
 ![](https://main.qcloudimg.com/raw/b721393fb8cb95e9ebb14ee8c3db1536.png)
> !Changing the bandwidth limit mode will delete existing configurations. The bandwidth cap will be set to 1 Gbps by default. To increase the bandwidth, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
> 
       ![](https://main.qcloudimg.com/raw/e267c561ea9be180cd3dcdab451b1233.png)
 4. Configure the bandwidth cap according to the bandwidth limit mode of the CCN instance:	 
   - Setting inter-region bandwidth limit
Click **Change bandwidth**. In the pop-up window, select **Region A** and **Region B** from the drop-down list and enter the **Bandwidth cap**. You can also click **Add** to configure multiple bandwidth limit rules, and then click **OK**.
![](https://main.qcloudimg.com/raw/8985f4739ef6e55716e4d56370745365.png)
   - Setting region outbound bandwidth limit
Click **Adjust bandwidth cap**. In the pop-up window, select regions for which you want to limit the bandwidth on the left and set the bandwidth cap on the right. Click **OK**.
![](https://main.qcloudimg.com/raw/a204cb4fadc323ea81af2aa5daa00aa6.png)
>?Communication between CCN instances may incur fees. For pricing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

## Result Validation
Log in to a CVM in the Shanghai region, and run the `ping <IP address>` command to connect with the CVM in the Guangzhou region. If the following result appears, the two CVMs are connected.
<img src="https://main.qcloudimg.com/raw/85cf83efdb100080db078e4f497baf7e.png" width="70%">

