## Overview
A healthy monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud Tencent Kubernetes Engine (TKE). You can collect monitoring data of different dimensions for different resources, making it easy to understand every resource’s usage information and locate errors quickly.
Tencent Cloud TKE features collection and display of monitoring data at 5 levels: cluster, node, workload, pod, and container.
The collection of monitoring data allows you to establish normal standards for cluster performance. By testing performance of a container cluster at different times and under different load conditions, you can better understand the normal performance of a container cluster or service. This allows you to quickly determine if the running status is exceptional based on the current monitoring data, and to find solutions promptly. For example, you can monitor a service’s CPU utilization, memory usage, or disk I/O.

## Monitoring
For more information on TKE monitoring, please see [Viewing Monitoring Data](https://intl.cloud.tencent.com/document/product/457/30689).
For more information on the currently supported monitoring metrics, please see [List of Monitoring and Alarm Metrics](https://intl.cloud.tencent.com/document/product/457/30691).

## Alarms
We recommend that you set the necessary alarms on all production clusters in order to detect TKE exceptions promptly and ensure the stability and reliability of your business. For more information on setting alarms, please see [Setting Alarms](https://intl.cloud.tencent.com/document/product/457/30690).
For more information on the currently supported alarm metrics, please see [List of Monitoring and Alarm Metrics](https://intl.cloud.tencent.com/document/product/457/30691).

>TKE monitoring and alarm features primarily cover the core metrics and events of Kubernetes objects. To ensure more fine-grained metric coverage, please use these features in combination with the basic resource monitoring provided by [Cloud Monitoring](https://console.cloud.tencent.com/monitor/overview), (e.g. CVM, Cloud Block Storage, Load Balancer, etc.).
