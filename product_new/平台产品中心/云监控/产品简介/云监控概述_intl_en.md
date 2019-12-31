Tencent Cloud’s Cloud Monitor (CM) can monitor your Tencent Cloud product resources in real time. It serves as the monitoring and management entry for all cloud products. You can view the most comprehensive and detailed monitoring data on CM. CM monitors cloud products in real time, including [Cloud Virtual Machine](https://intl.cloud.tencent.com/product/cvm), [Cloud Database](https://intl.cloud.tencent.com/product/cdb), and [Cloud Load Balancer](https://intl.cloud.tencent.com/product/clb). It extracts key metrics of cloud products and displays them in monitoring charts and tables. CM provides you with a comprehensive understanding of your resource usage, application performance, and the running status of your cloud products. It also allows you to set custom alarm thresholds and send notifications based on custom rules.

CM provides information in charts and tables to help you understand the running status and performance of your cloud products, while pushing alarm notifications in a timely manner to inform you of business exceptions. This allows you a comprehensive understanding of the resource usage and running status of your cloud products, with no need for extra development efforts. You can obtain relevant monitoring data from the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview), [Cloud Monitoring API](https://intl.cloud.tencent.com/document/api/248), or [TCCLI](https://intl.cloud.tencent.com/document/product/1013).

## Basic Features

You can gain access to the following features in the Cloud Monitor console.

| Module | Capability | Main Features |
| ---------- | ---------------------------- | ------------------------------------------------------------ |
| Monitor Overview | Display overall monitoring information for cloud products | Provide overall information and alarms for cloud products, giving you an overview of monitoring information |
| Dashboard | Provide a custom monitoring dashboard               | Provide flexible and personalized view features that are applicable to multiple monitoring scenarios, such as cross-instance data aggregation, real-time and historical data display, comparison of similar metrics, and chart and table linkage |
| Alarm Management | Manage alarms in a unified manner | Allow users to configure and manage alarms as well as view the alarm history |
| Cloud Product Monitoring | Display monitoring details for cloud products | Allow users to view monitoring details and alarm details of the cloud resources under their accounts |
| Custom Monitoring | Display users’ custom monitoring metrics | Provide more entries in addition to regular monitoring metrics to facilitate the self-reporting of monitoring data |
| Event Monitoring | Display key event information of products and platforms | Provide reporting, query, and alarm functions for event-type data |
| Traffic Monitoring | Display traffic information | Provide the overall outbound bandwidth information of the public network |

## Supported Services

Currently, CM can automatically monitor the following services. Once you start a service, its metric data will automatically be sent to the CM.

>  Currently, monitoring data statistics are collected at a granularity of one minute, five minutes, one hour, and one day. Most products, such as Cloud Virtual Machine (CVM) and Cloud Database, support a monitoring granularity of one minute, meaning data statistics are collected every minute. Some products only support a granularity of five minutes, meaning data statistics are collected every five minutes.
We will gradually provide seconds-level monitoring for certain products. TencentDB for MySQL instances now support free monitoring at a granularity of five seconds. We will inform you via SMS, Tencent Cloud internal message, and email one month before the official billing starts.

[Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213)
[Cloud Block Storage](https://intl.cloud.tencent.com/doc/product/362) (only when mounted on a running CVM)
[Cloud Load Balancer](https://intl.cloud.tencent.com/doc/product/214)
- Cloud Database
  - [TencentDB for MySQL](https://intl.cloud.tencent.com/doc/product/236)
  - [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/240)
  - [TencentDB for Redis](https://intl.cloud.tencent.com/doc/product/239)
  - TencentDB for Memcached
- [Elasticsearch Service](https://intl.cloud.tencent.com/document/product/845)
- [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/215)
  - [NAT Gateway](https://intl.cloud.tencent.com/zh/document/product/1015)
  - Peering Connection
  - Cross-Region Connection via Basic Network
  - VPN Gateway
  - [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037)
  - [Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216)
  - [Elastic Public IP](https://intl.cloud.tencent.com/document/product/215/4958)
  - Anycast Elastic Public IP
- [Direct Connect](https://intl.cloud.tencent.com/doc/product/216)
  - Connection
  - Direct Connect
- Message Service
  - Topic Subscription
  - Queue
- [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436)
- [Cloud File Storage](https://intl.cloud.tencent.com/document/product/582)
- Oceanus
- BM
  - Cloud Physical Machine (CPM)
  - BM NAT Gateway
  - BM Elastic Public IP
  - BM Load Balancer
  - BM IPsec VPN Tunnel
  - BM IPsec VPN Gateway
  - BM SSL VPN Gateway

## Architecture

CM provides basic metric monitoring and data storage for users. You can view the metric data of your products in the console or pull metric data from APIs. If the basic metric monitoring function provided by CM cannot meet your needs, you can use [Custom cloud monitoring](https://intl.cloud.tencent.com/doc/product/397) to report metric data and view relevant data charts and tables in the Cloud Monitor console.

CM stores metric data for all cloud resources. The metric data of all other cloud products (such as CVM) is stored in the repository for your retrieval. In addition, the raw data stored for cloud products is used to collect metric statistics, which are then presented in graphs in the Cloud Monitor console.

**Architecture Diagram**
![](https://main.qcloudimg.com/raw/3295e8492d0691ca32ea5e4399c5f8df.png)
