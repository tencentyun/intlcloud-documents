You can assign different addressing routes for subnets in the same VPC by configuring and managing route table selection policy and using the custom route tables. Thus, you can manage the paths requested by the networks in CCN in a more fine-grained manner.
>? The custom route table and route table selection policy features are currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

## Overview
You can assign different addressing route tables for subnets in different business VPCs by configuring route table selection policy. In the figure below, we create three **custom route tables** for the CCN instance, i.e. business route table 1, business route table 2 and office route table. We configure the next hop route table of subnet 2 in the business VPC as business route table 2 by adding the route table selection policy.
The information is as follows:
- The business route table 1 only receives and learns routes from the office VPC 1 and is bound to the business VPC.
- The business route table 2 only receives and learns routes from the office VPC 2 and is not bound to any network instance.
- The office route table receives and learns routes from the business VPC and is bound to the office VPC 1 and office VPC 2.
![]()

## Prerequisite
1. You have activated CCN service and created a CCN instance. For more information, see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
2. You have associated three network instances in the CCN instance (it is for verification, you can configure this based on your actual needs). For more information on how to associate network instances, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

## Directions

### Step 1: planning for the custom route table and route table selection policy
**Plan of the custom route table**
The routing plan of the custom route table is as follows:
<table>
<tr>
<th>Item</th>
<th>Business route table 1</th>
<th>Business route table 2</th>
<th>Office route table</th>
</tr>
<tr>
<td>Route reception policy</td>
<td>Office VPC 1</td>
<td>Office VPC 2</td>
<td>Business VPC</td>
</tr>
<tr>
<td>Bound network instance</td>
<td>Business VPC</td>
<td>Not bound to any network instance</td>
<td>Office VPC 1 and office VPC 2</td>
</tr>
</table>

**Plan of route table selection policy**
<table>
<tr>
<th>Source network instance</th>
<th>Source IP range</th>
<th>Next hop route table</th>
</tr>
<tr>
<td>Business VPC</td>
<td>10.0.100.0/24</td>
<td>Business route table 2</td>
</tr>
</table>

### Step 2: creating a custom route table
1. Log in to the [CCN Console](https://console.cloud.tencent.com/vpc/ccn).
2. In the CCN list, click the **ID/Name** of the desired CCN instance to open the **Route Table** tab. 
3. Click **Create Route Table**.
![]()
4. Enter the name and other relevant information in the pop-up window.
![]()
5. Click **OK** to complete the creation for business route table 1.
6. Repeat steps 3-5 to create business route table 2 and office route table.


### Step 3: setting the route reception policy
1. Click the ID of business route table 1 to enter the details page and access the **Route Reception Policy** tab.
2. Click **Add Network Instance**.
![]()
3. Select "Office VPC 1" in **Select a Network Instance** tab.
![]()
4. Click **OK** to complete the route reception policy configuration for the business route table 1.
5. Repeat steps 1-4 to configure route reception policy for business route table 2 and office route table.
>? Please set according to the route table reception policy in the route plan.
>

### Step 4: binding a network instance
1. Click the ID of business route table 1 to enter the details page and access the **Bind an Instance** tab.
2. Click **Bind Network Instance**.
![]()
3. Select "Business VPC" in the **Select a Network Instance** tab.
![]()
4. Click **OK** to complete binding the business route table 1 to the network instance.
5. Select the office route table and repeat steps 1-4 to bind it to the network instance.
>?Business route table 2 is not bound to any network instance.
>

### Step 5: configuring route table selection policy
1. Click **Add Policy** in the **Route Table Selection Policy** tab.
   ![]()
2. Enter relevant parameters in **Add route table selection policy** pop-up window. Source network instance: business VPC; source IP range: 10.0.100.0/24; next hop route table: business route table 2.
   ![]()
3. Click **OK** to complete adding the route table selection policy.
