To create a complete AS plan, go through the three steps below:
![](https://main.qcloudimg.com/raw/bb6c41ddc7c79cb3c76580f9ae42a008.png)

>Here we demonstrate creating AS plan in the console. If you prefer using APIs, see [API Usage Sample](https://intl.cloud.tencent.com/document/product/377/4232).

## Creating a Launch Configuration
A launch configuration defines the information that is required for a scaling group to launch CVM (Cloud Virtual Machine) instances. The information includes CVM's image, storage, network, security group, and login method.

>Creating a launch configuration is **free of charge**.

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Launch Configuration** to go to the launch configuration management page.

### Selecting a Region

1. Select the project and region for the launch configuration, as shown below:
CVM instances and CLB instances must be the same region as the one specified for launch configuration. For example, when Guangzhou is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added in the scaling group.  In a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances in any region (e.g., Shanghai, Beijing, Hong Kong, Toronto) other than Guangzhou.

![Select a region](https://main.qcloudimg.com/raw/014744e64c1b5bb3f251a478baa84540.png)

2. Click **Create**, and enter the basic information of the launch configuration on the pop-up page.

### Selecting a Model

On the "Create a launch configuration" page, enter the launch configuration name, select the availability zone, and select the model. See the figure below:

![](https://main.qcloudimg.com/raw/0bd50d2d909e34deadd5d9681ba5f7e6.png)

- Enter a name for your launch configuration.
- Select the same model as the CVM instance that you want to bind to the scaling group.

### Selecting an Image

When creating a launch configuration, you can use either public or custom image.
We recommend using a "custom image" where the application environment has already been set up. Because:
- If you select a public image, the CVM instances created in a scaling group will have a "clean" operating system - you need to manually set up the application environment.
- Custom image enables batch production. You can create an image of a CVM instance with application environment deployed, and then use the image to batch create many CVM instances which will have the same application environment as the original instance.

Bind the image of the desired CVM instances to a scaling group. For more information about how to create a CVM instance bound to a scaling group, see [Creating a Custom Image](https://intl.cloud.tencent.com/document/product/213/4942).

![](https://main.qcloudimg.com/raw/51d1974f89849862c8a4536f02864c2a.png)

### Selecting Storage and Bandwidth

On the "3. Select storage and bandwidth" page, choose the disk and network. See the figure below:
![](https://main.qcloudimg.com/raw/2ef5c1920b6e1fbb46a9a17c5de91529.png)

>If you specify a CBS (Cloud Block Storage) disk as the system disk, then you can create a data disk using data disk snapshots.

Disk data snapshot makes it easier to store Big data: snapshot a data disk, then use this snapshot to create more disks as needed. 

When a new CVM instance is added to Auto Scaling, if you've specified a snapshot for the data disk in launch configuration, CBS automatically mounts a data disk in the launched CVM instance to copy data. In this case, the data disk must be correctly mounted in the CVM instance to automatically scale out the scaling group. To auto-mount data disk in a new CVM instance, some additional operations on snapshot's original instance are required before setting up the automatic scaling.

>Auto Scaling is free of charge, but the added CVM instances, disks, and networks are pay-as-you-go. Prices will be shown based on your configurations.

### Setting Information

1. On the "4. Security Group and CVM" tab, select the login method and security group. By default, Auto Scaling-created CVM instances are protected by Cloud Security and Cloud Monitor for free, as shown below:  
![](https://main.qcloudimg.com/raw/26b2f98e3a32eb5d9a50af56fbe6eb1e.png)
2. After the configuration is completed, you will see an entry on the launch configuration list, as shown below:  
![](https://main.qcloudimg.com/raw/7b25c445cf77fecdcf9c67b1f5431a70.png)

## Creating a Scaling Group

A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose.

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Scaling Group** to go to the scaling group management page.

### Creating a Scaling Group

1. Click ![](https://main.qcloudimg.com/raw/f5e390d089b31895de1c7ee94f7f1902.png) and enter the necessary information of the scaling group on the pop-up page. Fields marked with ![](//mccdn.qcloud.com/static/img/f9df27a1d1e0d42a7ff08dd884bfa34c/image.png) are required. See the figure below:
![](https://main.qcloudimg.com/raw/09b130b952b426530acbe5ad6288b5d7.png)
 - A scaling group maintains the number of CVM instances to meet the desired capacity between the minimum and maximum capacity values.
    - The starting instance quantity defines the default number of CVM instances in the scaling group.
    - If a scaling group has a number of CVM instances less than the minimum scaling capacity value, it will automatically increase the number of instances to meet the minimum condition. 
    - If a scaling group has a number of CVM instances greater than the maximum scaling capacity value, it will automatically terminate instances until the number of instances is equal to the maximum value allowed.
 - Select an existing launch configuration or create a new one.
 - Select the network, availability zone, and removal policy.
 - (Optional) Associate with an existing CLB instance or create a new one.

2. After the configuration is completed, you will see this entry on the scaling group list, as shown below: 
![](https://main.qcloudimg.com/raw/3943d03b316974835be615acef893bd2.png)

### Adding a CVM Instance (Optional)

Add the desired CVM instance to the CVM instance list. After the configuration is completed, you will see this entry on the launch configuration list, as shown below: 
![](https://main.qcloudimg.com/raw/741d48877eaef9642dfff2193d540403.png)

> If you are unable to add/remove a CVM instance to/from the list, please check the maximum and minimum capacity values you specified.

## Creating a Scaling Policy

You can use scaling policies  to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm trigger policy** to perform scaling adjusted by Cloud Monitor metrics (e.g., CPU utilization and memory usage).

### Creating a Scheduled Scaling Action

Scheduled Scaling works better in business scenarios where volume is stable and predictable. You can use it to automatically add/remove CVM instances at a specified point of time or periodically to meet changing needs, increase machine utilization, and reduce expenses on deployment and instances. 

1. On the **Scaling group** page, click "Scaling group" to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
2. Select the "Scheduled Action" tab and click **Create**.
![Scheduled task](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
3. Specify information such as the action name, execution startup time, and scaling activities to be run. You can also select **Duplicate** to run the scheduled action on a periodic basis.
![Create a scheduled scaling action](https://main.qcloudimg.com/raw/196e482efed765613323dea3703532e7.png)
4. After the configuration is completed, you will see the created scheduled action on the list, as shown below:
![Scheduled Scaling Task List](https://main.qcloudimg.com/raw/3bd91d894eeefb2b3fc5119500694574.png)

### Creating an Alarm Trigger Policy

If you want to adjust the scaling based on CVM metrics, you can create an alarm-triggered policy. This policy helps you automatically adjust (increase or decrease) the number of instances in your scaling group to handle dynamic volumes, increase machine utilization, and reduce expenses on deployment and instances.

>- By default,  a ping is created in a scaling group to trigger the alarm that tells you to replace unhealthy servers.
> - Before using an alarm-triggered policy, you need to install the latest version of Cloud Monitor agent in CVM's image. For more information, please see [Installing Monitoring Components](https://intl.cloud.tencent.com/document/product/248/6211).

1. On the **Scaling group** page, click a Scaling group ID to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
2. Select the "Alarm Trigger Policy" tab and click **Create**.
![](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
3. Configure the Alarm Trigger Policy. When the Alarm Trigger policy is in effect, the scaling group adjusts the number of instances or the percentage of the instance by Cloud Monitor metrics (e.g., CPU utilization, memory usage, and bandwidth).

You can also copy the policy to another scaling group.
![Create an alarm-triggered policy](https://main.qcloudimg.com/raw/196e482efed765613323dea3703532e7.png)  

4. After the configuration is completed, you will see the created alarm trigger policy on the list on the page, as shown below:
![Alarm-triggered policy list](https://main.qcloudimg.com/raw/3bd91d894eeefb2b3fc5119500694574.png)
