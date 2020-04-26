## Scenario
This document describes how to create an edge cluster to use TKE Edge from the Tencent Cloud TKE console.

## Prerequisites
- To use TKE Edge, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
- Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) to activate the required permissions.

## Notes on the Container Network
Edge TKE uses the node-side network to build the overlay network. Therefore, ensure that the cluster network and container network do not conflict with the node network on the edge server side.

## Directions
1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Edge Clusters** in the left sidebar.
2. On the "Edge Clusters" page, click **Create** to go to the "Create Edge Cluster" page.
3. On the "Create Edge Cluster" page, create an edge cluster based on the following information.
 - **Cluster name**: indicates the name of the edge cluster to be created, with a maximum length of 60 characters.
 - **Kubernetes version**: Kubernetes version 1.16 is currently supported. This version will be updated when a newer Kubernetes version is published by the Kubernetes community.
 - **Region**: select the region that is closest to your location to minimize access latency and improve the download speed.
 - **Cluster network**: assign a network for the cluster according to the internal network management of edge servers.
 - **Pod CIDR**: you need to assign a container network for the cluster according to the internal network management of edge servers. Therefore, plan the cluster size in advance to assign an IP range with sufficient IP addresses for the container network. **The pod CIDR block cannot overlap with IP ranges used by a VPC instance and existing Kubernetes clusters in the VPC instance. In addition, it cannot be modified once created.**
 - **Service CIDR**: you need to assign a service network for the cluster according to the internal network management of edge servers. Therefore, plan the cluster size in advance to assign an IP range with sufficient IP addresses for the service network. **The service CIDR block cannot overlap with IP ranges used by a VPC instance and existing Kubernetes clusters in the VPC instance. In addition, it cannot be modified once created.**
 - **Cluster description**: indicates information about the cluster, which is displayed on the **Cluster Information** page.
4. Click **Done** to finish creating the Master components of the cluster. You can check the progress of cluster creation on the "Edge Clusters" page.


## Next Steps
Go to "Node Management" and add nodes to the created edge cluster.

