## Overview

You can use scaling policies to increase or decrease the number of CVM instances in your scaling group:
- Create a **scheduled action** to perform scheduled scaling, which can be set to run periodically.
- Create an **alarm-triggered policy** to perform scaling based on Cloud Monitor metrics (such as CPU utilization and memory usage).


## Directions

### Creating a scheduled action

If your load changes are predictable, you can set scheduled actions to plan your scaling activities. This feature can automatically increase or decrease CVM instances according to a schedule. This allows you to flexibly cope with traffic load changes and improve device utilization while reducing deployment and instance costs.
1. Go to the **[Scaling group](https://console.cloud.tencent.com/autoscaling/group?rid=1)** page and select the ID of the target scaling group to enter its details page.
2. Select the **Scheduled action** tab, and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/8157fcd7ee03c86af5042b357ce5c4f8.png)
3. In the **Create scheduled action** window that pops up, specify the action name, scaling group activities, repeat cycle, and other information.
4. After completing the configuration, click **OK** to view the scheduled action.
![](https://qcloudimg.tencent-cloud.cn/raw/27bb342e8aef8100fa9e3e23377af78a.png)


### Creating an alarm policy

If you want to perform scaling based on CVM metrics, you can create an alarm policy to plan device scaling. This policy helps you automatically increase or decrease the number of instances in your scaling group to flexibly handle business load changes, increase device utilization, and reduce deployment and instance costs.


<dx-alert infotype="explain" title="">
 - When a scaling group is created, a ping unreachable alarm-triggered policy is created by default, which is used to replace unhealthy CVMs.
 - Before using an alarm policy, you need to install the latest version of Cloud Monitor Agent in the CVM image. For more information, see [Installing Monitor Components](https://intl.cloud.tencent.com/document/product/248/6211).
</dx-alert>


1. Go to the **[Scaling group](https://console.cloud.tencent.com/autoscaling/group?rid=1)** page and select the ID of the target scaling group to enter its details page.
2. Select the **Alarm-triggered policy** tab, and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/c11b3994d5f1eafb0ca80a167ed3e41f.png)
3. In the **Create alarm policy** window that pops up, configure the Cloud Monitor metrics (such as CPU utilization, memory usage, and bandwidth), which will be used as the basis of adding or removing CVM instances by a specified number or percentage.
You can also choose **Use existing policy (optional)** to copy an existing policy from an existing scaling group to the current scaling group.
![](https://qcloudimg.tencent-cloud.cn/raw/a1d45712cfae19d74cd7236c3814961d.png)
4. After completing the configuration, click **OK** to view the alarm-triggered policy.
![](https://qcloudimg.tencent-cloud.cn/raw/ddadd2956437ddb3abecffb9759411a3.png)
