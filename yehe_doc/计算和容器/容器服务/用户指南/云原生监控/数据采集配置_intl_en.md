

## Overview

This document describes how to configure monitoring collection items for the associated cluster.

## Prerequisites

Before configuring monitoring collection items, you need to perform the following operations:
- You've created a PROM instance. Refer to [Creating PROM instance](https://intl.cloud.tencent.com/document/product/457/38824).
- The cluster to be monitored has been associated with the corresponding instance. For more information, see [Associating with cluster](https://intl.cloud.tencent.com/document/product/457/38825).

## Directions
### Configuring data collection

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, select an instance name that needs to configure data collection rules to go to its details page.
3. Select **Associate with Cluster** tab and click **Data Collection** on the right side of the instance to go to the data collection page as shown in the figure below:
![](https://main.qcloudimg.com/raw/be1a5a37633e62b5972b9c0560c74a07.png)
4. In the **Data Collection** page, add the data collection configuration. The cloud native monitoring has preset some collection configuration files to collect regular monitoring data. You can configure new data collection rules to monitor your business data by using the following two methods:
<dx-tabs>
::: Adding data collection configuration via the console
#### Monitoring a service 
1. Click **Add**.
2. In the pop-up window, enter the configuration information, as shown below:
![](https://main.qcloudimg.com/raw/fd9ac24b78d0c48089877e20770a2113.png)
 - **Monitoring Type**: select **Service Monitoring**.
 - **Name**: enter the rule name.
 - **Namespace**: select the namespace to which the Service belongs.
 - **Service**: select the service to be monitored.
 - **ServicePort**: select the corresponding port.
 - **MetricsPath**: defaults to `/metrics`. You can directly enter the collection API as needed.
 - **View Configuration File**: click **Configuration File** to view the current configuration file. If you have special configuration requirements such as relabel, you can edit it in the configuration file.
 - **Detect Collection Target**: click **Detect Collection Target** to display a list of all targets that can be collected under the current collection configuration, and confirm whether the collection configuration meets your expectations.

#### Monitoring a workload
1. Click **Add**.
2. In the pop-up window, enter the configuration information, as shown below:
![](https://main.qcloudimg.com/raw/2c3c159a7ec08d9f2e5142ecb3644d02.png)
 - **Monitoring Type**: select **Workload Monitoring**.
 - **Name**: enter the rule name.
 - **Namespace**: select the namespace to which the workload belongs.
 - **Workload Type**: select the workload type to be monitored.
 - **Workload**: select the workload to be monitored.
 - **targetPort**: enter the target port that exposes the collection metrics through which the collection target can be found. If the port is incorrect, the collection target will not be obtained correctly.
 - **MetricsPath**: defaults to `/metrics`. You can directly enter the collection API as needed.
 - **View Configuration File**: click **Configuration File** to view the current configuration file. If you have special configuration requirements such as relabel, you can edit it in the configuration file.
 - **Detect Collection Target**: click **Detect Collection Target** to display a list of all targets that can be collected under the current collection configuration, and confirm whether the collection configuration meets your expectations.
:::
::: Adding data collection configuration via yaml
1. Click **Add via YAML**.
2. In the pop-up window, select the monitoring type, and enter the relevant configurations. Here takes “Add PodMonitors” as an example, as shown below:
![](https://main.qcloudimg.com/raw/fb9be2c21232236b335e929395b2420a.png)
You can refer to the use methods in the community to submit the corresponding yaml to complete the data collection configuration.
 - **Workload Monitoring**: the corresponding configuration is PodMonitors.
 - **Service Monitoring**: the corresponding configuration is ServiceMonitors.
 - **RawJobs Monitoring**: the corresponding configuration is RawJobs.
:::
</dx-tabs>
5. Click **Confirm** to complete the configuration.
6. You can view the status of the collection target in the **Data Collection** page of the instance, as shown below:
![](https://main.qcloudimg.com/raw/9d8500c8e6d2fd45b74d13d6a89a3042.png)
 **targets (1/1)** indicates that one actually captured target / one detected collection target. When the number of actual captured targets equals to the number of detected targets, the status will be “up”, which means that the current capture is normal. When the number of actual captured targets is less than the number of detected targets, the status will be “down”, which means that some endpoints capture failed.
Click the field value (1/1) to view the details information of the collection target, as shown below:
![](https://main.qcloudimg.com/raw/8055782efb0d40b21a10180763468e89.png)
In the **Associate with Cluster** tab of the instance, you can click **More** > **Target Jobs** on the right side of the cluster name to view all the collection targets of this cluster, as shown below:
![](https://main.qcloudimg.com/raw/274667582cce5182cb4f19629776157a.png)


















### Viewing configuration

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, click an instance name to enter its details page. Select **Associate with Cluster** tab and click **Data Collection** > **View Configuration** on the upper-right corner as shown in the figure below:
![](https://main.qcloudimg.com/raw/02be57a84e4dcdd82e0c801cabee9d59.png)
3. In the pop-up **View Configuration** window, view all monitoring objects configured in the yaml file as shown in the figure below:
![](https://main.qcloudimg.com/raw/8261049f27e8c6c69ffd188025ac2e2c.png)


### Viewing collection targets

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native Monitoring** in the left sidebar.
2. On the instance list page, select an instance name that needs to view Targets and go to its details page.
3. Select **Associate with Cluster** tab and click **Target Jobs** on the right side of the instance.
4. In the Targets list, view the collection status of current data as shown in the figure below:
![](https://main.qcloudimg.com/raw/e1a6d0a56e777c6e6ea6387a741e5144.png)

<dx-alert infotype="explain" title="">
<li>The endpoints in the status of “Unhealthy” will be displayed at the top of the list by default.</li>
<li>You can search the target by the resource attributes in the collection target page.</li>
</dx-alert>




## Relevant Operations
### Mounting the file to the collector
When configuring the collection item, if you need to provide some files for the configuration, such as a certificate, you can mount the file to the collector in the following way, and the update of the file will be synchronized to the collector in real time.

- **prometheus.tke.tencent.cloud.com/scrape-mount = "true"**
  Add the above label to the configmap under the prom-xxx namespace, and all the keys will be mounted to the collector path `/etc/prometheus/configmaps/[configmap-name]/`.

- **prometheus.tke.tencent.cloud.com/scrape-mount = "true"**
 Add the above label to the secret under the prom-xxx namespace, and all the keys will be mounted to the collector path `/etc/prometheus/secrets/[secret-name]/`.

