## Feature Overview

 TMP provides the highly available Prometheus service as well as the open-source visualization tool Grafana while inheriting the monitoring capabilities of the open-source Prometheus, which reduce your development and OPS costs.

>?If you have already created a [TKE](https://intl.cloud.tencent.com/zh/document/product/457) cluster, you can create a TMP instance in the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and install the Prometheus monitoring plugin to monitor the cluster. In addition, TMP is integrated with Grafana and predefined dashboards for you to view performance metric data in different dimensions.

## Prerequisites

Create a TKE [cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions

### Step 1. Create a TMP instance[](id:step1)

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. Click **Create** to enter the purchase page and purchase an instance according to your actual needs. For more information, please see Creating Instance.


### Step 2. Integrate TKE[](id:step2)

TMP has been deeply integrated with TKE. You only need to perform quick installation and then you can monitor Kubernetes clusters and services running in them.

1. In the instance list, select the TMP instance to be integrated, click the **instance ID** or **Manage** on the right to enter the TMP instance management page.
2. Click **Integrate TKE**, select the corresponding TKE cluster, and click **Install** for automated integration. In the installation pop-up window, you can select the basic monitoring components that need to be integrated.
![](https://qcloudimg.tencent-cloud.cn/raw/04156f3da77e8ca3866a6601beb5e91d.png)
3. The overall integration operation is async, which takes about 2–3 minutes. When the monitoring status shows "Installed", the installation is successful.
  >?During the integration, you need to grant the permission to manipulate TKE. For detailed directions, please see Description of Role Permissions Related to Service Authorization.



### Step 3. Using the integration center[](id:step3)

To facilitate access, TMP integrates commonly used development languages, middleware, and big data. You only need to follow the instructions to monitor the corresponding components. It also provides out-of-the-box Grafana monitoring dashboards.
![](https://qcloudimg.tencent-cloud.cn/raw/6e15aeacee5a9a4f352fc0726503267e.png)


### Step 4. View monitoring data in Grafana[](id:step4)

TMP offers the out-of-the-box Grafana service. It also integrates a wealth of dashboards for Kubernetes basic monitoring and common service monitoring, which can be quickly used.

1. In the [TMP instance](https://console.cloud.tencent.com/monitor/prometheus) list, find the corresponding TMP instance, click <img src="https://main.qcloudimg.com/raw/978c842f0c093a31df8d5240dd01016d.png" width="2%"> on the right of the instance ID to open your Grafana page, and enter your account and password to access the Grafana visual dashboard operation section.
2. Enter Grafana and click <img src="https://main.qcloudimg.com/raw/7e3fff6131aa085987552a9725e9ae54.png" width="2%"> to expand the monitoring panel.
![](https://main.qcloudimg.com/raw/2821a37a7b766da09c1b6b3f995b32b4.png)
3. Click the name of the corresponding monitoring chart to view the monitoring data.
![](https://main.qcloudimg.com/raw/8d9c88d74a9fc1732145040f6df3954f.png)
>?For more information on how to use Grafana, please see [Getting started](https://grafana.com/docs/grafana/latest/getting-started/).
