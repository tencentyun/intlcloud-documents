<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into [TMP](https://intl.cloud.tencent.com/document/product/457/46734), which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be discontinued soon. Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. TPS instances can no longer be created, but you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>

## Overview

This document describes how to streamline the TPS **monitoring metrics** to avoid unnecessary expenses after the migration to [TMP](https://intl.cloud.tencent.com/document/product/457/46734).

## Prerequisites

Before configuring monitoring collection items, you need to perform the following operations:

- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2) and created a self-deployed cluster.
- You have [created a TMP instance](https://intl.cloud.tencent.com/document/product/457/46739) in the VPC of the cluster.

## Streamlining Metrics

### Streamlining basic metrics

TMP offers more than 100 free basic monitoring metrics as listed in [Free Metrics in Pay-as-You-Go Mode](https://intl.cloud.tencent.com/document/product/457/46735).

> ? You can streamline **basic monitoring** metrics only but not **custom monitoring** metrics by selecting/unselecting the metrics. To streamline and modify custom metrics, click **Edit** to customize the collection configurations.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Associate with cluster** page, click **Data collection** on the right of the cluster to enter the collection configuration list page.
4. You can add or remove the basic metrics to be collected by selecting/unselecting the metrics. Click **Metric details** on the right.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8e837e035089126feca9a827867b2647.png)
5. The following shows whether the metrics are free. If you select a metric, it will be collected. We recommend you deselect paid metrics to avoid additional costs after the migration to [TMP](https://intl.cloud.tencent.com/document/product/457/46734). For the billing details of paid metrics, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156).
   ![](https://qcloudimg.tencent-cloud.cn/raw/92c68bf0a10368f8c513c85327a66c43.png)

### Streamlining custom metrics

Currently, TMP is billed by the number of monitoring data points. We recommend you optimize your collection configuration to collect only required metrics and filter out unnecessary ones. This will save costs and reduce the overall reported data volume. For details of billing and cloud resource usage, see [here](https://intl.cloud.tencent.com/document/product/457/46733).

The following describes how to add filtering configurations to `ServiceMonitor`, `PodMonitor`, and `RawJob` to streamline custom metrics.
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** in the left sidebar.
2. On the instance list page, select the target instance to enter its details page.
3. On the **Associate with cluster** page, click **Data collection** on the right of the cluster to enter the collection configuration list page.
4. If you don't see **Metric details** on the right of the instance, click **Edit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/72cc5e6258ee9b7a8f3217ef0216f5ff.png)

#### `ServiceMonitor` and `PodMonitor`

`ServiceMonitor` and `PodMonitor` use the same filtering fields, and this document uses `ServiceMonitor` as an example.
Sample for `ServiceMonitor`:

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
    interval: 15s # It indicates the collection frequency. You can increase it to reduce the data storage costs. For example, set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    port: http-metrics
    scrapeTimeout: 15s
  jobLabel: app.kubernetes.io/name
  namespaceSelector: {}
  selector:
    matchLabels:
      app.kubernetes.io/name: kube-state-metrics
```

To collect `kube_node_info` and `kube_node_role` metrics, you need to add the `metricRelabelings` field to the endpoint list of `ServiceMonitor`. Note that it is **`metricRelabelings`** but not `relabelings`.
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
    interval: 15s # It indicates the collection frequency. You can increase it to reduce the data storage costs. For example, set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    port: http-metrics
    scrapeTimeout: 15s # It indicates the collection timeout period. TMP configuration requires that this value does not exceed the collection interval, i.e., `scrapeTimeout` <= `interval`.
    # The following four lines are added:
    metricRelabelings: # Each collected item is subject to the following processing.
    - sourceLabels: ["__name__"] # The name of the label to be detected. `__name__` indicates the name of the metric or any label that comes with the item.
      regex: kube_node_info|kube_node_role # Whether the above label satisfies this regex. Here, `__name__` should satisfy the requirements of `kube_node_info` or `kube_node_role`.
      action:  keep # Keep the item if it meets the above conditions, or drop it otherwise.
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
    scrape_interval: 15s # It indicates the collection frequency. You can increase it to reduce the data storage costs. For example, set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    static_configs:
      - targets:
          - '1.1.1.1'
```

If you only need to collect `kube_node_info` and `kube_node_role` metrics, add the `metric_relabel_configs` field. Note that it is **`metric_relabel_configs`** but not `relabel_configs`.
Sample for adding `metric_relabel_configs`:
```yaml
scrape_configs:
  - job_name: job1
    scrape_interval: 15s # It indicates the collection frequency. You can increase it to reduce the data storage costs. For example, set it to `300s` for less important metrics, which can reduce the amount of monitoring data collected by 20 times.
    static_configs:
    - targets:
      - '1.1.1.1'
    # The following four lines are added:
    metric_relabel_configs: # Each collected item is subject to the following processing.
    - source_labels: ["__name__"] # The name of the label to be detected. `__name__` indicates the name of the metric or any label that comes with the item.
      regex: kube_node_info|kube_node_role # Whether the above label satisfies this regex. Here, `__name__` should satisfy the requirements of `kube_node_info` or `kube_node_role`.
      action: keep # Keep the item if it meets the above conditions, or drop it otherwise.
		    
```

### Blocking collection targets

#### Blocking the monitoring of the entire namespace

TPS will monitor all the `ServiceMonitor` and `PodMonitor` resources in a cluster by default after the cluster is associated. If you want to block the monitoring of a namespace, you can add the label of `tps-skip-monitor: "true"` as instructed in [Labels and Selectors](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/).

#### Blocking certain targets

TPS collects monitoring data by creating CRD resources of `ServiceMonitor` and `PodMonitor` types in your cluster. If you want to block the collection of the specified `ServiceMonitor` and `PodMonitor` resources, you can add the label of `tps-skip-monitor: "true"` to these CRD resources as instructed in [Labels and Selectors](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/).
