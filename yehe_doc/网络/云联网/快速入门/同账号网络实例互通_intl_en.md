 CCN connects a VPC with another or with IDCs. This document introduces how to use CCN to interconnect VPCs in Guangzhou and Shanghai regions under the same account.

> This feature is currently in beta test. To use it, please [contact sales](https://intl.cloud.tencent.com/contact-sales).

## Background
When creating a CCN instance, you can select either of the billing mode as needed: monthly subscription or monthly 95th percentile pay-as-you-go. The instance creation varies by the billing mode, as shown below:
![](https://main.qcloudimg.com/raw/f0fe23c7fbe4afa675bfb76b435726bf.png)
This document guides you through how to interconnect a VPC in Guangzhou with a VPC in Shanghai under the same account.

## Prerequisites

You have created VPCs, subnets and CVMs in Shanghai and Guangzhou regions. The two subnets have no duplicate IP ranges, and CVMs reside in the subnets. For the step-by-step instructions, see [Building Up a IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).


<span id="1"></span>
## Step 1: create a CCN instance
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
3. Click **Cloud Connect Network** in the left sidebar to go to the **CCN** page, and then click **+New**.
4. In the **Create CCN instance** dialog box, complete the following configurations, and click **OK**.

 <table>
 <thead>
 <tr>
  <th>Field</th>
  <th>Subfield</th>
  <th>Description</th>
 </tr>
  </thead>
 <tr>
  <td align="center">Name</td>
   <td align="center">-</td>
  <td >Name of the CCN instance.</td>
 </tr>
 <tr >
  <td rowspan=2 align="center" >Billing Mode</td>
  <td align="center" >Monthly subscription</td>
  <td>Its unit price is about 20% lower than that of monthly 95th percentile billing. It's applicable to business with stable bandwidth needs.</td>
 </tr>
 <tr >
  <td align="center" style='white-space:nowrap'>Monthly 95th percentile</td>
  <td>Bill the actual bandwidth usage of the current month on 95th percentile basis. It's applicable to business with fluctuating bandwidth demands.</td>
 </tr>
 <tr>
  <td rowspan=3 align="center">Service Quality</td>
  <td align="center">Platinum</td>
  <td>It’s ideal for key businesses that require extremely high communication quality. Gold service is suitable for businesses that require high communication quality, such as payment and game acceleration./td>
 </tr>
 <tr>
  <td align="center" white-space="nowrap">Gold</td>
  <td >It’s suitable for businesses that require transmission of key business data, such as enterprise business data and ERP.</td>
 </tr>
 <tr >
  <td align="center">Silver</td>
  <td >It’s suitable for cost-sensitive and jitter-insensitive businesses that require high security./td>
 </tr>
 <tr>
  <td rowspan=2>Speed Limit Mode</td>
  <td align="center" style='white-space:nowrap'>Region outbound speed limit</td>
  <td >The overall outbound bandwidth limit from one region to another.</td>
 </tr>
 <tr>
  <td align="center" style='white-space:nowrap'>Inter-region speed limit</td>
  <td >It’s the total bandwidth limit for traffic from a certain region to other regions. A monthly subscription CCN instance only supports the inter-region speed limit.</td>
 </tr>
 <tr>
  <td   align="center">Associate with Instance</td>
  <td   align="center">-</td>
  <td >The options include VPC, Direct Connect Gateway, BM Virtual Private Cloud, and VPN Gateway.
  In this example, we choose to associate with VPC in the Shanghai region.</td>
 </tr>
</table>

<span id="2"></span>
Step 2: associate a network instance
To associate a VPC in the Guangzhou region with CCN, do as follows:
1. On the **CCN** page, click the ID/Name of the CCN you want to associate with.
2. On the **Associate with Instance** page, click **Add an instance**. 
3. In the **Associate with Instance** dialog box, choose to associate the VPC instance in the Guangzhou region.

>? If you need to associate another network instance, click **Add**.

4. Click **OK** to add the selected network instances to CCN.

<span id="3"></span>
Step 3: check the route table

Check and confirm that routing policies of each subnet in the VPC associated with the CCN take effect. Any IP range conflicts between associated network instances will invalidate routes.
1. On the **CCN** page, click ID/Name of the CCN instance for which you want to query the route table.
2. Select the **Route table** tab on the details page of the CCN instance to view its route tables.
3. Check for route in **invalid** status. If any, [modify the route](https://intl.cloud.tencent.com/document/product/1003/30052) and [enable it](https://intl.cloud.tencent.com/document/product/1003/30069).
![](https://main.qcloudimg.com/raw/e802fd5a736644e0a6dc2757400adbf1.png)

##Step 4: configure the bandwidth
-**Purchasing bandwidth in both regions (only for monthly subscription CCN instances)**
For monthly subscription CCN instances, bandwidth of 10 Kbps or less is free of charge in any region. If you need a higher bandwidth, purchase it according to regions.
   1. On the **CCN** page, click ID/Name of the CCN instance for which you want to purchase a bandwidth.
   2. Select the **Bandwidth Management** tab on the details page of the CCN instance, and click **Purchase Bandwidth**.
      3. On the **Purchase Bandwidth** dialog box, choose Guangzhou and Shanghai regions, configure the bandwidth cap and validity period, and click **Confirm**.


- **Setting cross-region bandwidth limit (only for monthly 95th percentile CCN instance)**
You can set the cross-region bandwidth cap for monthly 95th percentile CCN instances as needed:
>?The default bandwidth cap is 1 Gbps. If you want to increase the bandwidth, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
 - Setting inter-region bandwidth speed limit
Click **Change Bandwidth** to go to the **Change Bandwidth** page. In the pop-up window, select the two regions where you want to limit the bandwidth, and enter the **Bandwidth Cap**. If you need to add more entries, click **Add**, and then click**OK** to complete the configurations.
 - Setting region outbound bandwidth speed limit
Click **Adjust bandwidth speed limit**. In the pop-up window, select regions for which you want to limit the bandwidth on the left, enter the **Bandwidth Cap** on the right, and click **OK** to complete the configurations.

>?Communications between CCN instances may incur fees. For pricing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

## Result Validation
Log in to a CVM in Shanghai region, and run the `ping <IP address>` to connect the CVM in Guangzhou region. If the following result appears, the two CVMs are successfully connected. 
