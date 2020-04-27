To create a complete Auto Scaling solution, complete the following steps:
![](https://main.qcloudimg.com/raw/bb6c41ddc7c79cb3c76580f9ae42a008.png)

> The following describes how to create an Auto Scaling solution in the console. If you prefer to use APIs, see [API Use Cases](https://intl.cloud.tencent.com/document/product/377/4232).

## Creating a Launch Configuration
A launch configuration defines the configuration information of CVM instances used for auto scaling, including the images, storage, networks, security groups, login methods, and other configuration information of the CVMs.

> Creating a launch configuration is **free of charge**.

1. Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Launch Configuration** to go to the launch configuration management page.

### Selecting a region

1. Select the project and region for the launch configuration, which is explained as follows:
The selected region determines the scope of instances that can be manually added and CLBs that can be bound. For example, if the Guangzhou region is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added to the scaling group. For a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances in any region (for example, Shanghai, Beijing, Hong Kong (China), and Toronto) other than Guangzhou.
![](https://main.qcloudimg.com/raw/014744e64c1b5bb3f251a478baa84540.png)
2. Click **Create**, and complete the basic information of the launch configuration on the page that appears.

### Selecting a model

On the "Create Instance" page, enter the launch configuration name, select the availability zone, and select the model, as shown in the following figure:
![](https://main.qcloudimg.com/raw/0bd50d2d909e34deadd5d9681ba5f7e6.png)
- Enter a name for your launch configuration.
- Select the same model as the CVM instance that you want to bind to the scaling group.

### Selecting an image

When creating a launch configuration, you can use public images or custom images.
We recommend that you use a "custom image" where the application environment has already been deployed. The reasons are as follows:
- If you select a public image, the CVM instances created in a scaling group will have a "clean" operating system, which means you need to manually deploy the application environment.
- If you select a custom image, by creating an image for the CVM instance with an environment that has been deployed, and using the image to create CVM instances in batches, the CVM instances will have the same software environment as the original CVM instance after successful creation. In this way, you can perform batch deployment.

Bind the image of the desired CVM instances to a scaling group. For more information on how to create the image of a CVM instance to be bound to a scaling group, see [Creating a Custom Image](https://intl.cloud.tencent.com/document/product/213/4942).
![](https://main.qcloudimg.com/raw/51d1974f89849862c8a4536f02864c2a.png)

### Selecting a storage and bandwidth

On the "3. Select storage and bandwidth" page, choose the disk and network, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2ef5c1920b6e1fbb46a9a17c5de91529.png)
> If you specify a Cloud Block Storage (CBS) cloud disk as the system disk, you can create a data disk by using data disk snapshots.

Users with a large amount of data often use data disks to store data. When a snapshot file is created for data disk A, users can use this file to quickly clone multiple disks, achieving rapid CVM deployment.

When Auto Scaling automatically adds a new CVM instance, if a data disk snapshot is specified for the data disk in the launch configuration, Tencent Cloud cloud disks support the automatic mounting of the data disk containing the set data after the CVM instance is launched, meeting the needs of automatic data replication.

If a data disk snapshot is specified in the launch configuration, you must ensure that the data disk can be automatically and corrently mounted so that the scaling group can be scaled out automatically. Before configuring auto scaling, you must perform some operations on the original instance of the data disk snapshot in order to support the automatic mounting of the data disk when a new CVM instance is launched. For more information on the directions, see [Mounting a Data Disk Automatically When Launching New Instances by Using Custom Images and Data Disk Snapshots](https://intl.cloud.tencent.com/document/product/362/32401).

> Auto Scaling is free of charge, but the added CVM instances, disks, and networks are billed in pay-as-you-go mode. Prices will be shown based on your configurations.

### Setting information

1. On the "4. Security Group and CVM" page, select the login method and security group. By default, Auto Scaling-created CVM instances are protected by Cloud Security and Cloud Monitor for free, as shown in the following figure:
![](https://main.qcloudimg.com/raw/26b2f98e3a32eb5d9a50af56fbe6eb1e.png)
2. After the configuration is completed, you will see a new entry in the launch configuration list, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7b25c445cf77fecdcf9c67b1f5431a70.png)

## Creating a Scaling Group

A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose.
1. Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Scaling Group** to go to the scaling group management page.

### Creating a scaling group

1. Click **Create**, and complete the basic information of the scaling group on the page that appears. Here, ![](https://main.qcloudimg.com/raw/17d2d70b9ba8dcea80f315841bcd71ac.png) is a required item, as shown in the following figure:
![](https://main.qcloudimg.com/raw/09b130b952b426530acbe5ad6288b5d7.png)
 - A scaling group maintains the number of CVM instances to meet the desired capacity between the minimum and maximum capacities.
	- The initial instance quantity defines the default number of CVM instances in the scaling group.
	- If a scaling group has a number of CVM instances less than the minimum scaling capacity, it will automatically increase the number of instances to meet the minimum condition.
	- If a scaling group has a number of CVM instances greater than the maximum scaling capacity, it will automatically terminate instances until the number of instances is equal to the allowed maximum value.
 - Select an existing launch configuration or create one.
 - Select the network, availability zone, and removal policy.
 - (Optional) Associate with an existing CLB policy or create one.
After the configuration is completed, you will see a new entry in the scaling group list, as shown in the following figure:
![](https://main.qcloudimg.com/raw/3943d03b316974835be615acef893bd2.png)

### (Optional) Adding instances

In the instance list, add the instance that you want to bind. After the configuration is completed, you will see a new entry in the launch configuration list, as shown in the following figure:
![](https://main.qcloudimg.com/raw/741d48877eaef9642dfff2193d540403.png)
> If you cannot add a CVM instance to or remove a CVM instance from the list, check the specified maximum and minimum capacities.

## Creating a Scaling Policy

You can use scaling policies to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm trigger policy** to perform scaling adjusted by Cloud Monitor metrics (such as CPU utilization and memory usage).

### Creating a scheduled action

Scaling through scheduled actions works better in business scenarios where the volume is stable and predictable. You can use scheduled actions to automatically add or remove CVM instances at a specified point of time or periodically to meet changing needs, increase device utilization, and reduce deployment and instance costs.

1. On the **Scaling group** page, click "Scaling group" to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
2. Click the **Scheduled Action** tab and then click **Create**.
![Scheduled action](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
3. Specify information such as the scheduled action name, execution time, and activities to be executed on the "New" page. You can also select **Repeat** to define the interval of performing the scheduled action.
![Create a scheduled action](https://main.qcloudimg.com/raw/196e482efed765613323dea3703532e7.png)
4. After the configuration is completed, you will see the created scheduled action in the list. An example is shown in the following figure:
![Scheduled action list](https://main.qcloudimg.com/raw/3bd91d894eeefb2b3fc5119500694574.png)

### Creating an alarm trigger policy

To adjust business deployment based on CVM metrics, you can customize an alarm trigger policy, which will automatically increase or decrease the number of CVM instances when the business load pushes the metrics to the thresholds. This flexibly handles traffic load changes, improves device utilization, and reduces deployment and instance costs.

>
> - When a scaling group is created, an alarm trigger policy for unreachable pings is created by default to replace unhealthy CVMs.
> - Before using an alarm trigger policy, you need to install the latest version of Cloud Monitor agent in the CVM's image. For more information, see [Installing Monitoring Components](/doc/product/248/安装监控组件).

1. On the **Scaling group** page, click a scaling group ID to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
2. Click the **Alarm Trigger Policy** tab and then click **Create**.
![](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
3. Set the alarm policy on the creation page to automatically increase or decrease the CVM instances by a specified number or percentage for the scaling group based on cloud monitoring performance metrics (such as the CPU utilization, memory usage, or bandwidth).
You can also copy the policy (optional) directly from the existing policies of an existing scaling group to the current scaling group.
![Create an alarm trigger policy](https://main.qcloudimg.com/raw/196e482efed765613323dea3703532e7.png)
4. After the configuration is completed, you will see the created alarm trigger policy in the list on the page.


