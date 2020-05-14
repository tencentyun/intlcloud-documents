## What is Cloud Connect Network (CCN)
CCN is the bridge that connects Tencent Cloud [VPCs](https://intl.cloud.tencent.com/document/product/215/535), and VPCs with on-premise IDCs. It provides public and private network multi-point interconnection, self-taught learning routing, linkage prioritization, and fast failure convergence. CCN covers 20+ regions around the world, supports 100+ Gbps bandwidth and 99.99% high availability, allowing you to easily build fast, stable, secure, and flexible globally interconnected networks. Its typical use cases include the following: 
1. **High-quality private network connection between VPCs**: online education with real-time audio and video systems across regions, game acceleration using private network interconnection across regions, and cross-region disaster recovery.
2. **Private network connection between VPCs and on-premises IDCs**: create a [dedicated tunnel](https://intl.cloud.tencent.com/document/product/216) once and connect multiple VPCs for public and private network interconnection. Ideal for hybrid clouds.

## Components
A CCN has the following components:
- Associated network instances: network instances within the same CCN instance can communicate with each other. Supported network instance types include VPC, VPC (BM), and direct connect gateway. For more information, refer to [Associating Network Instance](https://intl.cloud.tencent.com/document/product/1003/30064).
- Route table: when network instances are added, the CCN instance can automatically learn the related routes and present them in its route table. For more information, refer to [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).


## Features
CCN has the following features:

**Public and private network interconnection**

CCN features multi-node multi-route-level automatic forwarding and learning on the public and private network and route convergence in seconds, which allows for all network instances to interconnect with a simple step and makes management a breeze.

**Smart learning and scheduling**

CCN frees you from the complex task of maintaining routing tables with Full Mesh interconnection between multiple nodes and links in public and private networks. The smart scheduling system monitors the multi-layer network topology, routes, and traffic of the entire network to allow connecting local services to the nearest point and ensure interconnection using the shortest link.

**Automatic route forwarding**

CCN supports multi-level route automatic learning. When your network topology changes, the routing table is automatically updated. You do not need to do additional configuration or updates. This simplifies your management requirements, which in turn, greatly improves the scalability and OPS efficiency of your network.

## Feature Comparison
**Differences between CCN and peering connection/dedicated tunnel**

Without CCN, if you want to interconnect multiple VPCs and your IDC with multiple VPCs, you need to establish one peering connection for each pair of VPCs and one dedicated tunnel between your IDC and each VPC. For the connections to work, you also need to make sure VPC and IDC IP ranges do not overlap. Finally, you must manage the route tables of instances and manually add routing policies to make it all work. 

On the other hand, doing the same with CCN would only require a CCN instance and adding all VPCs and the IDC to the CCN instance. After you add the instances to the CCN, it will automatically forward and learn all routes, saving you the hassle of manually configuring and managing the route tables of the instances.
> For information on how to migrate existing applications to CCN, refer to [Best Practices](https://intl.cloud.tencent.com/document/product/1003/30078).

<body>

<table>
	<tr>
		<th>CCN benefit</th>
		<th>Peering connection/Dedicated tunnel</th>
		<th>CCN</th>
	</tr>
	<tr>
		<td>Full-mesh interconnection</td>
		<td>1. To interconnect multiple VPCs, you need to establish Cn2 peers.<br />
			2. A single dedicated tunnel can only connect to one VPC.<br />	
			3. VPCs with overlapping IP ranges cannot be peered.
		</td>
		<td>1. No peering connection needed. Full mesh interconnection for all instances added to the CCN instance.<br />
			2. Each dedicated tunnel can communicate with all VPCs and IDCs.<br />	
			3. CCN allows for network instances with overlapping CIDR blocks. This provides greater flexibility for interconnection.
		</td>
	</tr>
	<tr>
		<td >Automatic route learning</td>
		<td >
			1. Routes must be configured for each link.<br />
			2. Link changes require manual updates.<br />
		</td>
		<td >
			1. Routes are automatically learned and forwarded.<br />
			2. Route tables are dynamically updated without manual maintenance.<br />
		</td>
	</tr>
	<tr>
		<td>Greater stability and reliability</td>
		<td>Multi-cluster disaster recovery in a single zone.</td>
		<td>Multi-zone hot backup disaster recovery with 99.99% availability.</td>
	</tr>
	<tr>
		<td >Lower costs</td>
		<td >
			1. You pay for each link separately.<br />
			2. Higher unit price. 
		</td>
		<td >
			1. You pay for all bandwidth in a region as a whole (similar to bandwidth packages), which evens out the price.<br />
			2. Unit price is more competitive.
		</td>
	</tr>	
	<tr>
		<td>Lower latency</td>
		<td>Connections are established using lines randomly selected among multiple underlying lines. The latency difference can be 10 ms or more and the latency fluctuates.</td>
		<td>Selects the optimal line.</td>
	</tr>
	</table>    

