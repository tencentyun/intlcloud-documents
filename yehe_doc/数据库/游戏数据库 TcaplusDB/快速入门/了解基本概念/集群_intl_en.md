## Cluster Overview
A cluster is the basic TcaplusDB management unit, which provides independent TcaplusDB service for business.
From the perspective of gaming business, a cluster can provide service for either a game's independent submodules or the entire game.

## Creating Cluster
For detailed directions, please see [Creating Cluster](https://intl.cloud.tencent.com/document/product/1016/32714).


## Cluster Details
You can view the cluster configuration and attributes details by logging in to the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/app) and then clicking the ID of the target cluster.
Cluster details consist of three parts:

##### Basic information
- Cluster ID: unique cluster ID, which can be used to locate the cluster and control access to the cluster but cannot be used for database connection.
- Access ID: cluster connection ID, which identifies the cluster when you access the database through the SDK or client tool.
- Connection protocol: table definition protocols supported by cluster. Currently, only Protocol Buffers is supported.
- Cluster name: cluster name, which can be customized as needed.
- Region: cluster region.
- RESTful API	: address used for database access through a RESTful API in the same VPC subnet.

##### Network information
- Network: information of the VPC where the current cluster resides.
- Subnet: information of the subnet where the current cluster resides.
- Private address: private IP address assigned to the current cluster. CVM instances in the same VPC subnet as the cluster can access this IP address.
- Private port: access port number assigned to the current cluster.

##### Other information
- Creation time: creation time of the current cluster.
- Connection password: if you forgot the password, you can view the cluster access password in the [console](https://console.cloud.tencent.com/tcaplusdb/app).
