
## Overview
TKE provides users with an out-of-the-box auditing dashboard and can automatically configure dashboards of auditing overview, node operation, K8s object operation, aggregation search for the clusters with the feature of **Cluster Auditing** enabled. With user-defined filter items, and built-in CLS global search, TKE makes it convenient for users to observe and search various cluster operations, so as to find and locate problems in time.




## Feature Description
Five dashboards are configured in the **Auditing Search**, namely **Auditing Overview**, **Node Operation Overview**, **K8s Object Operation Overview**, **Aggregation Search**, and **Global Search**. Please follow the steps below to go to the **Auditing Search** page and use the corresponding features:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Enable **Cluster Auditing**. For more information, see [Cluster Audit](https://intl.cloud.tencent.com/document/product/457/38338).
3. Click **Cluster Ops** > **Auditing Search** in the left sidebar to go to the **Auditing Search** page.


### Auditing overview
When you want to view the operation of the entire cluster APIserver, you can set filter conditions on the "Auditing Overview" page, view the summary statistics of the core audit log, and display the data comparison within a period, for example, core audit log statistics, distribution, important operation trends, etc.
You can customize the filter items as needed (up to 10 filter items can be set).
You can modify the custom fields of the filter item .

You can view more statistics on this page as follows:
- Core audit log statistics dashboard:

- Distribution dashboard

- Important operation trend dashboard:





### Node operation overview
When you need to troubleshoot node-related issues, you can set filter conditions on the **Node Operation Overview** page to view various dashboards related to node operations, including creation, deletion, patching, updating, cordoning, and draining .

### K8s object operation overview
When you need to troubleshoot problems related to K8s objects (such as a certain workload), you can set filter conditions on the **K8s Object Operation Overview** page to view the details of the operation overview, the corresponding users, and the corresponding audit log list of various K8s objects .
### Aggregation search
When you want to view the distribution trend of audit logs in a certain dimension, you can set filter conditions on the "Aggregation Search" page to view the sequence diagrams of various important operations. The dimensions include the user, namespace, operation type, status code, resource type, and the corresponding audit log list .

### Global search
Global search dashboard, with built-in CLS search analysis page, is convenient for users to quickly search all audit logs in the TKE console .