You have activated the CCN service, and all VPCs in your organization have been interconnected through CCN. By default, network instances added to CCN are interconnected.

In certain scenarios, you can divide different network zones in your organization network, and network instances in different zones are isolated from each other. This can be implemented through the custom route table feature of CCN. Specifically, you can plan different custom route tables for CCN and associate different network instances with them in order to isolate network instances.
>? The custom route table feature is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>


## Overview
The network instances associated with CCN are divided into a test zone and a production zone. Network instances are interconnected within the same zone but isolated across zones.
As shown below, create two custom route tables for the CCN instance: the test route table and the production route table.
Here:

- The test route table only receives and learns routes from and is bound to the test VPC.
- The production route table only receives and learns routes from and is bound to the production VPC.
![]()


## Prerequisites
1. You have activated the CCN service and created a CCN instance. For detailed directions, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
2. The CCN instance has been associated with 4 network instances (for verification and subject to your actual business needs). For detailed directions, please see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).


## Directions

### Step 1. Plan a custom route table
According to the isolation of network zones, two custom route tables need to be planned: the test route table and the production route table.
The routing plan of the custom route table is as follows:
<table>
<tr>
<th>Item</th>
<th>Test Route Table</th>
<th>Production Route Table</th>
</tr>
<tr>
<td>Route reception policy</td>
<td>Receive the routes of the network instances in the network zone of the test environment, i.e., routes of the test frontend VPC and the test backend VPC.</td>
<td>Receive the routes of the network instances in the network zone of the production environment, i.e., routes of the production frontend VPC and the production backend VPC.</td>
</tr>
<tr>
<td>Bound network instance</td>
<td>Bind the network instances in the network zone of the test environment, i.e., the test frontend VPC and test backend VPC.</td>
<td>Bind the network instances in the network zone of the production environment, i.e., the production frontend VPC and production backend VPC.</td>
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
6. Repeat steps 3–5 to create the production route table.


### Step 3. Set the route reception policy
1. Click the test route table ID to enter the details page and access the **Route Reception Policy** tab.
2. Click **Add Network Instance**.
![]()
3. On the **Select a network instance** tab, select the network instances in the test zone, i.e., the test frontend VPC and test backend VPC.
 ![]()
4. Click **OK** to complete the route reception policy configuration of the test route table.
5. Select the production route table and repeat steps 1–4 to configure its route reception policy.

### Step 4. Bind a network instance
1. Click the test route table ID to enter the details page and access the **Bind an Instance** tab.
2. Click **Bind Network Instance**.
![]()
3. On the **Select a network instance** tab, select the network instances in the test zone, i.e., the test frontend VPC and test backend VPC.
 ![]()
4. Click **OK** to complete binding the test route table to network instances.
5. Select the production route table and repeat steps 1–4 to bind it to network instances.
