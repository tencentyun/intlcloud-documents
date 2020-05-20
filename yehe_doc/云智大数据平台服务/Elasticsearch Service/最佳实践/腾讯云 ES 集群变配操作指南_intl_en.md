
As your business develops, the data volume and access traffic of your ES cluster grow. When the cluster size and configuration become insufficient to satisfy your actual business needs, you can scale out your ES cluster as needed.

The overview of Tencent Cloud ES cluster scaling is as shown above. You can quickly select a scaling method suitable for your current cluster according to the following table:

| Scaling and Configuration Adjustment Type | How It Works | Features |  Use Case
|---------|---------|---------|-----|
| Expanding cluster disk capacity | Perform vertical scaling on disks mounted to nodes in the cluster one by one | The cluster can be smoothly scaled out without interrupting your business, and the scaling is quick (about 30 seconds for each node) |  The computing resources are sufficient but the disk storage capacity is insufficient
| Adding nodes to cluster  |  Add more nodes in the same specification as that of existing nodes to the cluster   |  The cluster can be smoothly scaled out without interrupting your business, and the scaling is quick, which is not affected by the number of nodes and generally takes 5–10 minutes   |  The node specification is high but the overall computing resources of the cluster are insufficient
|  Upgrading node specification  |  Add the same number of new nodes as existing nodes in a higher specification, migrate data in the existing nodes to the new nodes, and then remove the existing nodes  |  The cluster can be smoothly scaled out without interrupting your business. Data needs to be migrated during scaling; therefore, the greater the data volume, the longer the scaling process  |  The node specification is low and the overall computing resources of the cluster are insufficient


The scaling scenarios currently supported by Tencent Cloud ES are detailed as below:

## Disk Capacity Expansion
**Disk capacity expansion:** it refers to increasing the overall storage capacity of the cluster without changing the computing resource configuration of the nodes.

**How it works:** during disk capacity expansion, vertical scaling is performed on disks mounted to each data node in the cluster one by one to increase the overall disk storage capacity of the cluster; for example, the original disk capacity is 1,000 GB, and you can use this scaling method to increase the capacity to 5,000 GB. This method does not require node restart; therefore, the use of the cluster by your business will not be affected. As data nodes are expanded on a rolling basis, the more the nodes in the cluster, the longer the scaling process. If it takes about 30 seconds to expand a node, then it will take about 2 minutes to expand a cluster with 5 data nodes. The process and principle are as shown below:
 ![](https://main.qcloudimg.com/raw/1bde355bce7b7b68ec920c50bc97d7e1.png)
**Use cases:** it is suitable for scenarios where the computing resources are sufficient, but the disk capacity is insufficient; for example, the CPU load and memory utilization of your cluster are relatively low, but the average disk utilization is high, and all data is important, which cannot be deleted to release disk space. In this case, you can scale the cluster by only expanding the disk capacity.

## Node Scaling
Node scaling is suitable for scenarios where the cluster computing resources hit the bottleneck; for example, the CPU load is continuously high, or the memory utilization stays high and repeatedly triggers memory issues or even OOM. In this case, you can scale out the cluster nodes to improve the cluster's overall performance.

### Adding nodes to cluster
**Adding nodes to cluster:** it is a scaling method in which more nodes are added to the cluster without changing the cluster node model configuration. Its process and principle are as shown below:
![](https://main.qcloudimg.com/raw/e955275f114fac35a73e5b97efa56fbc.png)
The major **advantage** of this scaling method is **smoothness**, so that your business will not be interrupted during the scaling. As no data migration between new and existing nodes is involved, the scaling will not be affected by the node quantity and can be completed generally in 5–10 minutes.

**Use cases:** the node configuration is already very high, but you want to further improve the cluster's overall read/write performance, and your business requires high cluster stability during the scaling. In this case, you can scale the cluster by adding nodes to it.

### Upgrading node specification
**Upgrading node specification:** it refers to upgrading the configuration of data nodes or dedicated master nodes in the cluster without changing the number of nodes, such as upgrading the data node configuration from 4-core 16 GB MEM to 8-core 16 GB MEM.

- Data migration
Scaling a cluster through data migration is to first add the same number of new nodes as existing nodes in a higher specification, migrate data in the existing nodes to the new nodes, and then remove the existing nodes. Its process and principle are as shown below:
 ![](https://main.qcloudimg.com/raw/d8056af7acef6c499456a5bae0ee149f.png)
The major **advantage** of this scaling method is **smoothness**, so that the cluster use and availability will not be affected during scaling. However, as the data in existing nodes needs to be migrated to the new nodes, the migration duration is greatly subject to the data volume. Therefore, if the cluster data volume is over 1 TB and you want to complete scaling as soon as possible, you can restart the nodes on a rolling basis or set the following attributes in Kibana to speed up the data migration:
```
PUT _cluster/settings
{
		"persistent": {
			"cluster.routing.allocation.node_concurrent_recoveries": "8",
			"indices.recovery.max_bytes_per_sec": "80mb"
		}
}
```
- The `cluster.routing.allocation.node_concurrent_recoveries` attribute specifies the number of shards concurrently restored on each node in the cluster, which is 2 by default and cannot exceed 50. You can determine the specific value by multiplying the number of CPU cores in an existing data node by 4; for example, you are recommended to set this attribute to 16 if the existing data node specification is 4-core 16 GB MEM or to 50 if the specification is 16-core 64 GB MEM. If you find that the cluster stability is compromised after you increase the attribute value, you can appropriately set a smaller value.
- The `indices.recovery.max_bytes_per_sec` attribute specifies the maximum bandwidth for data transfer between nodes, which is `40mb` by default. The bandwidth limit should not be too high; otherwise, the cluster stability may be compromised. You can adjust the limit by an increment of `5mb` while checking the cluster stability so as to determine an appropriate value.

**Use cases:** the node configuration is relatively low, you want to further improve the cluster's overall read/write performance, your business requires high cluster stability during the scaling, and you have ample time for the scaling. In this case, you can scale the cluster through data migration.

