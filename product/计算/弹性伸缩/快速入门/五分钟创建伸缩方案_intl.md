To create a complete AS plan, go through the three steps below:
![](https://main.qcloudimg.com/raw/05ef734d160c1c73061cf103cfb44d91.png)

>? Here we demonstrate creating AS plan in the console. If you prefer using APIs, see [API Usage Sample](https://cloud.tencent.com/document/product/377/4232).

## Creating a Launch Configuration
A launch configuration defines configuration information of the CVM instances for automatic scaling, including information of the CVM image, storage, network, security group, and login method.

>? Launch configurations can be created **free of charge**.

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Launch Configuration** to go to the launch configuration management page.

### Selecting a Region

1. Select the project and region for the launch configuration, as shown below:
The choice of region limits the CVM instances that can be added and the CLB instances that can be bound. For example, if the region selected for the launch configuration is Guangzhou, then the CVM instances automatically added in the scaling group are also instances in Guangzhou. In a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances of other regions such as Shanghai, Beijing, Hong Kong, or Toronto.
![Select a region](https://main.qcloudimg.com/raw/07a746c4f69b1a8641b74ce1ddc5cf4f.png)
2. Click ![](//mccdn.qcloud.com/static/img/9d38f7bfbe02a922370765f3adfa58bf/image.png)，and enter the basic information of the launch configuration on the pop-up page.

### Selecting a Model

On the "Create a launch configuration" page, enter the launch configuration name, select the availability zone, and select the model. See the figure below:
![](https://main.qcloudimg.com/raw/a38b03bb3c23c1393169598fcb195897.png)
- Name the configuration.
- Select the same model as the CVM instance that you want to bind to the scaling group.

### Selecting an Image

When creating a launch configuration, you can use either a public or custom image.
It is recommended to use a "custom image" where the environment has already been deployed. The reasons are as follows:
- If you select a public image, the CVM instances produced during scale-out are clean OS, and you have to manually deploy the application environment.
- If you select a custom image, you can create an image of the CVM instance where the environment has already been deployed, and then use the image to batch create CVM instances, which will have the software environment as the original instance after successful creation, helping achieve the purpose of batch deployment.

Bind the image of "a CVM instance for binding to a scaling group". For more information about how to create a CVM instance for binding to a scaling group, see [Creating a Custom Image](https://cloud.tencent.com/document/product/213/4942).
![](https://main.qcloudimg.com/raw/9459776ded2df48d711cf4b6a2bb77a4.png)

### Selecting Storage and Bandwidth

On the "3. Select storage and bandwidth" page, set the disk and network. See the figure below:
![](https://main.qcloudimg.com/raw/c958b41819de424b6e4b7e414c92d71e.png)
>! If you select a CBS cloud disk as the system disk, then you can select a data disk snapshot for the data disk.

If you have large amounts of data, you need lots of data disks to store data. After creating a snapshot file of data disk A, you can use the snapshot file to quickly clone multiple disks for rapid deployment of servers.

When AS automatically adds a new CVM instance, if the data disk snapshot is specified as the data disk in the launch configuration, CBS can automatically mount a data disk containing the set data to the CVM instance when it is launched, so as to implement automatic data copying.

If the data disk snapshot is specified in the launch configuration, it must be ensured that the data disk can be automatically mounted correctly, so that the scaling group can be automatically scaled out. In order to allow automatic data disk mounting when new CVM instances are launched, you need to perform certain operations on the original instance based on which to create the data disk snapshot before setting automatic scaling. For more information, see [here](https://cloud.tencent.com/doc/product/362/5564).

>? AS is free of charge, but the added CVM instances, disks and networks are pay-as-you-go. Prices will be displayed on the page based on your configurations. 

### Setting Information

1. On the "4. Security Group and CVM" tab, select the login method and security group. The CVM instances produced by AS enjoy Cloud Security and Cloud Monitor services for free by default. See the figure below:
![](https://main.qcloudimg.com/raw/e7e5cba6e2c52b768e959a5db4c73bae.png)
2. After the configuration is completed, this entry will be displayed in the launch configuration list on the page, as shown below: See the figure below:
![](https://mc.qcloudimg.com/static/img/67ba31fd6c1f12485bb8f96220aaf6af/image.png)

## Creating a Scaling Group

A scaling group is a collection of CVM instances that follow the same rules and are used for the same scenario.
1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Scaling Group** to go to the scaling group management page.

### Creating a Scaling Group

1. Click ![](//mccdn.qcloud.com/static/img/9d38f7bfbe02a922370765f3adfa58bf/image.png) and enter the basic information of the scaling group on the pop-up page. Fields marked with ![](//mccdn.qcloud.com/static/img/f9df27a1d1e0d42a7ff08dd884bfa34c/image.png) are required. See the figure below:
![](https://mc.qcloudimg.com/static/img/2fb365611291fb8917637dba46f398f4/image.png)
 - The current number of CVM instances in the scaling group will be maintained between the minimum and maximum capacity.
	- The starting instance quantity defines the number of CVM instances in the scaling group at the very beginning.
	- If the current number of CVM instances is less than the minimum scaling capacity, AS will automatically add instances to make the former equal to the latter.
	- If the current number of CVM instances is greater than the maximum scaling capacity, AS will automatically remove instances to make the former equal to the latter.
 - Select an existing launch configuration or create a new one.
 - Select the network, availability zone, and removal policy.
 - (Optional) Associate with an existing CLB instance or create a new one.
2. After the configuration is completed, this entry will be displayed in the list of scaling groups on the page. See the figure below:
![](https://mc.qcloudimg.com/static/img/c1c64cdb16c11aaa6d31bc4781db62c4/image.png)

### Adding a CVM Instance (Optional)

Add the CVM instance in the CVM instance list that you want to bind. After the configuration is completed, this entry will be displayed in the launch configuration list on the page, as shown below:
![](https://mc.qcloudimg.com/static/img/e3232872ad5fe19e89c9eb7306418a3d/image.png)
>? If you are unable to add or remove an CVM here, please check the maximum and minimum capacity setting.

## Creating a Scaling Policy

A scaling group increases or decreases the number of CVM instances according to the scaling policy:
- Create a **scheduled task** to perform a scheduled scaling action, which can be set to run periodically.
- Create an **alarm-triggered policy** to perform a scaling action based on Cloud Monitor metrics (such as CPU utilization and memory usage).

### Creating a Scheduled Task

If the changes in your business load are predictable, you can set up a scheduled task to plan your device scaling. You can use this feature to automatically add or remove CVM instances at a specified time point and periodically, elastically responding to business load changes, increasing device utilization, and reducing deployment and instance costs.

1. On the **Scaling group** page, click "Scaling group" to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
2. Select the "Scheduled task" tab and click **Create**.
![Scheduled task](https://main.qcloudimg.com/raw/9ed7c9dbfc82035a82136f5f215cc12a.png)
3. On the creation page, specify information such as the task name, run time, and action to be run. You can also select **Repeat** to run the scheduled task on a periodic basis.
![Create a scheduled task](https://main.qcloudimg.com/raw/5ebba7a45ab3db576eb3d8fd92246cfe.png)
4. After the configuration is completed, the scheduled task will be displayed in the list on the page. Below is an example:
![Scheduled task list](https://main.qcloudimg.com/raw/f21339e4d6650929e4b69ff61ce371e5.png)

### Creating an Alarm-triggered Policy

If you want to adjust your application deployment based on CVM metrics, you can create a custom alarm-triggered policy. When the business load reaches the metric threshold, CVM instances will be added or removed automatically, enabling you to elastically respond to business load changes, increase device utilization, and reduce deployment and instance costs.

>?
> - When a scaling group is created, an alarm-triggered policy for failed pings is created by default to replace unhealthy servers.
> - Before using an alarm-triggered policy, you need to install the latest version of Cloud Monitor agent in the image of CVM. For more information, please see [Installing Monitoring Components](/doc/product/248/安装监控组件).

1. On the **Scaling group** page, click a Scaling group ID to go to the scaling group management page.
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
2. Select the "Alarm-triggered policy" tab and click **Create**.
![](https://main.qcloudimg.com/raw/2fac8567b4042a2c65c1906ae8f8396d.png)
3. On the creation page, set the alarm-triggered policy. In the scaling group, the alarm-triggered policy automatically adds or removes the specified number of percentage of CVM instances based on Cloud Monitor performance metrics (such as CPU, memory, and bandwidth).
You can also copy an existing policy in an existing scaling group to the current scaling group.
![Create an alarm-triggered policy](https://main.qcloudimg.com/raw/41c7c0f95256e5b8492dc58826d13cd4.png)
4. After the configuration is completed, the alarm-triggered policy will be displayed in the list on the page. Below is an example:
![Alarm-triggered policy list](https://main.qcloudimg.com/raw/3b2af877848e11c337901172055ba466.png)


