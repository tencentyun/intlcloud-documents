ES is a cloud-based PaaS service developed based on open-source Elasticsearch. It enables you to quickly build an Elasticsearch cluster service to develop applications such as log analysis and data search. The following describes its capabilities and use limits.

## Product Composition
ES consists of ES cluster, its core component, and Kibana, its visual data analysis tool. For data collection and transfer to the ES cluster, you can deploy data collection tools such as Beats and Logstash or develop custom applications based on your own business needs.

## Available Configurations

**Node specification**

| Parameter Name | CPU Cores | Memory |
|---------|---------|---------|
| ES.S1.SMALL2 | 1 | 2 GB|
| ES.S1.MEDIUM4 | 2 | 4 GB |
| ES.S1.MEDIUM8 | 2 | 8 GB |
| ES.S1.LARGE16 | 4 | 16 GB |
| ES.S1.2XLARGE32 | 8 | 32 GB |
| ES.S1.4XLARGE32 | 16 | 32 GB |
| ES.S1.4XLARGE64 | 16 | 64 GB |

The node with 1 core and 2 GB of memory is intended for testing purpose only and is not recommended for production environments.

**Storage** 
SSD cloud disks are used. The disk capacity is 100 GB–6 TB on a single node.

**Number of nodes** 
The number of nodes is limited to 2–50. As an ES cluster typically consists of nodes deployed in a distributed manner, a master node is required to manage it. In order to prevent the risk of split brain caused by possible node failures, you are recommended to select at least three nodes for a cluster.

**Configuration selection** 
See [Evaluation of Cluster Specification and Capacity Configuration](https://intl.cloud.tencent.com/document/product/845/19551).

## Network Access

**Private network access in VPC** 
In order to ensure data security, ES is built in your VPC, and you can only access an ES cluster from your VPC to write and query data. If you need to access a cluster over the public network for development and debugging purposes, you can connect your local IDC to the VPC using [VPN Connections](https://intl.cloud.tencent.com/document/product/1037). In this case, please take effective measures to protect your data.

**Kibana page** 
You can access the Kibana page over the public network. For the sake of data security, a password and access IP blocklist/allowlist need to be set for the Kibana page.

**VPC network selection**
Once an ES cluster is created, its VPC network cannot be changed; therefore, please make a good plan for your business deployment in advance when creating a cluster.
