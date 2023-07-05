## Introduction
Removal protection allows you to specify CVMs in the scaling group that will not be removed during scale-in. When scale-in occurs, AS will remove other CVMs.

You can enable **Removal Protection** for one or more instances in a scaling group. You can modify the scaling group or the instance protection configuration at any time.

If a scale-in activity occurs when all the remaining instances in the scaling group are marked with “Removal Protection”, AS will decrease the capacity instead of removing any instances.

## Application Scenarios

Usually, the CVMs in a scaling group are stateless and can be removed at any time. However, in the following circumstances, you may need to prevent certain instances from being removed during scale-in:
- **One CVM for multiple uses:** if the CVM in the cluster is also used for other purposes, for example, if it is also used for storing the data generated in the cluster, then this CVM is actually stateful.
- **Avoid misoperation:** if you worry that your business will be affected due to a policy settings error, you can enable **Removal Protection** for some CVMs. In this way, AS will never remove these CVMs in scale-in, and the tunnel "Request-LB-CVM" will remain unblocked.

## Setting Up
1. Log in to the Auto Scaling console and select **[Scaling Groups](https://console.cloud.tencent.com/autoscaling/group)** in the left sidebar.
2. On the **Scaling Groups** page, select the target scaling group ID to go to the details page of the scaling group.
3. Select the **Associated Instances** tab and click **Enable Removal Protection** on the right side of the row of the target instance, as shown in the following figure:
![](https://mc.qcloudimg.com/static/img/f913547df4ed60c7aecb8784b1965a07/1.jpg)
3. Click **OK** in the pop-up box.
