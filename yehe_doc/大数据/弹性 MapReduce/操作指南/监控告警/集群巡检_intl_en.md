## Feature Overview
Each cluster can perform health checks on its servers and services instantly or regularly (by day or week) according to the selected inspection items. You can configure only one regular inspection task for one cluster so as to stay on top of the cluster health and handle exceptions or risks in time.

When an instant or regular inspection task is configured, general inspection items will be selected by default. In special cases where service features need to be inspected, you can add additional inspection items as needed, but service feature inspections will compromise the cluster performance. You are not recommended to conduct resource-consuming inspections during peak business hours.

An inspection report will be generated in PDF format after each inspection task is completed, which can be downloaded or deleted. Each root account can retain up to 50 inspection reports. If the upper limit is exceeded, older reports will be deleted.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select the target cluster in **Cluster List**, and click **Details** to enter the cluster details page.
2. Select **Cluster Monitoring** > **Cluster Inspection** on the cluster details page to perform health check on the servers and services of the current cluster. Each cluster can only be configured with one regular inspection task. You can also click **Instant Inspection** to perform inspection. To configure regular inspection tasks, click **Regular Inspection Settings**.

 - Instant inspection: it is to check the health status of the servers and services of the cluster from a certain moment to the current time and generate an inspection report.

 - Regular inspection: after the regular inspection policy is enabled, the system will automatically check the health status of the servers and services of the cluster in each inspection cycle and generate inspection reports. Each cluster can be configured with one regular inspection policy.
