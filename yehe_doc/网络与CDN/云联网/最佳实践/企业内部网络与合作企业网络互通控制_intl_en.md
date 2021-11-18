You have activated the CCN service, and all VPCs in your organization have been interconnected through CCN. By default, network instances added to CCN are interconnected.
In certain scenarios, you may want to restrict your partner's network instances from directly accessing your organization's internal network zone without affecting the interconnection between internal VPC network instances. This can be implemented through the custom route table feature of CCN. Specifically, you can plan different custom route tables for CCN and create an interconnection VPC, through which your partner's VPC can access your internal network zone.
>? The custom route table feature is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

## Overview
The network instances associated with CCN are divided into an internal zone, a peering zone, and an external partner zone. Network instances in the internal zone are interconnected, while the partner VPC access the internal zone through the interconnection VPC.
As shown below, create three custom route tables for the CCN instance: the internal route table, the interconnection route table, and the external route table.
Here:
- Internal VPCs are interconnected after they are bound to the internal route table.
- The interconnection VPC is bound to the interconnection route table, which contains the routing information of the internal VPCs and the partner VPC.
- The partner VPC is bound to the external route table, which contains only the routing information of the interconnection VPC.
![]()

## Prerequisites
1. You have activated the CCN service and created a CCN instance. For detailed directions, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
2. The CCN instance has been associated with 4 network instances (for verification and subject to your actual business needs). For detailed directions, please see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

## Directions

### Step 1. Plan a custom route table
According to the conditions of network zones, three custom route tables need to be planned: the internal route table, the interconnection route table, and the external route table.
The routing plan of the custom route table is as follows:

| Item           | Internal Route Table                                                | Connection Route Table                                                   | External Route Table                                               |
| -------------- | --------------------------------------------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| Route reception policy   | Receive the routes of the network instances in the internal network zone, i.e., routes of the internal VPCs. | Receive the routes of the network instances in the internal network zone and partner network zone, i.e., routes of the internal VPCs and partner VPC. | Receive the routes of the network instances in the interconnection network zone, i.e., routes of the interconnection VPC.    |
| Bound network instance | Bind network instances in the internal network zone, i.e., internal VPCs.            | Bind network instances in the interconnection network zone, i.e., the interconnection VPC. | Bind network instances in the partner network zone, i.e., the partner VPC. |

### Step 2. Create a custom route table
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn).
2. In the CCN list, click the CCN ID to enter the details page and access the **Route Table** tab. 
3. Click **Create Route Table**.
![]()
4. In the pop-up window, enter the name and other information.
![]()
5. Click **OK**.
6. Repeat steps 3–5 to create the interconnection route table and external route table.


### Step 3. Set the route reception policy
1. Click the internal route table ID to enter the details page and access the **Route Reception Policy** tab.
2. Click **Add Network Instance**.
![]()
3. On the **Select a network instance** tab, select the network instances in the internal network zone, i.e., the internal VPC 1 and internal VPC 2.
![]()
4. Click **OK** to complete the route reception policy configuration of the internal route table.
5. Repeat steps 1–4 to configure the route reception policies of the interconnection route table and external route table.
>? Please set according to the route table reception policy in the route plan.
>

### Step 4. Bind a network instance
1. Click the internal route table ID to enter the details page and access the **Bind an Instance** tab.
2. Click **Bind Network Instance**.
![]()
3. On the **Select a network instance** tab, select the network instances in the internal zone, i.e., the internal VPC 1 and internal VPC 2.
![]()
4. Click **OK** to complete binding the internal route table to the network instance.
5. Repeat steps 1–4 to bind the interconnection route table and external route table to network instances.
