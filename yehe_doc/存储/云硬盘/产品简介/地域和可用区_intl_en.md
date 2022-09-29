## Regions
A region is the physical location of an IDC. In Tencent Cloud, regions are fully isolated from each other, ensuring cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.
Regions have the following characteristics:
- The networks of different regions are fully isolated. Tencent Cloud services in different regions **cannot communicate via a private network by default**.
- Cloud products in different regions can access the Internet through the [public network service](https://intl.cloud.tencent.com/document/product/213/5224). Cloud products in a VPC can also use Tencent Cloud's [Peering Connection](https://www.tencentcloud.com/document/product/553) to communicate with each other by using Tencent Cloud's high-speed network to implement a connection that is faster and more stable than Internet access.
- [Cloud Load Balancer](https://www.tencentcloud.com/document/product/214) currently supports intra-region traffic forwarding by default. If you enable the [cross-region binding](https://www.tencentcloud.com/document/product/214/12014) feature, a CLB instance can be bound to CVM instances in another region.



## Availability Zones
An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network in the same region. It can ensure business stability, as failures (except for major disasters or power failures) in one AZ are isolated without affecting other AZs in the same region. By starting an instance in an independent AZ, users can protect their applications from being affected by a single point of failure.
Availability zones have the following characteristics:
- For cloud products under the same Tencent Cloud account, products in the same region but different availability zones and under the same [VPC](https://www.tencentcloud.com/document/product/215) can communicate with each other through the private network, and the [private network service](https://intl.cloud.tencent.com/document/product/213/5225) can be used for direct access.
- Resources under different Tencent Cloud accounts are availability zone-specific, meaning they cannot communicate via a private network, even if they are in the same region.

[](id:MainlandChina)
## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>AZ</th>
	</tr>
	<tr>
		<td rowspan="6">South China (Guangzhou)<br>ap-guangzhou</td>
		<td>Guangzhou Zone 1 (sold out)<br>ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Guangzhou Zone 2 (sold out)<br>ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 3<br>ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 4<br>ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 6<br>ap-guangzhou-6</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 7<br>ap-guangzhou-7</td>
	</tr>
	<tr>
		<td rowspan="6">East China (Shanghai)<br>ap-shanghai</td>
		<td>Shanghai Zone 1 (sold out)<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>Shanghai Zone 2<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Shanghai Zone 4<br>ap-shanghai-4</td>
	</tr>
 <tr>
		<td>Shanghai Zone 5<br>ap-shanghai-5</td>
	</tr>
	<tr>
		<td>Shanghai Zone 8<br>ap-shanghai-8</td>
	</tr>
		<tr>
			<td rowspan="3">East China (Nanjing)<br>ap-nanjing</td>
			<td>Nanjing Zone 1<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>Nanjing Zone 2<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td>Nanjing Zone 3<br>ap-nanjing-3</td>
	</tr>
		<tr>
			<td rowspan="7">North China (Beijing)<br>ap-beijing</td>
			<td>Beijing Zone 1 (sold out)<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>Beijing Zone 2<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>Beijing Zone 3<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>Beijing Zone 4<br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>Beijing Zone 5<br>ap-beijing-5</td>
	</tr>
		<tr>
			<td>Beijing Zone 6<br>ap-beijing-6</td>
	</tr>
		<tr>
			<td>Beijing Zone 7<br>ap-beijing-7</td>
	</tr>
	<tr>
		<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
		<td>Chengdu Zone 1<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>Chengdu Zone 2<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >Southwest China (Chongqing)<br>ap-chongqing</td>
			<td>Chongqing Zone 1<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="3">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
			<td>Hong Kong Zone 1 (Nodes in Hong Kong, China can cover Hong Kong/Macao/Taiwan regions) (sold out)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Hong Kong Zone 2 (Nodes in Hong Kong, China can cover Hong Kong/Macao/Taiwan regions)<br>ap-hongkong-2</td>
	</tr>
		<tr>
			<td>Hong Kong Zone 3 (Nodes in Hong Kong, China can cover Hong Kong/Macao/Taiwan regions)<br>ap-hongkong-3</td>
	</tr>
</tbody>
</table>

<dx-alert infotype="explain" title="">
The product is in beta test for Jinan, Hangzhou, Fuzhou, Wuhan, Changsha, and Shijiazhuang regions. To try it out, submit a ticket for application.
</dx-alert>

[](id:InternationalArea)
## Other Countries and Regions	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>AZ</th>
		</tr>
		<tr>
			<td  rowspan="4">Southeast Asia (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Nodes in Singapore can cover Southeast Asia)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Singapore Zone 2 (Nodes in Singapore can cover Southeast Asia)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>Singapore Zone 3 (Nodes in Singapore can cover Southeast Asia)<br>ap-singapore-3</td>
		</tr>
		<tr>
			<td>Singapore Zone 4 (Nodes in Singapore can cover Southeast Asia)<br>ap-singapore-4</td>
		</tr>
		<tr>
			<td rowspan="2">Southeast Asia (Jakarta)<br>ap-jakarta</td>
			<td>Jakarta Zone 1 (Nodes in Jakarta can cover Southeast Asia)<br>ap-jakarta-1</td>
		</tr>
		<tr>
			<td>Jakarta Zone 2 (Nodes in Jakarta can cover Southeast Asia)<br>ap-jakarta-2</td>
		</tr>
		<tr>
			<td  rowspan="2">Northeast Asia (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Nodes in Seoul can cover Northeast Asia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Seoul Zone 2 (Nodes in Seoul can cover Northeast Asia)<br>ap-seoul-2</td>
		</tr>
		<tr>
			<td rowspan="2">Northeast Asia (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Nodes in Tokyo can cover Northeast Asia)<br>ap-tokyo-1</td>
		</tr>
			<tr>
			<td>Tokyo Zone 2 (Tokyo nodes can cover services in Northeast Asia)<br>ap-tokyo-2</td>
		</tr>
       <tr>
			<td  rowspan="2">South Asia (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Nodes in Mumbai can cover South Asia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Nodes in Mumbai can cover South Asia) <br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td rowspan=2>Southeast Asia (Bangkok)<br>ap-bangkok</td>
				 <td >Bangkok Zone 1 (Nodes in Bangkok can cover Southeast Asia)<br>ap-bangkok-1</td>
		</tr>
		<tr>
				 <td >Bangkok Zone 2 (Nodes in Bangkok can cover Southeast Asia)<br>ap-bangkok-2</td>
		<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Nodes in Toronto can cover North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td>South America (São Paulo)<br>sa-saopaulo</td>
			<td>Sao Paulo Zone 1 (Sao Paulo nodes cover services in South America)<br>sa-saopaulo-1</td>
		</tr>
		<tr>
			<td rowspan="2">Western US (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Nodes in Silicon Valley can cover Western US)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Nodes in Silicon Valley can cover Western US)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">Eastern US (Virginia)<br>na-ashburn</td>
			<td>Virginia Zone 1 (Nodes in Virginia can cover Eastern US)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Nodes in Virginia can cover Eastern US)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td rowspan="2">Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Nodes in Frankfurt can cover Europe)<br>eu-frankfurt-1</td>
		</tr>
		<tr>
			<td>Frankfurt Zone 2 (Nodes in Frankfurt can cover Europe)<br>eu-frankfurt-2</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Northeast Europe Zone 1 (Nodes in Moscow can cover Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## Selection of Regions and AZs
When selecting a region and availability zone, take the following into consideration:
- A cloud disk can only be attached to a CVM in the same availability zone.
- The region of the CVM on which the cloud disk will be used, your location, and the location of your users. We recommend that you choose the region closest to your end users when purchasing Tencent Cloud services to minimize access latency and improve access speed.
- The relationship between the CVM on which the cloud disk will be used and other Tencent Cloud services. When you select other Tencent Cloud services, we recommend you try to locate them all in the same availability zone of a single region to allow them to communicate with each other through the private network, reducing access latency and increasing access speed.
- High availability and disaster recovery. Even if you have just one VPC, we still recommend that you deploy your businesses in different availability zones to prevent a single point of failure and enable cross-AZ disaster recovery.
- There may be network latency among different AZs. We recommend you assess your business requirements and find the optimal balance between high availability and low latency.

## Related Operations
Actions such as the use and viewing of cloud disks are region-specific. To easily migrate data and services to other regions or construct a cross-region disaster recovery system, you can copy snapshots to other regions. For more information, see [Cross-region Snapshot Replicating](https://intl.cloud.tencent.com/document/product/362/31623).
