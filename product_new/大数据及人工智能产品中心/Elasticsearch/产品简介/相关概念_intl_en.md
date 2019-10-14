An Elasticsearch cluster is generally a distributed one consisting of multiple nodes. The nodes communicate and cooperate with one another to provide searching and indexing services (client requests can be forwarded to the optimal node among all the nodes). Different nodes play one or more different roles. There are many node roles in Elasticsearch, and the most important two ones are data nodes and master nodes.

### **Data Node**
It is mainly responsible for operations related to the storing, processing, and manipulating of data and index shards, such as I/O-, memory-, and CPU-intensive operations like CRUD, search, and aggregation. During the use of cluster, you should closely monitor the resource utilization of the data nodes and ensure cluster stability by adding more nodes to scale the cluster up when the service is overloaded.

### **Master Node**
It is responsible for making cluster-wide operations lightweight, such as creating or deleting indices, tracking which nodes are part of which clusters, and deciding which shards to assign to which nodes. It is important to have a stable master node for the cluster health.

### **Master-eligible Node**
This refers to a node that is eligible to be selected as a master node. Any node that meets the requirements for a master node (all nodes by default) can be selected as a master node through the master selection process.

By default, all nodes are data nodes and eligible to be a master node, which is very convenient for small clusters. Because the requests for index processing and data searching are I/O-, memory-, and CPU-intensive for data nodes, they may cause pressure on the node resources. As the cluster grows, in order to ensure that the master nodes are stable and free from pressure and to ensure the cluster stability, the master nodes should be separated from the data nodes.

### **Dedicated Master Node** 
This is a node set to serve only as a master node in an Elasticsearch cluster.

#### **Suggestions on Dedicated Master Nodes**
Configuring dedicated master nodes is mainly to ensure the stability of the cluster as it grows. It is recommended to configure at least 3 dedicated master nodes:
- If the number of dedicated master nodes is 1, there is only one eligible master node. discovery.zen.minimum_master_nodes can only be set to 1, and there is no backup in case of network failure.
- If the number of dedicated master nodes is 2, there are 2 eligible master nodes. If minimum_master_nodes is set to 1, although there is a backup node, there may be a risk of split-brain (i.e., each eligible master node sets itself as the master node) when the master node is re-selected in case of network failure. If minimum_master_nodes is set to 2, as the number of eligible master nodes falls short, no master node can be selected in case of failure.
- If the number of dedicated master nodes is 3, there are 3 eligible master nodes. If discovery.zen.minimum_master_nodes is set to 2, even if one eligible master node is lost in case of network failure, there is still one master node that can be re-selected.

For more information, see [ES Node Description](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/modules-node.html#master-node).