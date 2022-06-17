
## Overview
TKE provides users with an out-of-the-box audit dashboard and can automatically configure dashboards of auditing overview, node operation overview, K8s object operation overview, and aggregation search for the clusters with the feature of **Cluster Auditing** enabled. With user-defined filter items, and built-in CLS global search, TKE makes it convenient for users to observe and search various cluster operations, so as to find and locate problems in time.




## Features
Five dashboards are configured in the **Auditing search**, namely **Auditing overview**, **Node operation overview**, **K8s object operation overview**, **Aggregation search**, and **Global search**. Follow the steps below to go to the **Auditing search** page and use the corresponding features:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Enable the Cluster Auditing feature. For more information, see [Cluster Auditing](https://intl.cloud.tencent.com/document/product/457/38338).
3. In the left sidebar, select **Log Management** > **Audit Logs** to open the “Auditing search” page.


### Auditing overview
When you want to view the operation of the entire cluster APIserver, you can set filter conditions on the "Auditing overview" page, view the summary statistics of the core audit log, and display the data comparison within a period, for example, core audit log statistics, distribution, important operation trends, etc.
You can customize the filter items as needed (up to 10 filter items can be set).

You can modify the custom fields of the filter item.

You can view more statistics on this page as shown below:
- Core audit log statistics dashboard:
- Distribution dashboard:
- Important operation trend dashboard:





### Node operation overview
When you need to troubleshoot node problems, you can set filters on the **Node operation overview** page to view dashboards of various node operations, including `create`, `delete`, `patch`, `update`, `block`, and `evict`.

### K8s object operation overview
When you need to troubleshoot problems related to K8s objects (such as a certain workload), you can go to the **K8s object operation overview** page, and set filter conditions to view the details of the operation overview, the corresponding users, and the corresponding audit log list of various K8s objects.

### Aggregation search
When you want to view the distribution trend of audit logs in a certain dimension, you can set filter conditions on the "Aggregation search" page to view the sequence diagrams of various important operations. The dimensions include the user, namespace, operation type, status code, resource type, and the corresponding audit log list.

### Global search
Global search dashboard, with built-in CLS search analysis page, is convenient for users to quickly search all audit logs in the TKE console.


### Configuring alarms based on the dashboards

You can configure alarms based on the preset dashboards. When the conditions you set are reached, the alarms will be triggered. The steps are as follows:
1. Click **Add alarm** on the right of the target dashboard.
2. Create an alarm policy in **Alarm Policy** in the **[CLS console](https://console.cloud.tencent.com/cls/)** as instructed in [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/614/39574).

