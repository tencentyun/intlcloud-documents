## What is Cloud Connect Network
Cloud Connect Network (CCN) bridges between a Tencent Cloud [VPC](https://intl.cloud.tencent.com/document/product/215/535) and another or between VPCs and local IDCs. It provides you with public and private network multi-point interconnection, automatically synced routes, linkage prioritization, failure fast convergence, and other capabilities. With its presence in over 20 regions around the world, over 100 Gbps bandwidth and 99.99% high availability, it helps you easily build a fast, stable, secure, and flexible global network. CCN is typically used in:
1. **High-quality private network connection between VPCs**: online education with real-time audio and video systems across regions, game acceleration using private network interconnection across regions, and cross-region disaster recovery.
2. **Private network connection between VPCs and on-premises IDCs**: connect multiple VPCs through one [dedicated tunnel](https://intl.cloud.tencent.com/document/product/216) for public and private network interconnection by a single access. Ideal for hybrid clouds.


## Product Components
A CCN consists of:
- Associated network instances: network instances within the same CCN instance can communicate with each other. Instances including VPC, VPC (BM), direct connect gateway, and VPN gateway can be added to CCN. For more information, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
>? For CCN to automatically add the routes from the VPN gateway, the VPN gateway for CCN has the VPN tunnel created and SPD policy configured. For more information, see [Connecting IDC to CCN Through VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/36018).
- Route table: CCN automatically syncs routes of network instances added and presents them in its route table. For more information, see [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).


## Features
CCN has the following features:
#### Public and private network interconnection
CCN features multi-node multi-route-level automatic forwarding and syncing on the public and private network and route convergence in seconds, which allows you to interconnect all network instances with a simple step, and manage them easily.
#### Smart learning and scheduling
CCN frees you from the heavy route maintenance with its Full Mesh interconnection between multiple nodes and links in public and private networks. The smart scheduling system monitors the multi-layer network topology, routes, and traffic of the entire network to connect your local services to the nearest point and ensure interconnection using the shortest link.
#### Automatic route forwarding
CCN automatically syncs multi-level routes, and updates the routing table if your network topology changes. This simple management replaces your extra manual configuration or updates, which in turn, greatly improves the scalability and OPS efficiency of your network.

## Feature Comparison
#### CCN vs. peering connection/dedicated tunnel
Without CCN, if you want to interconnect multiple VPCs or your IDC with multiple VPCs, you need to establish one peering connection for each pair of VPCs and one dedicated tunnel between your IDC and each VPC. And then, you also need to make sure VPC and IDC IP ranges do not overlap. After establishing the connection, you must manage the route tables of instances and manually add routing policies to make it all work. 

On the other hand, doing the same with CCN would only require a CCN instance and adding all VPCs and the IDC to the CCN instance. After you add the instances to the CCN, it will automatically forward and sync all routes, saving you the hassle of manually configuring and managing the route tables of the instances.
>? For more information on how to migrate existing applications to CCN, see [Best Practices](https://intl.cloud.tencent.com/document/product/1003/30078).
>
![]()

<table>
	<tr>
		<th>CCN Benefit</th>
		<th>Peering Connection/Dedicated Tunnel</th>
		<th>CCN</th>
	</tr>
	<tr>
		<td>Full-mesh links</td>
		<td>1. To interconnect n VPCs, you need to establish Cn2 peering connections, where Cn2 equals to n * (n-1)/2. Namely, six peering connections are required for interconnecting four VPCs.<br />
			2. A single dedicated tunnel can only connect to one VPC.<br />	
			3. Peer connections cannot be established between VPCs with overlapping IP ranges.
		</td>
		<td>1. All instances added to the CCN instance are in a full mesh interconnection.<br />
			2. Each dedicated tunnel can communicate with all VPCs and IDCs.<br />	
			3. CCN allows for network instances with overlapping CIDR blocks. This provides greater flexibility for interconnection.<br />
		</td>
	</tr>
	<tr>
		<td >Automatic route learning</td>
		<td>
			1. Routes must be configured for every link.<br />
			2. Manual updates are required for any link change.<br />
		</td>
		<td>
			1. Routes are automatically learned and forwarded.<br />
			2. Route tables are dynamically updated without manual maintenance.<br />
		</td>
	</tr>
	<tr>
		<td>Greater stability and reliability</td>
		<td>Multi-cluster disaster recovery in a single zone.</td>
		<td>Multi-zone hot backup disaster recovery with 99.99% high availability.</td>
	</tr>
	<tr>
		<td >Lower costs</td>
		<td>
			1. You pay for each link separately.<br />
			2. You pay a higher unit price. 
		</td>
		<td>
			1. You pay for all bandwidth in a region as a whole (similar to bandwidth packages), which evens out the price.<br />
			2. Unit price is more competitive.
		</td>
	</tr>	
	<tr>
		<td>Lower latency</td>
		<td>Connections are established using lines randomly selected among multiple underlying lines. The latency difference can be 10 ms or more and the latency fluctuates.</td>
		<td>Select the optimal line.</td>
	</tr>
</table>    
