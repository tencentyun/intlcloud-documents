## Introduction

AS allows you to dynamically add or remove instances in a scaling group based on monitoring metrics, provided that you define the alarm trigger policy, including the status of the monitoring metrics that trigger the scaling, and how you want to scale in response to changing demand.

To create an alarm policy, you need to specify the conditions and actions:
- Condition format: A metric + Threshold + Period + Number of periods during which the threshold is reached. That is, the metric at the threshold lasts for the number of periods that you specified.
- Execution actions: Sending notification(s) + adding or removing the specified number of CVMs.

We recommended you create two policies for each scaling group, one for scale-out and the other for scale-in. Once the traffic to your web application reaches the threshold of the alarm policy, AS executes the associated policy to scale your group in (by terminating instances) or out (by launching instances).

This is shown in the figure below:
![](https://mc.qcloudimg.com/static/img/83557f69f860be57cf464b2b45ab31c5/1.jpg)


## Scenarios

For example, you have an e-commerce web application that currently runs on five instances. You plan to carry out an operational activity, and are concerned that the access traffic is much greater than you had expected. You can configure a scaling group to add two instances when the load on the current instance reaches 70%, and terminate extra instances when the load decreases to 40%.
![](https://mc.qcloudimg.com/static/img/92435c4281be33320200ce3f69bbc36c/AS-Expanding+and+Reducing-Managing+Alarm+Triggering+Policies.jpg)

## Directions

1. Log in to [Auto Scaling Console](https://console.cloud.tencent.com/autoscaling/config), and select **Scaling group** in the left sidebar.

2. Select the scaling group to modify, and click the ID of a scaling group to enter the **Scaling Group Details** page.
![](https://mc.qcloudimg.com/static/img/cebad1b79ccba9fb9548c2bd2c30a210/2.jpg)

3. Select the **Alarm Trigger Policy** tab, and manage the alarm trigger policy associated with the scaling group on this page.
	- Click **Create** to add an alarm trigger policy.
	- Click **Delete** to delete the alarm trigger policy.
![](https://mc.qcloudimg.com/static/img/570e5bd24b8975c65dd939bc9052d5a3/3.jpg)


## Preventing Specified CVMs from being Removed by the Scaling Policy
For the proper running of your existing business, if the CVMs in the cluster are used for the following purposes, you need to prevent them from being removed by the scale-in policy:

- **Multiple purposes**: Apart from the tasks specified by the cluster, the CVM in the cluster is also used for other purposes, for example, the CVM is used as both a cache server and a file server.

- **Data storage**: The CVM is stateful or stores data that other CVMs do not have. For example, the CVM stores the incremental data of other running CVMs in a cluster.

- **Image/Snapshot updates**: The CVM is used to regularly update images and snapshots.


**Configuration:**

**Step 1**: In the [Scaling group](https://console.cloud.tencent.com/autoscaling) page, click the scaling group to which the CVM belongs to go to the management page.

**Step 2**: In the **Instance List** at the bottom of the management page, click **Enable removal protection** for the CVM.
