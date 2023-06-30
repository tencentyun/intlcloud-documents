<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into [TMP](https://intl.cloud.tencent.com/document/product/457/46734), which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be discontinued on May 16, 2022,see [Announcements](https://intl.cloud.tencent.com/document/product/457/46999). Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. TPS instances can no longer be created, but you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>


## Overview

This document describes how to configure monitoring collection items for the associated cluster.

## Prerequisites

Before configuring monitoring collection items, you need to perform the following operations:
- You've [created a TMP instance](https://intl.cloud.tencent.com/document/product/457/46739).
- The cluster to be monitored has been associated with the corresponding instance as instructed in [Associating with Cluster](https://intl.cloud.tencent.com/document/product/457/38825).

## Directions
### Configuring data collection

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Associate with cluster** page, click **Data collection** on the right of the instance to enter the collection configuration list page.
![](https://qcloudimg.tencent-cloud.cn/raw/2f4a25e860c811521cd699d54210d9e9.png)
4. On the **Data collection** page, add the data collection configuration. The cloud native monitoring has preset some collection configuration files to collect regular monitoring data. You can configure new data collection rules to monitor your business data by using the following two methods:
<dx-tabs>
::: Adding configuration in the console
#### Monitoring service 
1. Click **Add**.
2. In the **Create collection policy** pop-up window, enter the configuration information.
![](https://qcloudimg.tencent-cloud.cn/raw/90d6cb705291ec0507fc02cca712de8e.png)
 - **Monitoring type**: Select **Service monitoring**.
 - **Name**: Enter the rule name.
 - **Namespace**: Select the namespace to which the service belongs.
 - **Service**: Select the service to be monitored.
 - **ServicePort**: Select the corresponding port.
 - **MetricsPath**: Defaults to `/metrics`. You can directly enter the collection API as needed.
 - **View configuration file**: Click **Configuration file** to view the current configuration file. If you have special configuration requirements such as relabel, you can edit them in the configuration file.
 - **Check the target**: Click **Check the target** to view a list of all targets that can be collected under the current collection policy, and confirm whether the collection policy meets your expectations.

#### Monitoring workload
1. Click **Add**.
2. In the **Create collection policy** pop-up window, enter the configuration information.
![](https://qcloudimg.tencent-cloud.cn/raw/c35d3c86973fbd742de817f026a2eab0.png)
 - **Monitoring type**: Select **Workload monitoring**.
 - **Name**: Enter the rule name.
 - **Namespace**: Select the namespace to which the workload belongs.
 - **Workload type**: Select the workload type to be monitored.
 - **Workload**: Select the workload to be monitored.
 - **targetPort**: Enter the target port that exposes the collection metrics through which the collection target can be found. If the port is incorrect, the collection target will not be obtained correctly.
 - **MetricsPath**: Defaults to `/metrics`. You can directly enter the collection API as needed.
 - **View configuration file**: Click **Configuration Ffile** to view the current configuration file. If you have special configuration requirements such as relabel, you can edit them in the configuration file.
 - **Check the target**: Click **Check the target** to view a list of all targets that can be collected under the current collection policy, and confirm whether the collection policy meets your expectations.
:::
::: Adding configuration via yaml
1. Click **Add via YAML**.
2. In the pop-up window, select the monitoring type and enter the relevant configurations. Here takes **Add PodMonitors** as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/a57bc9d2fd7227e88ee1d3a9b9f4ca66.png)
You can refer to the methods in the community to submit the corresponding yaml to complete the data collection configuration.
 - **Workload monitoring**: The corresponding configuration is `PodMonitors`.
 - **Service monitoring**: The corresponding configuration is `ServiceMonitors`.
 - **RawJobs monitoring**: The corresponding configuration is `RawJobs`.
:::
</dx-tabs>
5. Click **OK**.
6. You can view the status of the collection target on the **Data collection** page of the instance.
![](https://qcloudimg.tencent-cloud.cn/raw/6b483f8ea0d4a0538c761b473cedb9a8.png)
 **targets (1/1)** indicates one actually captured target/one checked collection target. When the number of actual captured targets equals to the number of checked targets, the status will be "up", which means that the current capture is normal. When the number of actual captured targets is less than the number of checked targets, the status will be "down", which means that some endpoints capture failed.
Click the field value (1/1) to view the details of the collection target.
![](https://qcloudimg.tencent-cloud.cn/raw/cca8ebe23797442415ff584b618ea6fc.png)
On the **Associate with cluster** tab of the instance, click **More** > **Target Jobs** on the right of the cluster name to view all the collection targets of this cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/c536d75b4257741a85b4a28a3938e927.png)


















### Viewing existing configuration

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, click **View configuration** in the upper-right corner.
3. In the **View configuration** pop-up window, view all monitoring metrics configured in the yaml file.
![](https://qcloudimg.tencent-cloud.cn/raw/e7a536ada035fa06b2661a18e46fe5ba.png)


### Viewing collection targets

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Associate with cluster** tab, click **Target Jobs** on the right of the instance.
4. On the targets list page, view the collection status of current data.
![](https://qcloudimg.tencent-cloud.cn/raw/cca8ebe23797442415ff584b618ea6fc.png)

<dx-alert infotype="explain" title=" ">
<li>The endpoints in the status of "Unhealthy" are displayed at the top of the list by default.</li>
<li>You can filter a target by resource attribute on the collection target page.</li>
</dx-alert>




## Related Operations
### Mounting file to collector
When configuring the collection item, if you need to provide some files for the configuration, such as a certificate, you can mount the file to the collector in the following way, and the update of the file will be synchronized to the collector in real time.

- **prometheus.tke.tencent.cloud.com/scrape-mount = "true"**
  Add the above label to the configmap under the `prom-xxx` namespace, and all the keys will be mounted to the collector path `/etc/prometheus/configmaps/[configmap-name]/`.

- **prometheus.tke.tencent.cloud.com/scrape-mount = "true"**
 Add the above label to the secret under the `prom-xxx` namespace, and all the keys will be mounted to the collector path `/etc/prometheus/secrets/[secret-name]/`.

