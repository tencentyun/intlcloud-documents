You can use scaling policies to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm trigger policy** to perform scaling adjusted by Cloud Monitor metrics (e.g., CPU utilization and memory usage).

## Creating a Scheduled Scaling Action

### Scenario

Scheduled Scaling works better in business scenarios where volume is stable and predictable. You can use it to automatically add/remove CVM instances at a specified point of time or periodically to meet changing needs, increase machine utilization, and reduce expenses on deployment and instances. 

### Directions

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling group". See the figure below:
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
3. On the scaling group management page, select the "Scheduled Action" tab and click **Create**. See the figure below:
![Scheduled Action](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
4. In the "Create Scheduled Action" window that pops up, specify information such as the action name, execution startup time, and scaling activities to be run. You can also select **Duplicate** to run the scheduled action on a periodic basis. See the figure below:
![Create scheduled action](https://main.qcloudimg.com/raw/196e482efed765613323dea3703532e7.png)
5. Click **OK** to complete the set-up, then you will see the created scheduled action on the list, as shown below:
![Scheduled action list](https://main.qcloudimg.com/raw/3bd91d894eeefb2b3fc5119500694574.png)

## Creating an Alarm Trigger Policy

### Scenario

If you want to adjust the scaling based on CVM metrics, you can create an alarm-triggered policy. This policy helps you automatically adjust (increase or decrease) the number of instances in your scaling group to handle dynamic volumes, increase machine utilization, and reduce expenses on deployment and instances.

### Directions

>- By default,  a ping is created in a scaling group to trigger the alarm that tells you to replace unhealthy servers.
> - Before using an alarm-triggered policy, you need to install the latest version of Cloud Monitor agent in CVM's image. For more information, please see [Installing Monitoring Components](https://intl.cloud.tencent.com/document/product/248/6211).

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling group". See the figure below:
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
3. On the scaling group management page, select the "Alarm Trigger Policy" tab and click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/c3e776e6e456d2e6fa1ddd5e63e26653.png)
4. In the "Create Alarm Policy" window, set the alarm policy. See the figure below:  
When the Alarm Trigger policy is in effect, the scaling group adjusts the number of instances or the percentage of the instance by Cloud Monitor metrics (e.g., CPU utilization, memory usage, and bandwidth). You can also copy an existing policy (optional) in an existing scaling group to the current scaling group.
![Create an alarm-triggered policy](https://main.qcloudimg.com/raw/696dd366766aac9dce3e966bc86922ec.png)
5. Click **OK** to complete the set-up, then you will see the created alarm trigger policy on the list on the page, as shown below:
![Alarm-triggered policy list](https://main.qcloudimg.com/raw/47324c543af7f14dc6b11c26494346b2.png)



