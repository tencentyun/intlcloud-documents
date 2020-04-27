This document describes how to set a static IP address for external access if the cluster needs to actively access external devices.

## Requirements

Check whether the following requirements are met in the cluster of your scaling group:
- Requests are received from a CLB.
- Cluster CVMs need to actively access external devices.
- A **static** public IP address is required for external access.

If yes, you can set the IP address by referring to the following solution.

## Solution Overview
1. Receive and respond to external requests by using the CLB.
2. Place the CVM in the subnet of VPC, map the route table to the NAT gateway, and deliver all active external access requests through the public IP address of the NAT gateway.
3. Set the network attribute of the scaling group to this subnet, so that all the scaled-out CVMs can actively access external devices through the NAT gateway.

See the following figure:

![](https://main.qcloudimg.com/raw/645411d191ecdf976ed11d5a11cd69aa.png)



## Configuration Method

### Step 1: Create a VPC instance and a subnet

#### **1. Create a VPC instance**

1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/), click **Virtual Private Cloud** in the navigation bar or click **Experience** on Tencent Cloud's [VPC overview page](https://intl.cloud.tencent.com/product/vpc) to enter the [VPC console](https://console.cloud.tencent.com/vpc/).

2. Select a region in the drop-down list above the list and click **New** to create a VPC instance. For example, select the "North China (Beijing)" region.

3. Enter the names of the VPC, subnet, and CIDR block, and select an availability zone for the subnet.

4. Click **Create**.


#### **2. Create a subnet**

1. Log in to the [Tencent Cloud console] (https://console.cloud.tencent.com/), click "Virtual Private Cloud" in the navigation bar, and then click "Subnet" in the leftside bar. Select a region and VPC in the drop-down list.
![](https://main.qcloudimg.com/raw/8c04a129eabe941ad8ef9758347e028f.png)

2. Click **New**, complete the subnet name, CIDR block, availability zone, and associated route table. Then, click **Create**.

3. After finishing the creation, you can purchase CVMs for this subnet.


### Step 2: Create an NAT gateway
#### **1. Purchase a NAT gateway**
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/), click the "Virtual Private Cloud" tab, and select "NAT Gateway".

2. Click **Create** in the upper-left corner, and complete or confirm the following parameters in the pop-up box:
	- Gateway name
	- Gateway type (which can be modified after creation)
	- VPC instance for the NAT Gateway service (which is the one just created by you)
	- Assign an EIP for the NAT gateway. This IP address is the static IP address through which your CVMs can access external devices.

3. Click **OK** to finish creating the NAT gateway.

4. After finishing the creation, configure routing rules on the route table page in the VPC console to direct subnet traffic to the NAT gateway.

#### **2. (Important) Configure the route table**
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/), click "Virtual Private Cloud" in the navigation bar to enter the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=8). Then, select "Route Table".

2. In the route table list, click the route table ID associated with the subnet that needs to access the Internet to go to the details page of the route table. Then, click **Edit** in "Routing Policies".

3. Click "New Line", specify the destination (for example, enter "0.0.0.0/0" in this example), select "NAT Gateway" as the next-hop type, select the ID of the created NAT gateway, and then click **OK**.
![](https://main.qcloudimg.com/raw/e5029e42a6570c26814375f2264a7f4b.png)

Now, even without a public IP address, your CVMs in this subnet can actively access external devices through the static IP address of the NAT gateway, during which this IP address is externally static.

Even if you purchase a CVM without any public IP addresses and with zero bandwidth, you can still actively access external devices, as shown in the following figure:
![](https://mc.qcloudimg.com/static/img/17ed153e06272885b56764781d9ab581/49.jpg)
However, the scaling group needs to recognize this subnet and ensure that all the CVMs are created in this subnet.

### Step 3: Configure the scaling group
This step is to map the subnet information to the scaling group so that the newly expanded CVM can be installed in this subnet by the scaling group.
**In this way, the expanded CVM will use the static outbound IP address of the NAT gateway to access external devices.**

In the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling/config), click **Create**:

- Complete the name of the scaling group, launch configuration (which needs to be correctly set up in advance), maximum number of groups, minimum number of groups, initial number of instances, and other required information.
- Set "Network" and "Subnet" to the set VPC and subnet respectively **(important)**.

See the following figure:
![](https://main.qcloudimg.com/raw/f752a1ae61b9a49c97d50626f33f76da.png)

You have finished the configuration.
