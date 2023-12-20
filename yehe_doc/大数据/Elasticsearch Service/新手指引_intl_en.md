This document describes how to get started with Elasticsearch Service (ES).

## 1. Basic knowledge of ES
- [Why ES?](https://intl.cloud.tencent.com/document/product/845/16479)
- [What features does ES have?](https://intl.cloud.tencent.com/document/product/845/16780)
- [Performance of ES](https://intl.cloud.tencent.com/document/product/845/40975)
- [Use cases of ES](https://intl.cloud.tencent.com/document/product/845/16480)
- [Elastic Stack (X-Pack)](https://intl.cloud.tencent.com/document/product/845/30943)
- [Capabilities and restrictions of ES](https://intl.cloud.tencent.com/document/product/845/16481)

## 2. ES billing mode
ES is pay-as-you-go. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/845/18379).


## 3. Getting started
**3.1. Evaluation of cluster specification and capacity configuration**
Before purchasing a cluster, you need to evaluate your specific business according to the actual situation to ensure that the created cluster meets your actual needs. For more information, please see [Evaluation of Cluster Specification and Capacity Configuration](https://intl.cloud.tencent.com/document/product/845/19551).
**3.2. ES cluster purchase**
Before using ES, you need to sign up for a Tencent Cloud account first and then click **Buy Now** on the [purchase page](https://intl.cloud.tencent.com/product/es) to create a cluster. For more information, please see [Creating Clusters](https://intl.cloud.tencent.com/document/product/845/19536).
**3.3. Cluster access**
After successfully creating a cluster, you can start to access it through the [API](https://intl.cloud.tencent.com/document/product/845/19540), [client](https://intl.cloud.tencent.com/document/product/845/19538), or [Kibana](https://intl.cloud.tencent.com/document/product/845/19541). Enabling [ES cluster user authentication](https://intl.cloud.tencent.com/document/product/845/35275) can improve the security of cluster access.


## 4. Overview of console features

| If you want to | 	You can read |
|---------|---------|
| View cluster status information in the cluster list | [Cluster Status](https://intl.cloud.tencent.com/document/product/845/16996) |
| Restart a cluster as needed | [Restarting Clusters](https://intl.cloud.tencent.com/document/product/845/32597) |
| Terminate a cluster | [Terminating Clusters](https://intl.cloud.tencent.com/document/product/845/30949) |
| Create a cluster that supports multi-AZ | [Multi-AZ Cluster Deployment](https://intl.cloud.tencent.com/document/product/845/32591) |
| Understand the concepts and principles of cluster configuration adjustment and scale a cluster | [Adjusting Configuration](https://intl.cloud.tencent.com/document/product/845/30944) and [Suggestions and Principles for Cluster Specification Adjustment](https://intl.cloud.tencent.com/document/product/845/35713) |
| Configure synonyms and YML in a cluster | [Synonym Configuration](https://intl.cloud.tencent.com/document/product/845/36418) and [YML File Configurations](https://intl.cloud.tencent.com/document/product/845/37438) |
| Configure plugins in a cluster | [Plugin List](https://intl.cloud.tencent.com/document/product/845/37440), [IK Analysis Plugin](https://intl.cloud.tencent.com/document/product/845/37441), and [QQ Analysis Plugin](https://intl.cloud.tencent.com/document/product/845/36776) |
| Monitor the status of a running cluster | [Viewing Monitors](https://intl.cloud.tencent.com/document/product/845/30947), [Configuring Alarms](https://intl.cloud.tencent.com/document/product/845/30948), and [Suggestions for Configuring Monitors and Alarms](https://intl.cloud.tencent.com/document/product/845/32608) |
| Query cluster logs | [Querying Cluster Logs](https://intl.cloud.tencent.com/document/product/845/30950) |
| Back up data | [Automatic Snapshot Backup](https://intl.cloud.tencent.com/document/product/845/32587) and [Using COS for Backup and Restoration](https://intl.cloud.tencent.com/document/product/845/19549) |
| Upgrade a cluster and use advanced features | [Upgrading ES Clusters](https://intl.cloud.tencent.com/document/product/845/32600) and [ES Version Upgrade Check](https://intl.cloud.tencent.com/document/product/845/32599) |


## 5. Best practice
### 5.1. Data migration and sync
**1. Data migration**
If you want to migrate your data to ES, you can choose a suitable migration solution based on your business needs, such as COS snapshot, Logstash, and elasticsearch-dump. For more information, please see [Data Migration](https://intl.cloud.tencent.com/document/product/845/32614).
**2. Data ingestion into ES**
You can connect your data source of different types to ES through the Logstash and Beats components. For more information, please see [Data Ingestion into ES](https://intl.cloud.tencent.com/document/product/845/17343).
**3. Real-time MySQL data sync to ES**
You can sync data to ES in real time by syncing MySQL binlog. For more information, please see [Syncing MySQL Data to ES in Real Time](https://intl.cloud.tencent.com/document/product/845/32576).

### 5.2. Use case construction
**1. Build a log analysis system**
You can import your logs into ES and access Kibana from a browser to perform query and analysis (for example, through the most typical log analysis architectures Filebeat + Elasticsearch + Kibana and Logstash + Elasticsearch + Kibana). For more information, please see [Building a Log Analysis System](https://intl.cloud.tencent.com/document/product/845/32590).

### 5.3. Index settings
**1. Default index template description and adjustment**
You can describe and adjust the default template. For more information, please see [Default Index Template Description and Adjustment](https://intl.cloud.tencent.com/document/product/845/32607).
**2. Index management with Curator**
By managing indexes with Curator, you can clear indexes created 7 days ago, back up specified indexes regularly every day, and migrate indexes from a hot node to a warm node regularly. For more information, please see [Managing Indexes with Curator](https://intl.cloud.tencent.com/document/product/845/32613).
**3. Hot/Warm architecture and index lifecycle management**
You can specify the specifications of hot and warm nodes based on your business needs to quickly build an ES cluster in the hot/warm architecture. For more information, please see [Hot/Warm Architecture and Index Lifecycle Management](https://intl.cloud.tencent.com/document/product/845/34890).

### 5.4. SQL support
ES supports SQL instead of DSL as the query language. For those engaged in product operations and data analysis and new ES users, using SQL for queries can reduce their learning costs for getting started with ES. For more information, please see [SQL Support](https://intl.cloud.tencent.com/document/product/845/32574).


## 6. FAQs for beginners
### 6.1. Product
- [What business scenarios is ES suitable for?](https://intl.cloud.tencent.com/document/product/845/16599)
- [I have an unpaid switch order. Will the order still be valid if I upgrade the cluster configuration?](https://intl.cloud.tencent.com/document/product/845/16599)
- [Can I change the cloud disk type after a successful purchase?](https://intl.cloud.tencent.com/document/product/845/16599)

### 6.2 Cluster exceptions 
- [Exceptional Cluster Health Status (Red and Yellow)](https://intl.cloud.tencent.com/document/product/845/40983)
- [Memory Cleanup Methods](https://intl.cloud.tencent.com/document/product/845/40982)
- [Bulk Rejection/Search Rejection](https://intl.cloud.tencent.com/document/product/845/40981)
- [High Cluster CPU Utilization](https://intl.cloud.tencent.com/document/product/845/40980)
- [High Cluster Disk Utilization and read_only Status](https://intl.cloud.tencent.com/document/product/845/40979)
- [Uneven Cluster Load](https://intl.cloud.tencent.com/document/product/845/40978)


## 7. Feedback and suggestions
If you have any questions or suggestions about ES, you can send your feedback through the following channels, and we will get back to you accordingly:
- If you find issues with product documentation, such as links, contents, and APIs, you can click **Send Feedback** on the right of the document page and select the specific issues.
- If you encounter problems when using the product, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
