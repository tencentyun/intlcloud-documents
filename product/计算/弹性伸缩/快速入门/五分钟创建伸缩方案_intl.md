To create a complete Auto Scaling plan, go through the following steps:
![](https://main.qcloudimg.com/raw/05ef734d160c1c73061cf103cfb44d91.png)

>? Here we demonstrate creating AS plan in the console. If you prefer using APIs, see [API Usage Sample](https://cloud.tencent.com/document/product/377/4232).

## Creating a Launch Configuration
A launch configuration defines the information that is required for a scaling group to launch CVM (Cloud Virtual Machine) instances. The information includes CVM's image, storage, network, security group, and login method.

>? Creating a launch configuration is **free of charge**.

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Launch Configuration** to go to the launch configuration management page.

### Selecting a Region

1. Select the project and region for the launch configuration, as shown below:
CVM instances and CLB instances must be the same region as the one specified for launch configuration. For example, when Guangzhou is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added in the scaling group.  In a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances in any region (e.g., Shanghai, Beijing, Hong Kong, Toronto) other than Guangzhou.

![Select a region](https://main.qcloudimg.com/raw/07a746c4f69b1a8641b74ce1ddc5cf4f.png)

2. Click ![](//mccdn.qcloud.com/static/img/9d38f7bfbe02a922370765f3adfa58bf/image.png), and enter the basic information of the launch configuration on the pop-up page.

### Selecting a Model

On the "Create a launch configuration" page, enter the launch configuration name, select the availability zone, and select the model. See the figure below:

![](https://main.qcloudimg.com/raw/a38b03bb3c23c1393169598fcb195897.png)

- Enter a name for your launch configuration.
- Select the same model as the CVM instance that you want to bind to the scaling group.

### Selecting an Image

When creating a launch configuration, you can use either public or custom image.
We recommend using a "custom image" where the application environment has already been set up. Because:
- If you select a public image, the CVM instances created in a scaling group will have a "clean" operating system - you need to manually set up the application environment.
- However, the custom image helps batch production.  you can create an image of a CVM instance with application environment deployed, and then use the image to batch create many CVM instances which will have the same application environment as the original instance.

Bind the image of the desired CVM instances to a scaling group. For more information about how to create a CVM instance bonded to a scaling group, see [Creating a Custom Image](https://cloud.tencent.com/document/product/213/4942).

![](https://main.qcloudimg.com/raw/9459776ded2df48d711cf4b6a2bb77a4.png)

### Selecting Storage and Bandwidth

On the "3. Select storage and bandwidth" page, choose the disk and network. See the figure below:
![](https://main.qcloudimg.com/raw/c958b41819de424b6e4b7e414c92d71e.png)
>! If you specify a CBS (Cloud Block Storage) disk as the system disk, then you can create a data disk using data disk snapshots.

Disk data snapshot makes it easier to store Big data: snapshot a data disk, then use this snapshot to create more disks as needed. 

When a new CVM instance added to Auto Scaling, if you've specified a snapshot for the data disk in lunch configuration, CBS automatically mounts a data disk in the launched CVM instance to copy data. In this case, the data disk must be correctly mounted in the CVM instance to automatically scale out the scaling group. To auto-mount data dick in a new CVM instance, some additional operations on snapshot's original instance are required before setting up the automatic scaling. To learn about the operations, see [here](https://cloud.tencent.com/doc/product/362/5564).

>? Auto Scaling is free of charge, but the added CVM instances, disks, and networks are pay-as-you-go. You will see the prices based on your configurations. 

### Setting Information

1. On the "4. Security Group and CVM" tab, select the login method and security group. By default, Cloud Security and Cloud Monitor  guard Auto Scaling-created CVM instances with free of charge, as shown below:  
![](https://main.qcloudimg.com/raw/e7e5cba6e2c52b768e959a5db4c73bae.png)
2. After the configuration is completed, you will see this entry on the launch configuration list, as shown below:  
![](https://mc.qcloudimg.com/static/img/67ba31fd6c1f12485bb8f96220aaf6af/image.png)

## Creating a Scaling Group

A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose.

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Scaling Group** to go to the scaling group management page.

### Creating a Scaling Group

1. Click ![](//mccdn.qcloud.com/static/img/9d38f7bfbe02a922370765f3adfa58bf/image.png) and enter the necessary information of the scaling group on the pop-up page. Fields marked with ![](//mccdn.qcloud.com/static/img/f9df27a1d1e0d42a7ff08dd884bfa34c/image.png) are required. See the figure below:
![](https://mc.qcloudimg.com/static/img/2fb365611291fb8917637dba46f398f4/image.png)
 - A scaling group maintains the number of CVM instances too meet the desired capacity between the minimum and maximum capacity values.
    - The starting instance quantity defines the default number of CVM instances in the scaling group.
    - If a scaling group has a number of CVM instances less than the minimum scaling capacity value, it will automatically increase the number of instances to meet the minimum condition. 
    - If a scaling group has a number of CVM instances greater than the maximum scaling capacity value, it will automatically terminate instances until the number of instances is equal to the maximum value allowed.
 - Select an existing launch configuration or create a new one.
 - Select the network, availability zone, and removal policy.
 - (Optional) Associate with an existing CLB instance or create a new one.

2. After the configuration is completed, you will see this entry on the scaling group list, as shown below: 
![](https://mc.qcloudimg.com/static/img/c1c64cdb16c11aaa6d31bc4781db62c4/image.png)

### Adding a CVM Instance (Optional)

Add the desired CVM instance to the CVM instance list. After the configuration is completed, you will see this entry on the launch configuration list, as shown below: 
![](https://mc.qcloudimg.com/static/img/e3232872ad5fe19e89c9eb7306418a3d/image.png)
>? If you are unable to add/remove a CVM instance to/from the list, please check the maximum and minimum capacity values you specified.

## Creating a Scaling Policy

You can use scaling policies  to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled task** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm-triggered policy** to perform scaling adjusted by Cloud Monitor metrics (e.g., CPU utilization and memory usage).

### Creating a Scheduled Scaling Task

Scheduled Scaling works better in such scenarios as the business volume is stable and predictable. You can use it to automatically add/remove CVM instances at a specified point of time or periodically to meet changing needs, increase machine utilization, and reduce expenses on deployment and instances. 

1. On the **Scaling group** page, click "Scaling group" to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
2. Select the "Scheduled Scaling" tab and click **Create**.
![Scheduled task](https://main.qcloudimg.com/raw/9ed7c9dbfc82035a82136f5f215cc12a.png)
3. Specify information such as the task name, run time, and action. You can also select **Repeat** to run the scheduled scaling task regularly
![Create a scheduled scaling task](https://main.qcloudimg.com/raw/5ebba7a45ab3db576eb3d8fd92246cfe.png)
4.  After the configuration is completed, you will see this task, as shown below:
![Scheduled Scaling Task List](https://main.qcloudimg.com/raw/f21339e4d6650929e4b69ff61ce371e5.png)

### Creating an Alarm-triggered Policy

If you want to adjust the scaling based on CVM metrics, you can create an alarm-triggered policy. This policy helps you automatically adjust (increase or decrease) the number of instances in your scaling group to handle dynamic volumes, increase machine utilization, and reduce expenses on deployment and instances.

>?
> - By default,  a ping is created in a scaling group to trigger the alarm that tells you to replace unhealthy servers.
> - Before using an alarm-triggered policy, you need to install the latest version of Cloud Monitor agent in CVM's image. For more information, please see [Installing Monitoring Components](/doc/product/248/安装监控组件).

1. On the **Scaling group** page, click a Scaling group ID to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
2. Select the "Alarm-triggered policy" tab and click **Create**.
![](https://main.qcloudimg.com/raw/2fac8567b4042a2c65c1906ae8f8396d.png)
3. Configure the alarm-triggered policy. When the alarm-triggered policy is in effect, the scaling group adjusts the number of instances or the percentage of the instance by Cloud Monitor metrics (e.g., CPU utilization, memory usage, and bandwidth).

You can also copy the policy to another scaling group.
![Create an alarm-triggered policy](https://main.qcloudimg.com/raw/41c7c0f95256e5b8492dc58826d13cd4.png)  

4. After the configuration is completed, you will see your alarm-triggered policy on the list, as shown below:
![Alarm-triggered policy list](https://main.qcloudimg.com/raw/3b2af877848e11c337901172055ba466.png)
