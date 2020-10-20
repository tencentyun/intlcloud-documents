## Operation Scenario
Tencent Cloud TKE supports setting alarms for three cluster dimensions: cluster, node, and pod. Setting reasonable alarms for your clusters will assist in locating exceptions quickly, thus reducing your business risks.
>!
> - TKE only provides alarms for the metrics and events most crucial to the healthy operation of Kubernetes clusters.
> - Alarms set in TKE can only be managed from the TKE console.
> - Alarms set in TKE can coexist with those set in [Cloud Monitoring](https://console.cloud.tencent.com/monitor/overview), but it is still recommended to use Cloud Monitoring services to set alarms for CVM and Load Balancer resources.

## Prerequisites

Log in to the [TKE Console](https://console.cloud.tencent.com/tke2).

## Directions 

1. Select the alarm settings based on your actual needs.
 >? If no alarms have been set for the list of clusters, then a message will appear: **Alarm not set**. This message will disappear after you set an alarm.

 - Choose **Cluster** > **Operations** > **Configure Alarm Policy** to view the list of alarms for the current cluster. See the figure below:
![](https://main.qcloudimg.com/raw/1b164e1f17b0fc1b06eb2251b35e4a8b.png)
 - Choose **Cluster OPS** > **Alarm Policies** > **Cluster**, select a cluster, and view its alarm list. See the figure below:
![](https://main.qcloudimg.com/raw/aac05a04f5651d934c25d300816a0701.png)
2. Click **Create** or **Create a Policy** to create an alarm policy. See the figure below:
>! Alarms are only valid for the cluster for which they are configured.

![](https://main.qcloudimg.com/raw/a84350464b6bfc13b186f449d4f28979.png)

