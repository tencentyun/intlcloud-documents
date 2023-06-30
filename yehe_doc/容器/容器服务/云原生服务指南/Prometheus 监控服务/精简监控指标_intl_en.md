
<dx-alert infotype="notice" title="">
TMP will adjust the free storage period for free metrics to 15 days on October 27, 2022. For instances with a storage period of more than 15 days, storage fees for their free metrics will be charged based on the excessive storage period.
</dx-alert>

This document describes how to streamline the TMP **collection metrics** to avoid unnecessary expenses.

## Prerequisites

Before configuring monitoring collection items, you need to perform the following operations:

- You've created a PROM instance. Refer to [Creating PROM instance](https://intl.cloud.tencent.com/document/product/457/46739).
- You’ve [associated the monitored cluster with the corresponding instance](https://intl.cloud.tencent.com/document/product/457/46731).

## Streamlining Metrics

### Streamlining metrics in the console

TMP offers more than 100 free basic monitoring metrics as listed in [Free Metrics in Pay-as-You-Go Mode](https://intl.cloud.tencent.com/document/product/457/46735).

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[TMP](https://console.cloud.tencent.com/tke2/prometheus2)** on the left sidebar.
2. On the instance list page, select an instance name that needs to configure data collection rules to go to its details page.
3. On the **Cluster monitoring** page, click **Data collection** on the right of the cluster to enter the collection configuration list page.
4. You can add or remove targets of basic metrics on the productized page. Click **Metric Details** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/8e837e035089126feca9a827867b2647.png)
5. The following shows whether the metrics are free. If you select a metric, it will be collected. We recommend you deselect paid metrics to avoid additional costs. Only metrics for basic monitoring are free of charge. For more information on free metrics, see [Free Metrics in Pay-as-You-Go Mode](https://intl.cloud.tencent.com/document/product/457/46735). For more information on paid metrics, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156).
![](https://qcloudimg.tencent-cloud.cn/raw/92c68bf0a10368f8c513c85327a66c43.png)

### Streamlining metrics through YAML

Currently, TMP is billed by the number of monitoring data points. We recommend you optimize your collection configuration to collect only required metrics and filter out unnecessary ones. This will save costs and reduce the overall reported data volume. For details of billing and cloud resource usage, see [here](https://intl.cloud.tencent.com/document/product/457/46733).

The following describes how to add filtering configurations to `ServiceMonitor`, `PodMonitor`, and `RawJob` to streamline custom metrics.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **[TMP](https://console.cloud.tencent.com/tke2/prometheus2)** in the left sidebar.
2. On the instance list page, select an instance name that needs to configure data collection rules to go to its details page.
3. On the **Cluster monitoring** page, click **Data collection** on the right of the cluster to enter the collection configuration list page.
4. Click **Edit** on the right of the instance to view the metric details.
    ![](https://qcloudimg.tencent-cloud.cn/raw/086b82da019fd9b39c1efdca7c6524d0.png)
    <dx-tabs>
    ::: `ServiceMonitor` and `PodMonitor`
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
    scrapeTimeout: 15s # It indicates the collection timeout period. TMP configuration requires that this value does not exceed the collection interval, i.e., `scrapeTimeout` <= `interval`.
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
    scrapeTimeout: 15s
    # The following four lines are added:
    metricRelabelings: # Each collected item is subject to the following processing.
    - sourceLabels: ["__name__"] # The name of the label to be detected. `__name__` indicates the name of the metric or any label that comes with the item.
      regex: kube_node_info|kube_node_role # Whether the above label satisfies this regex. Here, `__name__` should satisfy the requirements of `kube_node_info` or `kube_node_role`.
      action:  keep # Keep the item if it meets the above conditions, or drop it otherwise.
  jobLabel: app.kubernetes.io/name
  namespaceSelector: {}
  selector:
```

:::
::: RawJob
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
      action:  keep # Keep the item if it meets the above conditions, or drop it otherwise.
		    
```

:::
</dx-tabs>

5. Click **OK**.


### Blocking collection targets

#### Blocking the monitoring of the entire namespace

TMP will monitor all the `ServiceMonitor` and `PodMonitor` resources in a cluster by default after the cluster is associated. If you want to block the monitoring of a namespace, you can add the label of `tps-skip-monitor: "true"` as instructed in [Labels and Selectors](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/).

#### Blocking certain targets

TMP collects monitoring data by creating CRD resources of `ServiceMonitor` and `PodMonitor` types in your cluster. If you want to block the collection of the specified `ServiceMonitor` and `PodMonitor` resources, you can add the label of `tps-skip-monitor: "true"` to these CRD resources as instructed in [Labels and Selectors](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/).
