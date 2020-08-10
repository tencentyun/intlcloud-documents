You can use scaling policies to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm-triggered policy** to perform scaling based on Cloud Monitor metrics (such as CPU utilization and memory usage).

## Creating a Scheduled Action

### Scenario

If your load changes are predictable, you can set a scheduled action to plan your scaling activities. This feature can automatically add or remove CVM instances according to a schedule. This allows you to flexibly cope with traffic load changes and improve device utilization while reducing deployment and instance costs.

### Directions

1. Log in to the Auto Scaling console and select **[Scaling Groups](https://console.cloud.tencent.com/autoscaling/group)** in the left sidebar.
2. On the **Scaling Groups** page, select a scaling group ID, as shown in the following figure:
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
3. On the management page of the scaling group, select the **Scheduled Action** tab and click **Create**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/50a8f16c5826b2b1886e1e9aabba8671.png)
4. In the **Create Scheduled Action** window that pops up, specify the action name, startup time, activity, and other information as shown in the following figure:
![](https://main.qcloudimg.com/raw/196e482efed765613323dea3703532e7.png)
5. Click **OK** to complete the configuration. Then, the created scheduled action will be displayed in the list on the page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/3bd91d894eeefb2b3fc5119500694574.png)

## Creating an Alarm-Triggered Policy

### Scenario

If you want to adjust the scaling based on CVM metrics, you can create an alarm-triggered policy. This policy helps increase or decrease instances in the scaling group to handle dynamic volumes, increase machine utilization, and reduce expenses on deployment and instances.

### Directions

>?
> - When a scaling group is created, a ping unreachable alarm-triggered policy is created by default, which is used to replace unhealthy CVMs.
> - Before using an alarm-triggered policy, you need to install the latest version of Cloud Monitor agent in the CVM image. For more information, see [Installing Monitoring Components](https://intl.cloud.tencent.com/document/product/248/6211).

1. Log in to the Auto Scaling console and select **[Scaling Groups](https://console.cloud.tencent.com/autoscaling/group)** in the left sidebar.
2. On the **Scaling Groups** page, select a scaling group ID, as shown in the following figure:
![Scaling group](https://main.qcloudimg.com/raw/2bd1126836549e378ac52a664e107e79.png)
3. On the management page of the scaling group, select the **Alarm-triggered Policy** tab and click **Create**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/c3e776e6e456d2e6fa1ddd5e63e26653.png)
4. In the **Create an Alarm-triggered Policy** window that pops up, set up the policy as shown in the following figure:
The scaling policy automatically adds or removes CVM instances in the scaling group by a specified number or percentage based on cloud monitoring performance metrics (such as CPU utilization, memory usage, and bandwidth). You can also copy existing policies from an existing scaling group to the current scaling group.
![](https://main.qcloudimg.com/raw/696dd366766aac9dce3e966bc86922ec.png)
5. Click **OK** to complete the configuration, and the created alarm-triggered policy will be displayed in the list on the page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/47324c543af7f14dc6b11c26494346b2.png)




