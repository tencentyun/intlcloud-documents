Based on native Kubernetes, Tencent Kubernetes Engine (TKE) is a container-oriented, highly scalable, and high-performance container management service. It is fully compatible with the native Kubernetes APIs and adds Tencent Cloud's Kubernetes plugins such as CBS and CLB. It provides containerized applications with a complete set of features ranging from efficient deployment and resource scheduling to service discovery and dynamic scaling, which solves environment consistency issues in the process of development, testing, and OPS, makes it much easier to manage large-scale container clusters, and helps reduce costs and improve efficiency. TKE is free of charge currently, but other involved Tencent Cloud services are billed separately.

TKE operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------------------|------|-------------------------------------|
| Adding existing node                 | tke  | AddExistedInstances                 |
| Canceling application installation                 | tke  | CancelClusterRelease                |
| Opening cluster access port               | tke  | CreateClusterEndpoint               |
| Opening the port for access over public network of managed cluster     | tke  | CreateClusterEndpointVip            |
| Adding (or creating) cluster node           | tke  | CreateClusterInstances              |
| Creating application in cluster                 | tke  | CreateClusterRelease                |
| Deleting cluster                   | tke  | DeleteCluster                       |
| Deleting cluster scaling group                | tke  | DeleteClusterAsGroups               |
| Deleting cluster access port               | tke  | DeleteClusterEndpoint               |
| Deleting the port for access over public network of managed cluster     | tke  | DeleteClusterEndpointVip            |
| Deleting cluster node                 | tke  | DeleteClusterInstances              |
| Querying cluster scaling group attribute                | tke  | DescribeClusterAsGroupOption        |
| Querying cluster scaling group list                | tke  | DescribeClusterAsGroups             |
| Querying the status of cluster access port             | tke  | DescribeClusterEndpointStatus       |
| Querying the openness status of the port for access over public network of managed cluster | tke  | DescribeClusterEndpointVipStatus    |
| Querying cluster node                 | tke  | DescribeClusterInstances            |
| Querying application being installed             | tke  | DescribeClusterPendingReleases      |
| Querying cluster application details               | tke  | DescribeClusterReleaseDetails       |
| Querying installed application in cluster             | tke  | DescribeClusterReleases             |
| Querying cluster key                 | tke  | DescribeClusterSecurity             |
| Draining node                   | tke  | DrainClusterNode                    |
| Modifying cluster scaling group attribute              | tke  | ModifyClusterAsGroupAttribute       |
| Modifying cluster scaling attribute               | tke  | ModifyClusterAsGroupOptionAttribute |
| Modifying cluster attribute                 | tke  | ModifyClusterAttribute              |
| Modifying the security group of the port for access over public network for managed cluster    | tke  | ModifyClusterEndpointSP             |
| Deleting installed application                | tke  | UninstallClusterRelease             |
| Upgrading cluster authorization mode              | tke  | UpgradeClusterAuthorizationMode     |
| Upgrading application                   | tke  | UpgradeClusterRelease               |
| Deleting image repositories in batches             | ccr | BatchDeleteRepository              |
| Deleting image tags in batches           | ccr | BatchDeleteTag                     |
| Creating image repository namespace           | ccr | CreateCCRNamespace                 |
| Creating image repository               | ccr | CreateRepository                   |
| Adding node                 | ccs | AddClusterInstances                |
| Adding existing CVM instance to cluster               | ccs | AddClusterInstancesFromExistedCvm  |
| Checking for cluster route table conflict          | ccs | CheckClusterRouteTableCidrConflict |
| Creating cluster                 | ccs | CreateCluster                      |
| Creating cluster namespace             | ccs | CreateClusterNamespace             |
| Creating cluster route               | ccs | CreateClusterRoute                 |
| Creating cluster route table              | ccs | CreateClusterRouteTable            |
| Creating service                 | ccs | CreateClusterService               |
| Creating CLB instance               | ccs | CreateIngress                      |
| Creating log collector              | ccs | CreateLogCollector                 |
| Deleting cluster                 | ccs | DeleteCluster                      |
| Deleting cluster namespace             | ccs | DeleteClusterNamespace             |
| Deleting cluster route               | ccs | DeleteClusterRoute                 |
| Deleting cluster route table              | ccs | DeleteClusterRouteTable            |
| Deleting service                 | ccs | DeleteClusterService               |
| Deleting instance                 | ccs | DeleteInstances                    |
| Deleting log collector              | ccs | DeleteLogCollector                 |
| Pulling cluster list               | ccs | DescribeCluster                    |
| Pulling cluster container list             | ccs | DescribeClusterContainer           |
| Pulling server list               | ccs | DescribeClusterInstances           |
| Pulling namespace list             | ccs | DescribeClusterNamespaces          |
| Pulling the request and limit information of cluster | ccs | DescribeClusterRequestLimitInfo    |
| Querying cluster route               | ccs | DescribeClusterRoute               |
| Querying cluster route table              | ccs | DescribeClusterRouteTable          |
| Pulling service list               | ccs | DescribeClusterService             |
| Pulling service details             | ccs | DescribeClusterServiceInfo         |
| Pulling the list of layer-7 CLB instances           | ccs | DescribeIngress                    |
| Getting container log               | ccs | DescribeInstanceLog                |
| Pulling service event list             | ccs | DescribeServiceEvent               |
| Pulling instance list               | ccs | DescribeServiceInstance            |
| Enabling cluster log service             | ccs | EnableLogDaemon                    |
| Getting log collector              | ccs | GetLogCollector                    |
| Getting the enablement status of cluster log service       | ccs | GetLogDaemonStatus                 |
| Listing log collectors              | ccs | ListLogCollector                   |
| Setting whether the cluster node is schedulable         | ccs | ModifyClusterNodeSchedulable       |
| Modifying service                 | ccs | ModifyClusterService               |
| Modifying cluster service image             | ccs | ModifyClusterServiceImage          |
| Updating the number of instances               | ccs | ModifyServiceReplicas              |
| Modifying CLB instance               | ccs | MosifyIngress                      |
| Redeploying service               | ccs | RedeployClusterService             |
| Rolling back service                 | ccs | RollbackClusterService             |


