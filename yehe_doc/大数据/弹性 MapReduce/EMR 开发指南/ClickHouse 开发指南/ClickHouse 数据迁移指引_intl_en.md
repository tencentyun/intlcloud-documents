## Feature Overview
A ClickHouse cluster consists of at least one node and allows you to define one or more virtual clusters through configuration. If the node quantity or storage volume of a virtual cluster changes, you can use the data migration feature to balance data distribution and improve the cluster resource utilization. This feature supports deactivation mode and balancing mode.

## Use Cases
- In balancing mode, each target node will receive an equal amount of data migrated from source nodes, and only partition tables rather than non-partition tables will be migrated. It is suitable for cluster scale-out and node load balancing scenarios.
- In deactivation mode, all data including partition and non-partition tables from source nodes will be migrated to target nodes. It is suitable for node termination and data backup scenarios.

## Directions
Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **ClickHouse Cluster** > **Cluster Service** in the cluster list, and click **Operation** > **Data Migration** in the "ClickHouse" block.
![](https://main.qcloudimg.com/raw/e4d815d3f4d372ac2ab193248ab8c4ae.png)
You can migrate data in the following four steps:
1. **Select Cluster**: select a cluster and the migration mode, which is **balance mode** by default. You can select only one cluster for each migration task.
![](https://main.qcloudimg.com/raw/a52996fb597995e866c52c42b654c69b.png)
2. **Next: Select Nodes**: select the migration nodes and set the maximum data migration bandwidth, which is 200 MB/s by default (recommended) and can be customized. The system will check all nodes in the cluster by default and automatically mark source and target nodes, which can be slightly adjusted on your own. A node can be either a source node or target node, and a cluster must contain at least one source node and one target node.
![](https://main.qcloudimg.com/raw/50122a6d01939d8f5500111ccba48555.png)
3. **Next: Select Data Tables**: select the data tables to be migrated. The system will pull all tables from the source node and sort them in descending order by data volume. 10 tables are displayed per page and checked by default. You can search for tables by their thresholds and whether they contain or do not contain certain conditions.
 
4. **Next: Information Confirmation**: confirm the final migration information.
 
>!
>- Balancing mode: only partition tables will be migrated.
>- Deactivation mode: partition and non-partition tables will be migrated.
