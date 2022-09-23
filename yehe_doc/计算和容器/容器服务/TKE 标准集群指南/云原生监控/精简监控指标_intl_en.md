<dx-alert infotype="alarm" title="Note">
To provide better and more powerful product capabilities, TPS will be merged and upgraded into [Tencent Managed Service for Prometheus (TMP)](https://intl.cloud.tencent.com/document/product/457/46734). The new TMP service supports cross-region and cross-VPC monitoring and connecting a unified Grafana dashboard to multiple TMP instances for data display in one place. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For Tencent Cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be deactivated on May 16, 2022. For more information, see [Announcements](https://intl.cloud.tencent.com/document/product/457/46999). Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out the launched TMP service. TPS instances can no longer be created. You can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency first; otherwise, higher costs may be incurred.
</dx-alert>

## Overview

This document describes how to streamline the TPS **collection metrics** to avoid unnecessary expenses after the migration to [TMP](https://intl.cloud.tencent.com/document/product/457/46734).

## Prerequisites

Before configuring monitoring collection items, you need to perform the following operations:

- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2) and created a self-deployed cluster.
- You have [created a TMP instance](https://intl.cloud.tencent.com/document/product/457/38824?lang=zh&pg=#.E5.88.9B.E5.BB.BA.E7.9B.91.E6.8E.A7.E5.AE.9E.E4.BE.8B) in the VPC of the cluster.

## Streamlining Metrics

### Streamlining metrics in the console

TMP offers more than 100 free basic monitoring metrics as listed in [Free Metrics in Pay-as-You-Go Mode](https://intl.cloud.tencent.com/document/product/457/46735).

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** on the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Associate with Cluster** page, click **Data Collection Configuration** on the right of the cluster to enter the collection configuration list page.
4. You can add or remove targets of basic metrics on the productized page. Click **Metric Details** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/8e837e035089126feca9a827867b2647.png)
5. The following shows whether the metrics are free. If you select a metric, it will be collected. We recommend you deselect paid metrics to avoid additional costs after the migration to [TMP](https://intl.cloud.tencent.com/document/product/457/46734). Only metrics for basic monitoring are free of charge. For more information on free metrics, see [Free Metrics in Pay-as-You-Go Mode](https://intl.cloud.tencent.com/document/product/457/46735). For more information on paid metrics, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156).
![](https://qcloudimg.tencent-cloud.cn/raw/92c68bf0a10368f8c513c85327a66c43.png)

### Streamlining metrics through YAML

Currently, TMP is billed by the number of monitoring data points. We recommend you optimize your collection configuration to collect only required metrics and filter out unnecessary ones. This will save costs and reduce the overall reported data volume. For more information on the billing mode and Tencent Cloud resource usage, see [here](https://intl.cloud.tencent.com/document/product/457/46733).

The following describes how to add filters for ServiceMonitors, PodMonitors, and RawJobs to streamline custom metrics.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** on the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Associate with Cluster** page, click **Data Collection Configuration** on the right of the cluster to enter the collection configuration list page.
4. Click **Edit** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/72cc5e6258ee9b7a8f3217ef0216f5ff.png)

#### ServiceMonitor and PodMonitor

A ServiceMonitor and a PodMonitor use the same filtering fields, and this document uses a ServiceMonitor as an example.
Sample for ServiceMonitor:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  labels:
    app.kubernetes.io/name: kube-state-metrics
    app.kubernetes.io/version: 1.9.7
  name: kube-state-metrics
  namespace: kube-system
spec:
  endpoints:
  - bearerTokenSecret:
      key: ""
    interval: 15s # This parameter is the collection frequency. You can increase it to reduce the data storage costs. For example, you can set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    port: http-metrics
    scrapeTimeout: 15s
  jobLabel: app.kubernetes.io/name
  namespaceSelector: {}
  selector:
    matchLabels:
      app.kubernetes.io/name: kube-state-metrics
```

To collect `kube_node_info` and `kube_node_role` metrics, you need to add the `metricRelabelings` field to the Endpoint list of the ServiceMonitor. Note that it is **`metricRelabelings`** but not `relabelings`.
Sample for adding `metricRelabelings`:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  labels:
    app.kubernetes.io/name: kube-state-metrics
    app.kubernetes.io/version: 1.9.7
  name: kube-state-metrics
  namespace: kube-system
spec:
  endpoints:
  - bearerTokenSecret:
      key: ""
    interval: 15s # This parameter is the collection frequency. You can increase it to reduce the data storage costs. For example, you can set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    port: http-metrics
    scrapeTimeout: 15s # This parameter is the collection timeout period. TMP configuration requires that this value not exceed the collection interval, i.e., `scrapeTimeout` <= `interval`.
    # The following four lines are added:
    metricRelabelings: # Each collected item is subject to the following processing.
    - sourceLabels: ["__name__"] # The name of the label to be detected. `__name__` indicates the name of the metric or any label that comes with the item.
      regex: kube_node_info|kube_node_role # Whether the above label satisfies this regex. Here, `__name__` should satisfy the requirements of `kube_node_info` or `kube_node_role`.
      action:  keep # Keep the item if it meets the above conditions; otherwise, drop it.
  jobLabel: app.kubernetes.io/name
  namespaceSelector: {}
  selector:
```

#### RawJob

If Prometheus' RawJob is used, see the following method for metric filtering.
Sample job:

```yaml
scrape_configs:
  - job_name: job1
    scrape_interval: 15s # This parameter is the collection frequency. You can increase it to reduce the data storage costs. For example, you can set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    static_configs:
      - targets:
          - '1.1.1.1'
```

If you only need to collect `kube_node_info` and `kube_node_role` metrics, add the `metric_relabel_configs` field. Note that it is **`metric_relabel_configs`** but not `relabel_configs`.
Sample for adding `metric_relabel_configs`:

```yaml
scrape_configs:
  - job_name: job1
    scrape_interval: 15s # This parameter is the collection frequency. You can increase it to reduce the data storage costs. For example, you can set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    static_configs:
    - targets:
      - '1.1.1.1'
    # The following four lines are added:
    metric_relabel_configs: # Each collected item is subject to the following processing.
    - source_labels: ["__name__"] # The name of the label to be detected. `__name__` indicates the name of the metric or any label that comes with the item.
      regex: kube_node_info|kube_node_role # Whether the above label satisfies this regex. Here, `__name__` should satisfy the requirements of `kube_node_info` or `kube_node_role`.
      action: keep # Keep the item if it meets the above conditions; otherwise, drop it.
		    
```

### Blocking certain targets

#### Blocking the monitoring of the entire namespace

TPS will manage all the ServiceMonitors and PodMonitors in a cluster by default after the cluster is associated. If you want to block the monitoring of a namespace, you can label it with `tps-skip-monitor: "true"` as instructed in [Labels and Selectors](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/).

#### Blocking certain targets

TPS collects monitoring data by creating CRD resources of ServiceMonitor and PodMonitor types in your cluster. If you want to block the collection of the specified ServiceMonitor and PodMonitor resources, you can add the label of `tps-skip-monitor: "true"` to these CRD resources as instructed in [Labels and Selectors](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/).
