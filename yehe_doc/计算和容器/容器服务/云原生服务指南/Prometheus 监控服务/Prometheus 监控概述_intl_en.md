## Overview 

Tencent Managed Service for Prometheus (TMP) is a monitoring and alarming solution specially optimized for cloud-native service scenarios. It has the full monitoring capabilities of open-source Prometheus and provides lightweight, stable, and highly available cloud-native monitoring services. It eliminates your need to build a Prometheus monitoring system on your own or care about issues such as data storage, data display, and system Ops, and enables you to enjoy a high-performance multi-cluster Prometheus monitoring service after simple configuration.

### Prometheus overview 

Prometheus is an open-source system monitoring and alarming framework. It completely disrupts the testing and alarming models of traditional monitoring systems by forming a new model based on centralized rule computing and unified analysis and alarming. As a project in [Cloud Native Computing Foundation](https://www.cncf.io/) with a popularity only second to Kubernetes, it has gradually become a core monitoring component in the era of cloud native thanks to its powerful standalone performance, flexible PromQL, and active community ecosystem.

#### Strengths of Prometheus

- Support for powerful multidimensional data models.
- Built-in flexible query language PromQL.
- Support for all-around monitoring.
- Great openness.
- Support for target discovery and collection through dynamic service or static configuration.

#### Shortcomings of open-source Prometheus

- The native Prometheus is deployed on a single server and does not provide cluster features, which makes it impossible to monitor large clusters.
- It cannot easily implement dynamic scaling and load balancing.
- It is technically difficult to deploy and get started with.


### Comparison between TMP and open-source Prometheus

| Comparison Item            | TMP                                       | Open-Source Prometheus                     |
| ----------------- | ------------------------------------------------------------ | ----------------------------------- |
| Scenario              | Optimized for container cloud-native scenarios and allows you to use the [Integration Center](https://intl.cloud.tencent.com/document/product/1116/43163) to implement the monitoring of non-container scenarios | Oriented to multiple scenarios                        |
| Weight              | Super lightweight                                                     | High memory usage                          |
| Stability            | Higher than native                                                     | Not guaranteed                            |
| Availability            | High                                                           | Low                                  |
| Data storage capability      | Unlimited                                                       | Subject to local disk capacity                      |
| Monitoring of ultra large cluster      | Supported                                                         | Not supported                              |
| Data visualization   | Excellent visualization capabilities based on Grafana and data display of multiple monitoring instances at the same time on Grafana | Limited visualization capabilities based on native Prometheus UI |
| Open-Source ecosystem          | Full compatibility                                                     | Native support                            |
| Barrier to use          | Low                                                           | High                                  |
| Cost              | Low                                                           | High                                  |
| Cross-cluster collection        | Supported                                                         | Not supported                              |
| Cross-region and cross-VPC collection | Supports cluster data collection of other regions and VPCs as well as [associating with a cluster in TMP](https://intl.cloud.tencent.com/document/product/457/46731) | Not supported                              |
| Alarming policy configuration      | Rich [alarm and notification templates](https://intl.cloud.tencent.com/document/product/457/46732) | Manual configuration needed                |

## Benefits


**Full compatibility with the configurations and core APIs of Prometheus to retain the native features and strengths of Prometheus**
TMP supports custom multidimensional data models.
TMP has the built-in flexible query language PromQL.
TMP supports target discovery and collection through dynamic service or static configuration.
TMP is compatible with core Prometheus APIs.

**Support for monitoring ultra large clusters**
In the performance stress test for a single Prometheus server, when the number of series exceeds 3 million (the length of each label and its value is fixed at 10 characters), the memory usage increases significantly to over 20 GB; therefore, a large-memory server is required for running Prometheus.
TMP can monitor ultra large clusters based on its proprietary sharding technology.

**Support for monitoring cross-VPC clusters in one instance**
One instance can be associated with multiple clusters. Clusters from other VPCs can be monitored.

**Support for template-based management and configuration**
TMP allows you to configure templates for monitoring multiple instances and clusters. Then, you can use a template to quickly implement unified multi-cluster monitoring.

**Ultra lightweight and non-intrusion monitoring**
TMP is lighter than open-source Prometheus, which uses 16–128 GB memory. In contrast, TMP only requires the deployment of a small agent in your cluster, which uses only 20 MB memory to monitor a cluster with 100 nodes. In addition, its memory usage will never exceed 1 GB no matter how large a cluster is.
After you associate your cluster, TMP will automatically deploy the agent in it, so you can start monitoring your businesses without manually installing any add-on. The super lightweight agent has no impact on the businesses and add-ons in your cluster.

**Support for real-time dynamic scaling to meet elastic needs**
TMP uses Tencent Cloud's proprietary sharding and scheduling technologies to implement real-time dynamic scaling of collection tasks, meeting your elastic needs. It also supports load balancing.

**High availability**
TPS uses technical methods to avoid data breakpoints and losses, so as to secure high availability of the monitoring service.

**Low connection costs**
You can write configuration files easily in the TMP console, so you don't need to have an extensive knowledge of Prometheus to use TMP. If you already know how to use Prometheus, TMP also allows you to submit configuration information through a native YAML file, making it easier for you to customize advanced features for personalized monitoring.

For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/1116/43154).


## Product Architecture

TMP is a super lightweight, highly available, and non-intrusion monitoring system.

* It contains only one lightweight agent in your cluster.
* The collector is a TKE Serverless cluster created under your account and doesn't affect your native clusters.
* Monitoring data storage and display are achieved through separate modules.
* Cloud Monitor Grafana is connected to multiple monitoring instances for a unified view.

The product architecture is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/97fe0cd54132aa59c831a7402940d286.png)



TMP can monitor cross-region and cross-VPC clusters, businesses outside clusters in the same VPC, and ultra large clusters. It also supports real-time scaling of the monitoring add-on to secure the high availability of monitoring services.

After you associate a cluster, TMP will add the mainstream collection configuration from the community by default, making it available out of the box without any custom configuration required.

In addition, TMP is preset with common Grafana dashboards and alarm rule templates.

## Directions

Use your Tencent Cloud account to log in to the [TMP console](https://console.cloud.tencent.com/tke2/prometheus2/list?rid=16):

1. Create an instance.
2. Associate a cluster with the newly created instance. At this point, the system will automatically deploy the agent in your cluster and monitoring add-on in your newly created TKE Serverless cluster, so you don't need to install any add-ons.
3. Configure a collection rule. After a cluster is successfully associated, you can flexibly configure the data collection and alarm rules as needed. Then, you can open Grafana to view the monitoring data.

![](https://qcloudimg.tencent-cloud.cn/raw/10dd3ad358735a6098c1ac8b4f86c2bf.png)

#### Key concepts

- **Instance:** An instance corresponds to a complete set of monitoring services and has an independent GUI. It can be associated with multiple clusters in the same VPC to implement unified multi-cluster monitoring.
- **Cluster:** Generally indicates your TKE or TKE Serverless cluster on Tencent Cloud.
- **Cluster association:** Indicates the operation of associating an instance with a cluster.
- **Collection rule:** Indicates a custom monitoring data collection rule.
- **Job:** In Prometheus, a job is a collection task, which defines the public configurations of all monitoring targets in a job. Multiple jobs can form the configuration file of a collection task.
- **Target:** Indicates a data collection target obtained through static configuration or service discovery. For example, when a Pod is monitored, the target will be each container in the Pod.
- **Metric:** It is used to record the monitoring metric data. All metrics are time series data and identified by name. The sample data collected by each metric contains information in at least three dimensions (metric name, time, and metric value).
- **Series:** It is a metric-label pair displayed as a straight line on a dashboard.

## Use Cases

TMP mainly monitors container cloud-native business use cases. In addition to the implementation of mainstream container and Kubernetes monitoring solutions, it also flexibly supports custom monitoring of your businesses, gradually optimizes the preset dashboards in different use cases, and continuously summarizes industry-specific best practices, in order to help you perform multidimensional analysis and personalized display of monitoring data. It is committed to becoming the best monitoring solution in container use cases.


## Pricing

For TMP pricing details, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156).
Currently, when you use the TMP service, [TKE Serverless clusters](https://intl.cloud.tencent.com/document/product/457/34054) and [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) resources will be created under your account and billed in pay-as-you-go mode. For more information on the created resources and pricing, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733).

