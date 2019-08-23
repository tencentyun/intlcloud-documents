## Release 3

Release time: April 28, 2019 15:37:22

Release updates:

Improvements on the existing documents.

New APIs:

* [CreateCluster](/document/api/457/34527)

Modified APIs:

* [DescribeClusterInstances](/document/api/457/31863)
	* **Modified input parameters:** InstanceIds

New data structures:

* [ClusterAdvancedSettings](/document/api/457/31866#ClusterAdvancedSettings)
* [ClusterBasicSettings](/document/api/457/31866#ClusterBasicSettings)
* [ClusterCIDRSettings](/document/api/457/31866#ClusterCIDRSettings)
* [ExistedInstancesForNode](/document/api/457/31866#ExistedInstancesForNode)
* [ExistedInstancesPara](/document/api/457/31866#ExistedInstancesPara)
* [RunInstancesForNode](/document/api/457/31866#RunInstancesForNode)

Modified data structures:

* [Cluster](/document/api/457/31866#Cluster)
	* New members: ProjectId

## Release 2

Release time: February 22, 2019 15:16:39

Release updates:

Improvements on the existing documents.

Modified APIs:

* [DescribeClusters](/document/api/457/31862)
	* New input parameters: Filters

New data structures:

* [Filter](/document/api/457/31866#Filter)

Modified data structures:

* [Cluster](/document/api/457/31866#Cluster)
	* New members: ClusterNodeNum
	* **Modify members:** ClusterDescription
* [ClusterNetworkSettings](/document/api/457/31866#ClusterNetworkSettings)
	* New members: Ipvs
	* **Deleted members:** IPVS

## Release 1

Release time: December 24, 2018 17:32:12

Release updates: 

Improvements on the existing documents.

New APIs:

* [AddExistedInstances](/document/api/457/31865)
* [DeleteClusterInstances](/document/api/457/31864)
* [DescribeClusterInstances](/document/api/457/31863)
* [DescribeClusters](/document/api/457/31862)

New data structures:

* [Cluster](/document/api/457/31866#Cluster)
* [ClusterNetworkSettings](/document/api/457/31866#ClusterNetworkSettings)
* [EnhancedService](/document/api/457/31866#EnhancedService)
* [Instance](/document/api/457/31866#Instance)
* [InstanceAdvancedSettings](/document/api/457/31866#InstanceAdvancedSettings)
* [LoginSettings](/document/api/457/31866#LoginSettings)
* [RunMonitorServiceEnabled](/document/api/457/31866#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](/document/api/457/31866#RunSecurityServiceEnabled)

