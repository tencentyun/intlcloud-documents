## Feature Overview

 TMP provides the highly available Prometheus service as well as the open-source visualization tool Grafana while inheriting the monitoring capabilities of the open-source Prometheus, which reduce your development and Ops costs.

>?If you have already created a [TKE](https://www.tencentcloud.com/document/product/457) cluster, you can create a TMP instance in the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and install the Prometheus monitoring plugin to monitor the cluster. In addition, TMP is integrated with Grafana and predefined dashboards for you to view performance metric data in different dimensions.

## Prerequisites

Create a TKE [cluster](https://intl.cloud.tencent.com/document/product/457/30637).



### Step 1. Create a TMP instance[](id:step1)

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. Click **Create** to enter the purchase page and purchase an instance as needed. For more information, see [Creating Instance](https://intl.cloud.tencent.com/document/product/1116/43170).

### Step 2. Integrate with TKE

1. In the TMP instance list, click the **ID/Name** of the newly created instance.
2. Go to the TMP management center and click **Integrate with TKE** on the left sidebar.
3. Perform the following operations on the cluster monitoring page.
 - Associate a cluster: Associate a cluster with a TMP instance as instructed in [Associating with Cluster](https://intl.cloud.tencent.com/document/product/457/46731).
 - Configure data collection: Configure a data collection rule to monitor your business data by adding the configuration in the console or via a YAML file.
 - Streamline basic monitoring metrics: Select only the required metrics to avoid unnecessary fees as instructed in [Streamlining Monitoring Metrics](https://intl.cloud.tencent.com/document/product/457/47004).


### Step 3. Integrating a service[](id:step3)

To facilitate access, TMP integrates commonly used development languages, middleware, and big data. You only need to follow the instructions to monitor the corresponding components. It also provides out-of-the-box Grafana monitoring dashboards.
![](https://qcloudimg.tencent-cloud.cn/raw/031b569dc51470630014a9798269a830.png)

### Step 4. View monitoring data in Grafana[](id:step4)

TMP offers the out-of-the-box Grafana service. It also integrates a wealth of dashboards for Kubernetes basic monitoring and common service monitoring, which can be quickly used.

1. In the [TMP instance](https://console.cloud.tencent.com/monitor/prometheus) list, find the corresponding TMP instance, click <img src="https://main.qcloudimg.com/raw/978c842f0c093a31df8d5240dd01016d.png" width="2%"> on the right of the instance ID to open your Grafana page, and enter your account and password to access the Grafana visual dashboard operation section.
2. Enter Grafana and click <img src="https://main.qcloudimg.com/raw/7e3fff6131aa085987552a9725e9ae54.png" width="2%"> to expand the monitoring panel.
   ![](https://main.qcloudimg.com/raw/2821a37a7b766da09c1b6b3f995b32b4.png)
3. Click the name of the corresponding monitoring chart to view the monitoring data.
   ![](https://main.qcloudimg.com/raw/8d9c88d74a9fc1732145040f6df3954f.png)

>?For more information on how to use Grafana, see [Get started](https://grafana.com/docs/grafana/latest/getting-started/).



