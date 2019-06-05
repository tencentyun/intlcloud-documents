A scaling group increases or decreases the number of CVM instances according to the scaling policy:
- Create a **scheduled task** to perform a scheduled scaling action, which can be set to run periodically.
- Create an **alarm-triggered policy** to perform a scaling action based on Cloud Monitor metrics (such as CPU utilization and memory usage).

## Creating a Scheduled Task

### Scenario

If the changes in your business load are predictable, you can set up a scheduled task to plan your device scaling. You can use this feature to automatically add or remove CVM instances at a specified time point and periodically, elastically responding to business load changes, increasing device utilization, and reducing deployment and instance costs.

### Directions

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling group". See the figure below:
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
3. On the scaling group management page, select the "Scheduled task" tab and click **Create**. See the figure below:
![Scheduled task](https://main.qcloudimg.com/raw/9ed7c9dbfc82035a82136f5f215cc12a.png)
4. In the "Create a scheduled task" window that pops up, specify information such as the task name, run time, and action to be run. You can also select **Repeat** to run the scheduled task on a periodic basis. See the figure below:
![Create a scheduled task](https://main.qcloudimg.com/raw/5ebba7a45ab3db576eb3d8fd92246cfe.png)
5. Click **OK** to complete the setup. The created scheduled task will be displayed in the list on the page, as shown below:
![Scheduled task list](https://main.qcloudimg.com/raw/f21339e4d6650929e4b69ff61ce371e5.png)

## Creating an Alarm-triggered Policy

### Scenario

If you want to adjust your application deployment based on CVM metrics, you can create a custom alarm-triggered policy. When the business load reaches the metric threshold, CVM instances will be added or removed automatically, enabling you to elastically respond to business load changes, increase device utilization, and reduce deployment and instance costs.

### Directions

>?
> - When a scaling group is created, an alarm-triggered policy for failed pings is created by default to replace unhealthy servers.
> - Before using an alarm-triggered policy, you need to install the latest version of Cloud Monitor agent in the image of CVM. For more information, please see [Installing Monitoring Components](/doc/product/248/安装监控组件).

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling group". See the figure below:
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
3. On the scaling group management page, select the "Alarm-triggered policy" tab and click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/2fac8567b4042a2c65c1906ae8f8396d.png)
4. In the "Create an alarm-triggered policy" window, set the alarm policy. See the figure below:
In the scaling group, the alarm-triggered policy automatically adds or removes the specified number of percentage of CVM instances based on Cloud Monitor performance metrics (such as CPU, memory, and bandwidth). You can also copy an existing policy (optional) in an existing scaling group to the current scaling group.
![Create an alarm-triggered policy](https://main.qcloudimg.com/raw/41c7c0f95256e5b8492dc58826d13cd4.png)
5. Click **OK** to complete the setup. The created alarm-triggered policy will be displayed in the list on the page, as shown below:
![Alarm-triggered policy list](https://main.qcloudimg.com/raw/3b2af877848e11c337901172055ba466.png)



