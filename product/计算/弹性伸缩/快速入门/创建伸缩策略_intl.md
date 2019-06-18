You can use scaling policies to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm-triggered policy** to perform scaling adjusted by Cloud Monitor metrics (e.g., CPU utilization and memory usage).

## Creating a Scheduled Scaling Action

### Scenario

Scheduled Scaling works better in business scenarios where volume is stable and predictable. You can use it to automatically add/remove CVM instances at a specified point of time or periodically to meet changing needs, increase machine utilization, and reduce expenses on deployment and instances. 

### Directions

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling group". See the figure below:
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
3. On the scaling group management page, select the "Scheduled Action" tab and click **Create**. See the figure below:
![Scheduled Action](https://main.qcloudimg.com/raw/9ed7c9dbfc82035a82136f5f215cc12a.png)
4. In the "Create Scheduled Action" window that pops up, specify information such as the action name, execution startup time, and scaling activities to be run. You can also select **Duplicate** to run the scheduled action on a periodic basis. See the figure below:
![Create scheduled action](https://main.qcloudimg.com/raw/5ebba7a45ab3db576eb3d8fd92246cfe.png)
5. Click **OK** to complete the set-up, then you will see the created scheduled action on the list, as shown below:
![Scheduled action list](https://main.qcloudimg.com/raw/f21339e4d6650929e4b69ff61ce371e5.png)

## Creating an Alarm Trigger Policy

### Scenario

If you want to adjust the scaling based on CVM metrics, you can create an alarm-triggered policy. This policy helps you automatically adjust (increase or decrease) the number of instances in your scaling group to handle dynamic volumes, increase machine utilization, and reduce expenses on deployment and instances.

### Directions

>?
> - By default,  a ping is created in a scaling group to trigger the alarm that tells you to replace unhealthy servers.
> - Before using an alarm-triggered policy, you need to install the latest version of Cloud Monitor agent in CVM's image. For more information, please see [Installing Monitoring Components](/doc/product/248/安装监控组件).

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling group". See the figure below:
![Scaling group](https://main.qcloudimg.com/raw/d6e81e4df05c1c8e77368c50b765a55a.png)
3. On the scaling group management page, select the "Alarm Trigger Policy" tab and click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/2fac8567b4042a2c65c1906ae8f8396d.png)
4. In the "Create Alarm Policy" window, set the alarm policy. See the figure below:  
When the Alarm Trigger policy is in effect, the scaling group adjusts the number of instances or the percentage of the instance by Cloud Monitor metrics (e.g., CPU utilization, memory usage, and bandwidth). You can also copy an existing policy (optional) in an existing scaling group to the current scaling group.
![Create an alarm-triggered policy](https://main.qcloudimg.com/raw/41c7c0f95256e5b8492dc58826d13cd4.png)
5. Click **OK** to complete the set-up, then you will see the created alarm trigger policy on the list on the page, as shown below:
![Alarm-triggered policy list](https://main.qcloudimg.com/raw/3b2af877848e11c337901172055ba466.png)



