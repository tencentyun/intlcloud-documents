## Overview

Tencent Prometheus Service (TPS) is a monitoring and alarming solution specially optimized for cloud native service scenarios. It has the full monitoring capabilities of open-source Prometheus and provides a lightweight, stable, and high-availability cloud native monitoring service. It eliminates your need to build a Prometheus monitoring system on your own or care about issues such as data storage, data display, and system OPS, and enables you to enjoy a high-performance multi-cluster cloud native monitoring service after simple configuration.

### Overview of Prometheus

Prometheus is an open-source system monitoring and alarming framework. It completely disrupts the testing and alarming models of traditional monitoring systems by forming a new model based on centralized rule computing and unified analysis and alarming. As a project in [Cloud Native Computing Foundation](https://www.cncf.io/) with a popularity only second to Kubernetes, it has gradually become a core monitoring component in the era of cloud native thanks to its powerful standalone performance, flexible PromQL, and active community ecosystem.

#### Strengths of Prometheus

- Support for powerful multidimensional data models.
- Built-in flexible query language PromQL.
- Support for all-around monitoring.
- Great openness.
- Support for target discovery and collection through dynamic service or static configuration.

#### Shortcomings of open-source Prometheus

- Native (open-source) Prometheus is deployed on a single server and does not provide cluster features, which makes it impossible to use Prometheus to monitor large clusters.
- It cannot easily implement dynamic scaling and load balancing.
- It is technically difficult to deploy and get started with.


### Comparison between TPS and open-source Prometheus

| Comparison Item       | TPS                        | Open-Source Prometheus                     |
| ------------ | --------------------------------- | ----------------------------------- |
| Scenario         | Optimized for container cloud native scenarios            | Oriented to multiple scenarios                        |
| Weight         | Super lightweight                          | High memory usage                          |
| Stability       | Higher than native                          | Not guaranteed                            |
| Availability       | High                                | Low                                  |
| Data storage capability | Unlimited                            | Subject to local disk capacity                      |
| Monitoring of ultra large cluster | Supported                              | Not supported                              |
| Data visualization   | Excellent visualization capabilities based on Grafana | Limited visualization capabilities based on native Prometheus UI |
| Open-Source ecosystem     | Full compatibility                          | Native support                            |
| Barrier to use     | Low                                | High                                  |
| Cost         | Low                                | High                                  |

## Strengths


**Full compatibility with the configurations and core APIs of Prometheus to retain the native features and strengths of Prometheus**
TPS supports custom multidimensional data models.
TPS has the built-in flexible query language PromQL.
TPS supports target discovery and collection through dynamic service or static configuration.
TPS is compatible with core Prometheus APIs.

**Support for monitoring ultra large clusters**
In the performance stress test for a single Prometheus server, when the number of series exceeds 3 million (the length of each label and its value is fixed at 10 characters), the memory usage increases significantly to over 20 GB; therefore, a large-memory server is required for running Prometheus.
TPS can monitor ultra large clusters based on its proprietary sharding technology and unlimited data storage provided by COS.

**Support for monitoring multiple clusters in one instance**
One TPS instance can be associated with multiple clusters.

**Support for template-based management and configuration**
TPS allows you to configure templates for monitoring multiple instances and clusters. Then, you can use a template to quickly implement unified multi-cluster monitoring.

**Ultra lightweight and non-intrusion monitoring**
TPS is lighter than open-source Prometheus. Prometheus uses 16–128 GB memory. In contrast, TPS only requires the deployment of a small agent in your cluster, which uses only 20 MB memory to monitor a cluster with 100 nodes; plus, its memory usage will never exceed 1 GB no matter how large the cluster is.
After you associate your cluster, TPS will automatically deploy the agent in it, so you can start monitoring your businesses without manually installing any component. The ultra lightweight agent has no impact on the businesses and components in your cluster.

**Support for real-time dynamic scaling to meet elastic needs**
TPS uses Tencent Cloud's proprietary sharding and scheduling technologies to implement real-time dynamic scaling of collection tasks, meeting your elastic needs. It also supports CLB for better load balancing.

**High availability**
TPS uses technical methods to avoid data breakpoints and losses, so as to secure high availability of the monitoring service.

**Low connection costs**
You can write configuration files easily in the TPS console, so you don't need to have an extensive knowledge of Prometheus to use TPS. If you already know how to use Prometheus, TPS also allows you to submit configuration information through a native YAML file, making it easier for you to customize advanced features for personalized monitoring.






## Product Architecture

As an ultra lightweight, high-availability, and non-intrusion monitoring system, TPS only places a small agent in your cluster. Specifically, the agent in your VPC performs operations such as data collection, remote storage, and query, Grafana visually displays data, and AlertManager is used for alarms. The product architecture is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/601d86521b2a5f71d9a0b6859dfc8541.png)


TPS can monitor multiple clusters, businesses outside clusters in the same VPC, and ultra large clusters. It also supports real-time scaling of the monitoring component to secure high availability of the monitoring service.

After you associate a cluster, TPS will add the mainstream collection configuration from the community by default, making it available out of the box without any custom configuration required.

In addition, each TPS instance has a built-in independent Grafana account, which provides a rich variety of preset dashboards and highly customizable monitoring capabilities. In this way, you can implement business-based custom monitoring without caring about the management and scheduling of basic monitoring resources and bottlenecks in the monitoring performance, and enjoy the best monitoring service at the minimum costs.

## Directions

Log in to your Tencent Cloud account, go to the [TPS console](https://console.cloud.tencent.com/tke2/prometheus/list?rid=8), authorize COS as prompted, and use TPS as follows:
1. Create a TPS instance. For more information, see [TPS Instance Management](https://intl.cloud.tencent.com/document/product/457/38824).
2. Associate a cluster with the newly created TPS instance. At this point, the system will automatically deploy the agent in your cluster and deploy the monitoring component in your VPC, so you don't need to install any plugins. For more information, see [Associating Cluster](https://intl.cloud.tencent.com/document/product/457/38825).
3. Configure a collection rule. After a cluster is successfully associated, you can flexibly configure the data collection and alarm rules as needed. Then, you can open Grafana to view the monitoring data. For more information, see [Configuring Collection Rule](https://intl.cloud.tencent.com/document/product/457/38826) and [Alarm Configuration](https://intl.cloud.tencent.com/document/product/457/38828).

![](https://qcloudimg.tencent-cloud.cn/raw/ae4061d92ddf45da9ad72ef5e7a4767e.png)

#### Key concepts

- **TPS instance**: a TPS instance corresponds to a complete set of monitoring services and has an independent GUI. One instance can be associated with multiple clusters in the same VPC to implement unified multi-cluster monitoring.
- **Cluster:** it generally refers to your TKE or EKS cluster in Tencent Cloud.
- **Cluster association**: it refers to the operation of associating a TPS instance with a cluster.
- **Collection rule:** it refers to a custom monitoring data collection rule.
- **Job:** in Prometheus, a job is a collection task, which defines the public configurations of all monitoring targets in a job workload. Multiple jobs can form the configuration file of a collection task.
- **Target:** it refers to a data collection target obtained through static configuration or service discovery. For example, when a Pod is monitored, the target will be each container in the Pod.
- **Metric:** it is used to record the monitoring metric data. All metrics are time series data and identified by metric name. The sample data collected by each metric contains information in at least three dimensions (metric name, time, and metric value).
- **Series:** it is a metric-label pair and represented as a straight line on a dashboard.

## Use Cases

TPS mainly monitors container cloud native business scenarios. In addition to the implementation of mainstream container and Kubernetes monitoring solutions, it also flexibly supports custom monitoring of your businesses, gradually optimizes the preset dashboards in different scenarios, and continuously summarizes industry-specific best practices, in order to help you perform multidimensional analysis and personalized display of monitoring data. It is committed to becoming the best monitoring solution in container scenarios.


## Pricing

Currently, TPS is in beta test and free of charge. You only need to pay small storage fees to enjoy the high-quality TPS service. To try it out, go to the [TPS console](https://console.cloud.tencent.com/tke2/prometheus/list?rid=8).



## Related Services

TPS is responsible for container cloud native monitoring. If you want to use Prometheus to monitor other non-container scenarios, use Managed Service for Prometheus (TMP).
