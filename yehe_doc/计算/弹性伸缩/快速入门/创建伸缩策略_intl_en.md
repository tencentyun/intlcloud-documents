You can use scaling policies to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm trigger policy** to perform scaling adjusted by Cloud Monitor metrics (for example, CPU utilization and memory usage).

## Creating a Scheduled Scaling Action

### Scenario

Scheduled actions work better in business scenarios where the volume is stable and predictable. You can use them to automatically add or remove CVM instances at a specified point in time or periodically to meet changing needs, increase device utilization, and reduce deployment and instance costs.

### Directions

1. Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling groups", as shown in the following figure:
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
3. On the scaling group management page, click the "Scheduled Action" tab and then click **Create**, as shown in the following figure:
![Scheduled actions](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
4. In the "Create a Scheduled Action" window that appears, specify information such as the scheduled action name, execution time, and activities to be executed. You can also select "Repeat" to define the interval of performing the scheduled action, as shown in the following figure:
![Create a scheduled action](https://main.qcloudimg.com/raw/196e482efed765613323dea3703532e7.png)
5. Click **OK** to finish the configuration, and the created scheduled action appears in the list on the page, as shown in the following figure:
![Scheduled action list](https://main.qcloudimg.com/raw/3bd91d894eeefb2b3fc5119500694574.png)

## Creating an Alarm Trigger Policy

### Scenario

If you wish to adjust business deployment based on CVM metrics, you can customize an alarm trigger policy, which will automatically increase or decrease the number of CVM instances when the business load pushes the metrics to the thresholds. This flexibly handles with traffic load changes, improves device utilization, and reduces deployment and instance costs.

### Directions

>
> - When a scaling group is created, an alarm trigger policy for unreachable pings is created by default to replace unhealthy CVMs.
> - Before using an alarm trigger policy, you need to install the latest version of Cloud Monitor agent in the CVM's image. For more information, see [Installing Monitoring Components](/doc/product/248/安装监控组件).

1. Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling).
2. On the "Scaling group" page, click "Scaling group", as shown in the following figure:
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
3. On the scaling group management page, click the "Alarm Trigger Policy" tab and then click **Create**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/c3e776e6e456d2e6fa1ddd5e63e26653.png)
4. In the "Create an Alarm-Triggered Policy" window that appears, set the alarm policy, as shown in the following figure:
The alarm policy automatically increases or decreases CVM instances by a specified number or percentage for the scaling group based on cloud monitoring performance metrics (such as the CPU utilization, memory usage, and bandwidth). You can copy existing policies from an existing scaling group to the current scaling group.
![Create an alarm-triggered policy](https://main.qcloudimg.com/raw/696dd366766aac9dce3e966bc86922ec.png)
5. Click **OK** to finish the configuration, and the created alarm policy appears in the list on the page, as shown in the following figure:
![Alarm-triggered policy list](https://main.qcloudimg.com/raw/47324c543af7f14dc6b11c26494346b2.png)




