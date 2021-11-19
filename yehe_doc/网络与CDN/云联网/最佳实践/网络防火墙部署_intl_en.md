You have activated the CCN service, and all VPCs in your organization have been interconnected through CCN. By default, network instances added to CCN are interconnected.

In certain scenarios, you may want to control the interconnection between network instances. This can be implemented through the custom route table feature of CCN. Specifically, you can plan different custom route tables for CCN to manage business VPC interconnection with the firewall VPC.
>? The custom route table feature is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


## Overview
The network instances associated with CCN are divided into a business zone and a firewall zone, and the interconnection between network instances in the business zone is managed by the firewall VPC.
As shown below, create two custom route tables for the CCN instance: the business route table and the firewall route table.
Here:
- The business route table only receives and learns routes from the firewall VPC and is bound to the business VPC.
- The firewall route table only receives and learns routes from the business VPC and is bound to the firewall VPC.
![]()



## Prerequisites
1. You have activated the CCN service and created a CCN instance. For detailed directions, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
2. The CCN instance has been associated with 3 network instances (for verification and subject to your actual business needs). For detailed directions, please see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

## Directions

### Step 1. Plan a custom route table
According to the conditions of network zones, two custom route tables need to be planned: the business route table and the firewall route table.
The routing plan of the custom route table is as follows:
<table>
<tr>
<th >Item</th>
<th>Business route table</th>
<th>Firewall route table</th>
</tr>
<tr>
<td>Route reception policy</td>
<td>Receive the routes of the network instances in the network zone of the firewall, i.e., routes of the firewall VPC.</td>
<td>Receive the routes of the network instances in the network zone of the business, i.e., routes of the business VPC 1 and business VPC 2.</td>
</tr>
<tr>
<td>Bound network instance</td>
<td>Bind the network instances in the network zone of the business, i.e., the business VPC 1 and business VPC 2.</td>
<td>Bind the network instances in the network zone of the firewall, i.e., the firewall VPC.</td>
</tr>
</table>


### Step 2. Create a custom route table
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn).
2. In the CCN list, click the CCN ID to enter the details page and access the **Route Table** tab. 
3. Click **Create Route Table**.
![]()
4. In the pop-up window, enter the name and other information.
![]()
5. Click **OK**.
6. Repeat steps 3–5 to create the firewall route table.



### Step 3. Set the route reception policy
1. Click the business route table ID to enter the details page and access the **Route Reception Policy** tab.
2. Click **Add Network Instance**.
![]()
3. On the **Select a network instance** tab, select the firewall VPC.
![]()
4. Click **OK** to complete the route reception policy configuration of the business route table.
5. Select the firewall route table and repeat steps 1–4 to configure its route reception policy.
>? Please set according to the route table reception policy in the route plan.
>

### Step 4. Bind a network instance
1. Click the business route table ID to enter the details page and access the **Bind an Instance** tab.
2. Click **Bind Network Instance**.
![]()
3. On the **Select a network instance** tab, select the network instances in the business zone, i.e., the business VPC 1 and business VPC 2.
![]()
4. Click **OK** to complete binding the business route table to network instances.
5. Select the firewall route table and repeat steps 1–4 to bind it to network instances.
