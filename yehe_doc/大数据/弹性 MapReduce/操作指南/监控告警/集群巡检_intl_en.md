## Feature Overview

You can perform health check on the nodes and services in each cluster instantly or periodically (daily or weekly) with the selected inspection items. Only one periodic inspection task can be configured for each cluster to help you know the cluster health conditions periodically and fix the exceptions and risks in time.

When you set a one-time or periodic inspection task, general inspection items will be selected by default. If you want to check certain service features in special cases, you can select the corresponding inspection items as needed. However, service feature inspection will compromise cluster performance, which is thus not recommended during business peak hours.

After each inspection task is completed, a PDF report will be generated, which can be downloaded and deleted. Up to 50 inspection reports can be retained under each root account. If an excessive report is generated, the oldest one will be deleted.

>?The inspection system supports service inspection items. Currently, only HDFS, YARN, HBase, Hive, and ZooKeeper are supported.


## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click the **ID/name** of the target cluster in **Cluster List** to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Inspection** and you can perform health check on the nodes and services in the current cluster. Only one periodic inspection task can be configured for each cluster. You can also click **One-Time Inspection** to perform an inspection. To configure a periodic inspection task, click **Periodic Inspection Settings**.
![](https://main.qcloudimg.com/raw/ce7e2d8727ebac8149f3eaf9e45a00e4.png)
 - Instant inspection: checks the health status of the cluster nodes and services from a certain moment till now and generates an inspection report.
![](https://main.qcloudimg.com/raw/75be9ef6b909944665a1b6a08fb780fe.png)
 - Regular inspection: after the regular inspection policy is enabled, the system will automatically check the health status of the cluster nodes and services in each inspection cycle and generate inspection reports. Each cluster can be configured with one regular inspection policy.
![](https://main.qcloudimg.com/raw/15c5e354c2c06f9f858406277da84034.png)
 - Inspection item: all enabled event monitoring policies are supported by default. You can adjust the inspection items as instructed in [Cluster Event](https://intl.cloud.tencent.com/document/product/1026/36889). All events with monitoring enabled are selected by default as the initial inspection items. When you customize the inspection items, those selected last time will be selected by default.
![](https://main.qcloudimg.com/raw/89019ff88ebf26e599e980db50647fa9.png)


