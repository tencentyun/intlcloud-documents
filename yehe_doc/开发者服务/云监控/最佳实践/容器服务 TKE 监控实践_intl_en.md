## New TKE Monitoring Features

● Monitored objects can be updated automatically.
● Workload/Component/Node monitoring scenarios are added.
● More monitoring metrics are added. The total number of new TKE metrics reaches 140.
● You can block a special object (such as a frequently alarming pod) in a specific monitoring dimension.


## Directions

This document describes how to [automatically update a monitored object in the dashboard](#step1), [automatically update an alarm object](#step2), and [block a frequently triggered alarm object](#step3) by taking the "TKE monitoring - pod" dimension as an example.


<span id ="step1"></span>
### Automatically updating monitored object in dashboard

1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor).
2. Select **Dashboard** > **Dashboard List** > **Create Dashboard** > **Create Chart**.
3. Configure the monitoring chart as detailed below:
 -  **Monitoring Type**: select **Cloud Product Monitoring** here.
 -  **Metric**: select "TKE (New) - pod" as the service and "CPU utilization (%)" as the metric here.
 -  **Filter**: you can filter the objects to be bound to the chart by dimension (such as region, cluster, namespace, and workload).
    -  **Region**: select the region of the monitored object.
    -  **Cluster**: select the cluster of the monitored object.
 -  **Filter**: you need to configure two filters, namely, the namespace and workload balance type, to monitor all pods under the specified workload and to automatically update the monitored object in the dashboard when pods are created/updated frequently, as shown below:
    ![](https://main.qcloudimg.com/raw/c45372837b44f2c8f05b7e3cda64bc2d.png)
4. After completing the configuration, click **Save** in the top-right corner of the page to save the chart.

<span id ="step2"></span>
### Automatically updating alarm object

1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor).
2. Select **Alarm Configuration** > **Alarm Policy** > **Create** to enter the alarm policy creation page.
3. Select "TKE (New) - pod" as the policy type and configure the alarm object as detailed below:
   - **Region**: select the region of the monitored object.
   - **Cluster**: select the cluster of the monitored object.
   - **Filter**: you need to configure two filters, namely, the namespace and workload balance type, to monitor all pods under the specified workload and to automatically update the alarm object when pods are created/updated frequently, as shown below:
 ![](https://main.qcloudimg.com/raw/d1fa4734d7a250fef6e7b5c95665640a.png)
>?For more information on how to configure an alarm, please see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

<span id ="step3"></span>
### Blocking frequently triggered alarm object

When a pod frequently triggers an alarm, you can block some or all alarm objects under the node as instructed below.

As shown below, you can block some pod alarms by configuring the "!=" operator for the pod name.
![](https://main.qcloudimg.com/raw/eef40dd363ab34a9069a067f919ee09e.png)








