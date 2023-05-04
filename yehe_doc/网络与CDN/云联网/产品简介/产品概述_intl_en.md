## What is Cloud Connect Network
Cloud Connect Network (CCN) can establish [VPC](https://intl.cloud.tencent.com/document/product/215/535)–to-VPC connections and VPC-IDC connections. It provides you with public and private network multi-point interconnection, automatically synced routes, linkage prioritization, failure fast convergence, and other capabilities. With its presence in over 30 regions around the world, over 100 Gbps bandwidth and 99.99% high availability.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/g3KM113_%E5%9B%BE%E7%89%871.png)

## Product Components
Configuration of a CCN instance includes:
- Associated network instances: Network instances added to the same CCN instance can communicate with each other. Supported resources include VPC, VPC (BM), direct connect gateways, and VPN gateways. For more information, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
>? For CCN to automatically add the routes from the VPN gateway, the VPN gateway for CCN has the VPN tunnel created and SPD policy configured. For more information, see [Connecting IDC to CCN Through VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/36018).
- Route table: CCN automatically syncs routes of network instances added and presents them in its route table. For more information, see [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).

## Description
CCN has the following features:
#### Public and private network interconnection
CCN features multi-node multi-route-level automatic forwarding and syncing on the public and private network and route convergence in seconds, which allows you to interconnect all network instances with a simple step, and manage them easily.
#### Smart learning and scheduling
CCN frees you from the heavy route maintenance with its Full Mesh interconnection between multiple nodes and links in public and private networks. The smart scheduling system monitors the multi-layer network topology, routes, and traffic of the entire network to connect your local services to the nearest point and ensure interconnection using the shortest link.
#### Automatic route forwarding
CCN automatically syncs multi-level routes, and updates the routing table if your network topology changes. This simple management replaces your extra manual configuration or updates, which in turn, greatly improves the scalability and OPS efficiency of your network.

## Feature Comparison
#### CCN vs. peering connection/dedicated tunnel
Without CCN, if you want to connect multiple VPCs with your cloud IDC, or connect to your cloud IDC via a direct connection, you need set up peering connections between each pair of VPC endpoints, and create dedicated channels and gateways between of each VPCs and the direct connection. At the same time, the VPC and IDC IP ranges cannot overlap. After establishing the connection, you must manage the route tables of instances and manually add routing policies to make it all work.

On the other hand, doing the same with CCN would only require a CCN instance and adding all VPCs and direct connect gateway to the CCN instance. Only one DC channel and gateway are required for one direct connection. CCN can automatically forward and sync all routes, saving you the hassle of manually configuring and managing the route tables of the instances.
>? For more information on how to migrate existing applications to CCN, see [Best Practices](https://intl.cloud.tencent.com/document/product/1003/30078).
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JLF3771_%E5%9B%BE%E7%89%871.png)
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
<td >Routing</td>
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
<td>Stability and reliability</td>
<td>Multi-cluster disaster recovery in a single zone.</td>
<td>Multi-zone hot backup disaster recovery with 99.99% high availability.</td>
</tr>
<tr>
<td >Costs</td>
<td>
1. Pay for each link separately.<br />
2. Relatively higher unit price. 
</td>
<td>
1. Pay for all bandwidth in a region as a whole (similar to bandwidth packages), which evens out the price.<br />
2. Lower unit price.
</td>
</tr>	
<tr>
<td>Latency</td>
<td>Connections are established using lines randomly selected among multiple underlying lines. The latency difference can be 10 ms or more and the latency fluctuates.</td>
<td>Select the optimal line.</td>
</tr>
</table> 
