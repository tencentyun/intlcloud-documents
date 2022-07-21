
## Overview
TKE provides users with an out-of-the-box audit dashboard and can automatically configure dashboards of auditing overview, node operation overview, K8s object operation overview, and aggregation search for the clusters with the feature of **Cluster Auditing** enabled. With user-defined filter items, and built-in CLS global search, TKE makes it convenient for users to observe and search various cluster operations, so as to find and locate problems in time.




## Feature Description
Five dashboards are configured in the **Auditing search**, namely **Auditing overview**, **Node operation overview**, **K8s object operation overview**, **Aggregation search**, and **Global search**. Follow the steps below to go to the **Auditing search** page and use the corresponding features:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Enable the Cluster Auditing feature. For more information, see [Cluster Auditing](https://intl.cloud.tencent.com/document/product/457/38338).
3. Select **Log Management > Audit Logs** in the left sidebar to go to the “Audit log search” page.


### Auditing overview
When you want to view the operation of the entire cluster APIserver, you can set filter conditions on the "Auditing overview" page, view the summary statistics of the core audit log, and display the data comparison within a period, for example, core audit log statistics, distribution, important operation trends, etc.

You can view more statistics on this page, as shown below:
- Core audit log statistics dashboard:
![](https://qcloudimg.tencent-cloud.cn/raw/72e7e252cb3bf2eaa643ad06cee0f3a4.png)
- Distribution dashboard:
![](https://qcloudimg.tencent-cloud.cn/raw/5495968f3f4e4ee78c24e987903dc32c.png)
- Important operation trend dashboard:
![](https://qcloudimg.tencent-cloud.cn/raw/960434920930f2528443a4f103eef372.png)





### Node operation overview
When you need to troubleshoot node problems, you can set filters on the **Node operation overview** page to view dashboards of various node operations, including `create`, `delete`, `patch`, `update`, `block`, and `evict`.
![](https://qcloudimg.tencent-cloud.cn/raw/150055420c58fa2c1e0d7f64bf278b63.png)

### K8s object operation overview
When you need to troubleshoot problems related to K8s objects (such as a certain workload), you can go to the **K8s object operation overview** page, and set filter conditions to view the details of the operation overview, the corresponding users, and the corresponding audit log list of various K8s objects.
![](https://qcloudimg.tencent-cloud.cn/raw/9bd056c529943cd18a19f392898cc004.png)

### Aggregation search
When you want to view the distribution trend of audit logs in a certain dimension, you can set filter conditions on the "Aggregation search" page to view the sequence diagrams of various important operations. The dimensions include the user, namespace, operation type, status code, resource type, and the corresponding audit log list.
![](https://qcloudimg.tencent-cloud.cn/raw/6132572a50dd7375dedbad453ec2c62d.png)

### Global search
Global search dashboard, with built-in CLS search analysis page, is convenient for users to quickly search all audit logs in the TKE console.
![](https://qcloudimg.tencent-cloud.cn/raw/28de4f8e3478c859f8ce53088e5ee580.png)


### Configuring alarms based on the dashboards

You can configure alarms based on the preset dashboards. When the conditions you set are reached, the alarms will be triggered. The steps are as follows:
1. Click **Quickly add alarm** on the right of the target dashboard.
2. Create an alarm policy in **Alarm Policy** in the **[CLS console](https://console.cloud.tencent.com/cls/)** as instructed in [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/614/39574).

