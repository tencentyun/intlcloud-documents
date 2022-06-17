
## Overview
EKS provides out-of-the-box audit dashboards and can automatically configure dashboards of audit overview, K8s object operation overview, and aggregated search for the clusters with cluster auditing enabled. With user-defined filters and built-in CLS global search, EKS makes it convenient for you to observe and search for cluster operations, so as to promptly find and locate problems.




## Feature Description

Four dashboards are configured in **Auditing Search**, namely **Audit Overview**, **K8s Object Operation Overview**, **Aggregated Search**, and **Global Search**. Follow the steps below to enter the **Auditing Search** page to use the features:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Enable cluster auditing. For more information, see [Cluster Auditing](https://intl.cloud.tencent.com/document/product/457/46742).
3. On the left sidebar, click **Cluster Ops** > **Auditing Search**.


### Audit overview

If you want to observe the operations of the API server in the entire cluster, you can set filters on the **Audit Overview** page to view the aggregated statistics of the core audit logs and display the data comparison within a period, for example, core audit log statistics, distribution, important operation trends.
You can customize up to ten filters as needed .
You can modify the custom fields of the filters .


You can view more statistics on this page as shown below:
- Core audit log statistics dashboard:
- Distribution dashboard:
- Important operation trend dashboard:






### K8s object operation overview

When you need to troubleshoot issues with K8s objects (such as a certain workload), you can switch to the **K8s Object Operation Overview** tab, where you can set filters to view the operation overview, operators, and audit log lists of various types of K8s objects .

### Aggregated search

If you want to observe the distribution trend of audit logs in a certain dimension, you can set filters on the **Aggregated Search** tab to view the sequence diagrams of important operations, including user, namespace, operation type, status code, resource type, and audit log list.

### Global search

The global search dashboard with built-in CLS search and analysis makes it convenient for you to quickly search all audit logs in the TKE console .

### Configuring alarm by dashboard

You can configure alarms based on the preset dashboards as instructed below, so that alarms will be triggered when the configured conditions are reached:

1. Click **<img src="https://main.qcloudimg.com/raw/77e0007d25c9724e5b2f05ab3ff8f95a.png" width="2.5%">** on the right of the target dashboard and select **Quickly Add Alarm** from the drop-down list .
2. For more information on how to configure alarm policies, see [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/614/39574).

