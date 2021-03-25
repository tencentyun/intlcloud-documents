To create a complete Auto Scaling solution, perform the following three steps:
![](https://main.qcloudimg.com/raw/bb6c41ddc7c79cb3c76580f9ae42a008.png)

>? This document describes how to create an Auto Scaling solution in the console. If you prefer to use APIs, see [API Use Case](https://intl.cloud.tencent.com/document/product/377/30983).

## Step 1. Create a Launch Configuration
A launch configuration defines the configuration information of CVM instances used for auto scaling, including their images, storage, networks, security groups, login methods, and other configuration information.

>? Creating a launch configuration is **free of charge**.



### Selecting a region
1. Log in to the Auto Scaling console and click **[Launch Configuration](https://console.cloud.tencent.com/autoscaling/config)** in the left sidebar.
2. At the top of the **Launch Configuration** management page, select the project and region of the launch configuration, as shown in the following figure:
![](https://main.qcloudimg.com/raw/014744e64c1b5bb3f251a478baa84540.png)
CVM instances and CLB instances must be in the same region as the one specified for launch configuration. For example, if the Guangzhou region is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added to the scaling group. For a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances from other regions (such as Shanghai, Beijing, Hong Kong (China), or Toronto).
3. Click **Create** to go to the **Create Launch Configuration** page.



### Selecting a model
Set up the launch configuration name, availability zone, and model, as shown in the following figure:
![](https://main.qcloudimg.com/raw/0bd50d2d909e34deadd5d9681ba5f7e6.png)

- **Launch configuration name**: set the name of the launch configuration.
- **Billing mode**: only **pay-as-you-go** is supported. For more information, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/213/2180).
- **Availability zone and instance**: select the model of the instance to be bound with the scaling group.


### Selecting images, storage, and bandwidth
1. When creating a launch configuration, you can use a public image, custom image or shared image as shown below. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/213/4940).
![](https://main.qcloudimg.com/raw/51d1974f89849862c8a4536f02864c2a.png)
We recommend that you use a custom image where the application environment has already been deployed for the following reasons:
	- If you select a public image, the CVM instances created in a scaling group will have an operating system without the application environment. Then, you need to manually deploy the application environment.
	- If you select **Custom Image**, you can use the image created for a CVM instance with an environment that has been deployed to batch create CVM instances have the same software environment as the original CVM, so as to implement batch deployment.
>?For more information about creating images for CVM instance to be bound to a scaling group, see [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
>
2. Set the disks in the launch configuration, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8c7bddbb071b278adec024d3070e69e6.png)
If you specify a cloud disk as the system disk, you can create a data disk using data disk snapshots:
	- Users with a large amount of data often use data disks to store data. You can create a snapshot for data disk A, and use this snapshot to quickly clone multiple disks for rapid server deployment.
	- When a new CVM instance is automatically added for Auto Scaling, if you've specified a snapshot for the data disk in the launch configuration, CBS automatically mounts a data disk to the launched CVM instance to copy data.
	- If a data disk snapshot is specified in the launch configuration, ensure that the data disk can be automatically mounted correctly so that the scaling group can be scaled out automatically. The snapshot of the data disk of the original instance should be taken before auto scaling is configured so that data disks can be automatically mounted when new CVM instances are activated. For more information, see the “Automatic Mounting” section in [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).
3. An independent public IP address is allocated by default at no charge. Please select a network billing method based on your actual needs, as shown in the following figure:
![](https://main.qcloudimg.com/raw/e4cc00d81ec2ba1806f232949d009074.png)
>? Auto Scaling is free of charge, but the added CVM instances, disks, and networks are billed in pay-as-you-go mode. Prices will be shown based on your configurations.
>

### Setting information
1. On the **Complete Configuration** page, select the login method and security group. By default, CVM instances created by Auto Scaling are protected by Cloud Security and Cloud Monitor free of charge. See the figure below:
![](https://main.qcloudimg.com/raw/26b2f98e3a32eb5d9a50af56fbe6eb1e.png)
2. After configuration confirmation and successful creation, you can view created launch configurations on the **Launch Configuration** page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7b25c445cf77fecdcf9c67b1f5431a70.png)

## Step 2. Create a Scaling Group
A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose.


### Creating a scaling group
1. Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling/group?rid=1) and click **Scaling group** in the left sidebar.
2. On the **Scaling group** management page, click **Create**.
3. In the pop-up window, enter the basic information of the scaling group (fields marked with <label style="color:#e1504a;">*</label> are required), as shown in the following figure:
![](https://main.qcloudimg.com/raw/09b130b952b426530acbe5ad6288b5d7.png)
 - **Name**: set the name of the scaling group.
 - **Min Capacity**: if the current number of CVM instances is less than this value, Auto Scaling will automatically add instances to meet the minimum scaling capacity.
 - **Initial Capacity**: this defines the initial number of CVM instances when the scaling group is created.
 - **Max Capacity**: if the current number of CVM instances is greater than this value, Auto Scaling will automatically remove instances to meet the maximum capacity.
>? The current number of CVM instances in the scaling group will be maintained between the minimum and the maximum capacity.
>
 - **Launch Configuration**: you can select an existing launch configuration or create one.
 - **Supported networks and subnets**: select networks and subnets as needed.
 Click **Next**.
4. (Optional) On the **Load Balancer Configuration** page, select an existing CLB or create one and then click **Next: other configurations**.
5. On the **Other configurations** page, refer to the following information to set the removal policy and instance creation policy.
 - **Removal policy**: when the scaling group wants to reduce the number of instances and has multiple choices, it determines which instances to remove according to the removal policy. The options **Remove the oldest instances** and **Remove the latest instances** are supported.
 - **Instance creation policy**:
	 - **Preferred Availability Zones (Subnets) First**: the availability zones (subnets) will be selected sequentially from top to bottom of the configuration list. This mode is suitable for architectures with one primary availability zone and other secondary availability zones.
	- **Multiple Availability Zones (Subnets) Distribution**: during scale-out, the system will select availability zones (subnets) with relatively few instances in which to create new instances. This mode is suitable for architectures where instances need to be evenly distributed. 
2. Click **Completed** to complete creation. You can view the created scaling groups on the **Scaling group** page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/3943d03b316974835be615acef893bd2.png)

### Adding instances (optional)
1. Go to the **[Scaling group](https://console.cloud.tencent.com/autoscaling/group?rid=1)** page and select the ID of the scaling group to be configured to enter its details page.
2. Select the **Associate with Instances** tab and click **Add Instances**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/741d48877eaef9642dfff2193d540403.png)
3. In the **Add Instances** window that pops up, select the instance to be bound and click **OK**.
>? If you cannot add or remove a CVM instance to or from the list, check the maximum and minimum capacity values specified for the scaling group.

## Step 3. Create a Scaling Policy

You can use scaling policies to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm-triggered policy** to perform scaling based on Cloud Monitor metrics (such as CPU utilization and memory usage).

### Creating a scheduled action

If your load changes are predictable, you can set scheduled actions to plan your scaling activities. This feature can automatically increase or decrease CVM instances according to a schedule. This allows you to flexibly cope with traffic load changes and improve device utilization while reducing deployment and instance costs.
1. Go to the **[Scaling group](https://console.cloud.tencent.com/autoscaling/group?rid=1)** page and select the ID of the scaling group to be configured to enter its details page.
2. Select the **Scheduled Action** tab and click **Create**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
3. In the **Create Scheduled Action** window that pops up, specify the action name, scaling group activities, repeat cycle, and other information.
4. After completing the configuration, click **OK** to view the scheduled action, as shown in the following figure:
![](https://main.qcloudimg.com/raw/3bd91d894eeefb2b3fc5119500694574.png)

### Creating an alarm trigger policy

If you want to perform scaling based on CVM metrics, you can create an alarm policy to plan device scaling. This policy helps you automatically increase or decrease the number of instances in your scaling group to flexibly handle business load changes, increase device utilization, and reduce deployment and instance costs.
>?
> - When a scaling group is created, a ping unreachable alarm policy is created by default, which is used to replace unhealthy CVMs.
> - Before using an alarm trigger policy, you need to install the latest version of Cloud Monitor Agent in the CVM image. For more information, see [Installing CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211).
> 
1. Go to the **[Scaling group](https://console.cloud.tencent.com/autoscaling/group?rid=1)** page and select the ID of the scaling group to be configured to enter its details page.
2. Select the **Alarm Trigger Policy** tab and click **Create**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/fb81fc1a502b12f736d6f71b2cdae467.png)
3. In the **Create Alarm Policy** window that pops up, configure the Cloud Monitor metrics (such as CPU utilization, memory usage, and bandwidth), which will be used as the basis of adding or removing CVM instances by a specified number or percentage.
You can also choose **Use Existing Policy (Optional)** to copy an existing policy from an existing scaling group to the current scaling group, as shown in the following figure:
![](https://main.qcloudimg.com/raw/6cd93ad87076ffbc43d7f2af2477ab01.png)
4. After completing the configuration, click **OK** to view the alarm policy.


