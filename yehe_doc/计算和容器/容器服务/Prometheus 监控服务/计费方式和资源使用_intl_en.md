Currently, when you use the TMP service, [EKS clusters](https://intl.cloud.tencent.com/document/product/457/34054) and [CLB](https://intl.cloud.tencent.com/document/product/214) resources will be created under your account. These resources and TMP are pay-as-you-go. This document describes resource usage details when you use TMP.

## Resource List

### TMP instance

The capability of **Billable Metric Collection Rate** has been launched for TMP, which helps you estimate the cost of monitoring by instance, cluster, target, and metric.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[TMP](https://console.cloud.tencent.com/tke2/prometheus2)** on the left sidebar.
2. In the TMP instance list, view the **Billable Metric Collection Rate**, which indicates the collection rate of billable metrics of a TMP instance and is estimated based on your reported metric data volume and the collection frequency. This value multiplied by 86400 is the number of monitoring data points per day, and you can calculate the estimated published price as instructed in [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156).
You can also view the **Billable Metric Collection Rate** under different dimensions on various pages such as **Associate with Cluster**, **Data Collection Configuration**, and **Metric Details**.

### EKS cluster

After each TMP instance is created, a pay-as-you-go EKS cluster will be created under your account for data collection. View the resource information on the [elastic cluster list page](https://console.cloud.tencent.com/tke2/ecluster) as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ef6140a1806a72058732a9e408a30881.png)

#### Notes

The name of the EKS cluster is the TMP **instance ID**, and the cluster description states that "For TMP use only. Do not modify or delete".
![](https://qcloudimg.tencent-cloud.cn/raw/a764cec686ca1c0836a15ceb688ee674.png)

#### Billing

The billing mode is **pay-as-you-go**. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055).

The EKS cluster automatically scales according to the monitoring size. The relationship between the monitoring size and the EKS cluster cost is as shown below:

| **Reported Instantaneous Series** | **Estimated EKS Resources Required** | **Published Price/Day** |
| ------------------------------ | ----------------------- | ----------------------- |
| <500,000                           | 1.25 cores, 1.6 GiB           | 0.35 USD                   |
| 1 million                           | 0.5 core, 1.5 GiB*2           | 1.46 USD                   |
| 5 million                          | 1 core, 3 GiB*3               | 2.93 USD                    |
| 20 million                         | 1 core, 6 GiB*5               | 7.98 USD                    |
| 30 million                         | 1 core, 6 GiB*8               | 12.77 USD                    |

Sample EKS cluster costs are as follows:
  The EKS cluster used for a newly initialized TMP instance consumes 1.25 CPU cores and 1.5 GiB memory. The estimated published price per day is 0.0319 x 24 + 0.0132 x 24 = 1.0824 USD.

### CLB

When you use TMP to associate the cluster monitoring container service, a private network CLB instance will be created under your account for network connectivity between the collector and the cluster.

If you associate an edge cluster or another cluster that is not connected, a public network CLB will be created for network connectivity.

To access the Grafana service over the public network, you need to create a public network CLB instance.

These CLB resources will be charged. You can view the resource information of the created public network CLB instances in the [CLB console](https://console.cloud.tencent.com/clb/instance?rid=1).

This resource is pay-as-you-go. For more information, see [Billing for Bill-by-IP Accounts](https://intl.cloud.tencent.com/document/product/214/36998).

## Resource Termination

Currently, you cannot delete resources in their respective consoles. For example, when you terminate TMP instances in the TMP console, all relevant resources will also be terminated. Tencent Cloud does not repossess TMP instances proactively. If you no longer use TMP, you need to delete the instances promptly to avoid additional charges.
