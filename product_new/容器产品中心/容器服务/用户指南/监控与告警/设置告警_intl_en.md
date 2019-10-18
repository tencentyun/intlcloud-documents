## Operation Scenario
Tencent Cloud TKE supports setting alarms for three cluster dimensions: cluster, node, and pod. Setting reasonable alarms for your clusters will assist in locating exceptions quickly, thus reducing your business risks.
>!
> - TKE only provides alarms for the metrics and events most crucial to the healthy operation of Kubernetes clusters.
> - Alarms set in TKE can only be managed from the TKE console.
> - Alarms set in TKE can coexist with those set in [Cloud Monitoring](https://console.cloud.tencent.com/monitor/overview), but it is still recommended to use Cloud Monitoring services to set alarms for CVM and Load Balancer resources.

## Prerequisites

Log into the [TKE console](https://console.cloud.tencent.com/tke2).

## Steps 

1. Select the alarm settings based on your actual needs.
 >?If no alarms have been set for the list of clusters, then a message will appear: **Alarm not set**. This message will disappear after you set an alarm.

 - Select **Cluster** > **Operations** > **Configure Alarm Policy** to view the list of alarms for the current cluster. See the figure below:
![](https://main.qcloudimg.com/raw/157053719e9c9cff2d0344083c084a3b.png)
 - Select **Alarm Policies** > **Cluster** to select a cluster and view its alarm list. See the figure below:
![](https://main.qcloudimg.com/raw/18ee3737d9351ba09a2f8b343f13ab29.png)
2. Click **Create** or **Create a Policy** to create an alarm policy. See the figure below:
>!Alarms are only valid for the cluster for which they are configured.
>
![](https://main.qcloudimg.com/raw/ef8fa47f76f9a3248432ac917ab33b3a.png)



