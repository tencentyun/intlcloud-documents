This document shows how to set a static IP address for outbound access of a cluster.


## Scenarios

This solution is applicable when clusters in your scaling group have all the three requirements below: 
- To receive requests from CLB
- To initiate outbound access 
- To use a **static** public IP address for outbound access

 

## Solution Overview
![](https://main.qcloudimg.com/raw/645411d191ecdf976ed11d5a11cd69aa.png)
1. Receive and respond to external requests by using the CLB.
2. Add the CVM to the subnet of the VPC and direct the route table to the NAT gateway so that all outbound access requests are delivered via the public IP address of the NAT gateway.
3. The network attribute of the scaling group is set as this subnet, so that all CVMs created for scale-out will use the NAT gateway for outbound access.



## Setting Up

### Step 1: create a VPC and subnet

#### 1. Create a VPC<span id="createVPC"></span>
1. Log in to the VPC console and select **[VPC](https://console.cloud.tencent.com/vpc/)** in the left sidebar.
2. At the top of the “VPC” page, select a region, such as “North China (Beijing)”.
3. Click **+Create**. In the “Create VPC” window that pops up, enter the names and CIDR blocks of the VPC and subnet, and choose the availability zone of the subnet.
4. Click **OK** to create the VPC.


#### 2. Create a subnet
1. In the VPC console, select **[Subnet](https://console.cloud.tencent.com/vpc/subnet)** in the left sidebar.
2. At the top of the “Subnet” page, select the region and VPC, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8c04a129eabe941ad8ef9758347e028f.png)
2. Click **+Create** and, in the **Create a Subnet** window that pops up, enter the subnet name, CIDR block, availability zone, and associated route table.
3. Click **Create**. After completing creation, you can purchase CVMs and add them to this subnet.


### Step 2: create a NAT gateway
#### 1. Create a NAT gateway<span id="createNAT"></span>
1. In the VPC console, select **[NAT Gateway](https://console.cloud.tencent.com/vpc/nat)** in the left sidebar.
2. On the **NAT Gateway** page, click **+Create**.
3. In the **Create a NAT Gateway** window that pops up, input or confirm the following parameters in sequence:
	- Gateway name
	- Gateway type (which can be modified after creation)
	- VPC of the NAT gateway (the VPC created in [Step 1](#createVPC)).
	- Assign an EIP for the NAT gateway. (This IP address is the static IP address for your CVM’s outbound access.)
3. After completing the configuration, click **Create** to complete the creation of the NAT gateway.
After the NAT gateway is created, you need to configure the routing rules on the route table page in the VPC console to redirect the subnet traffic to the NAT gateway.

#### **2. Set the route table (key)**
1. In the VPC Console, select **[Route Table](https://console.cloud.tencent.com/vpc/route)** in the left sidebar.
2. On the **Route Table** page, select the route table ID associated with the subnet that needs to access the Internet. The details page of the route table will be displayed.
3. Click **+ New routing policies**. In the **Add a route** window that pops up, complete the configuration, as shown in the following figure:
![](https://main.qcloudimg.com/raw/e5029e42a6570c26814375f2264a7f4b.png)
 - **Destination**: in this case, you can enter `0.0.0.0/0`.
 - **Next hop type**: select **NAT Gateway** and select the NAT gateway ID created in [Step 1](#createNAT).
4. Click **Create**. Now, even without a public IP address, your CVM in this subnet access internet through the static IP of the NAT gateway. 
Even if you purchase a CVM without any public IP addresses and with a bandwidth of zero, you still can enjoy active external access, as shown in the following figure:
![](https://mc.qcloudimg.com/static/img/17ed153e06272885b56764781d9ab581/49.jpg)
>? The scaling group needs to identify this subnet and ensure that all the CVMs are created on this subnet.
>

### Step 3: set up the scaling group
This step aims to direct the subnet information to the scaling group so that the newly created CVMs of the scaling group can be deployed in this subnet. **In this way, the newly created CVMs will use the the NAT gateway IP as the static IP to access internet.**
1. Log in to the Auto Scaling console and select **[Scaling Groups](https://console.cloud.tencent.com/autoscaling/group)** in the left sidebar.
2. On the **Scaling Groups** page, click **Create**.
3. On the **Create a Scaling Group** page that pops up, enter the scaling group name, the created launch configuration, maximum scaling capacity, minimum scaling capacity, initial number of instances, and other information.
In **Supported Network** and **Supported Subnet**, select the VPC and subnet you just set up, as shown in the following figure:
![](https://main.qcloudimg.com/raw/f752a1ae61b9a49c97d50626f33f76da.png)
This completes the configuration.
