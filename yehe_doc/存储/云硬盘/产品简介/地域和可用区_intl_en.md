## Regions
A region is the physical location of an IDC. In Tencent Cloud, different regions are fully isolated, ensuring cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.
Regions have the following characteristics:
- The networks of different regions are fully isolated. Tencent Cloud services in different regions **cannot communicate via a private network by default**.
- Tencent Cloud services in different regions can access the Internet through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224), while those in a VPC can use [peering connection](https://intl.cloud.tencent.com/document/product/553) to communicate with each other via Tencent Cloud’s high-speed network, which is faster and steadier.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) currently supports intra-region traffic forwarding by default. If [cross-region binding](https://intl.cloud.tencent.com/document/product/214/12014) is enabled, a CLB instance can be bound to CVM instances in another region.

## Availability Zones
An availability zone is a physical IDC of Tencent Cloud with independent power supply and network resource in a single region. It can ensure business stability, as failures (except for large-scale disaster or major power failure) in one AZ are isolated without affecting other AZs in the same region. By starting an instance in an independent availability zone, users can protect their applications from being affected by a single point of failure.
Availability zones have the following characteristics:
- Tencent Cloud services under the same account in the same [VPC](https://intl.cloud.tencent.com/document/product/215) are interconnected through the private network, meaning they can communicate using [private IPs](https://intl.cloud.tencent.com/document/product/213/5225), even if they are in different availability zones.
- Resources under different Tencent Cloud accounts are availability zone-specific, meaning they cannot communicate via a private network, even if they are in the same region.

<span id="MainlandChina"></span>
## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
	</tr>
	<tr>
		<td rowspan="5">South China (Guangzhou)<br>ap-guangzhou</td>
		<td>Guangzhou Zone 1 (sold out)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Guangzhou Zone 2 (sold out)<br>ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 3<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 4<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 6<br> ap-guangzhou-6</td>
	</tr>
	<tr>
		<td rowspan="5">East China (Shanghai) <br>ap-shanghai</td>
		<td>Shanghai Zone 1<br>ap-shanghai-1</td>
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
			<td rowspan="3">North China (Nanjing)<br>ap-nanjing</td>
			<td>Nanjing Zone 1<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>Nanjing Zone 2<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td>Nanjing Zone 3<br>ap-nanjing-3</td>
	</tr>
	<tr>
			<td rowspan="5">North China (Beijing) <br>ap-beijing</td>
			<td>Beijing Zone 1<br>ap-beijing-1</td>
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
			<td rowspan="2">Hong Kong/Macao/Taiwan (Hong Kong, China) <br>ap-hongkong</td>
			<td>Hong Kong Zone 1 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Hong Kong Zone 2 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>
## Other Countries and Regions	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>Availability Zone</th>
		</tr>
		<tr>
			<td  rowspan="2">Southeast Asia (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Singapore Zone 2 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td  rowspan="2">Northeast Asia (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Seoul Zone 2 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-2</td>
		</tr>
		<tr>
			<td >Northeast Asia (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">South Asia (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >Southeast Asia (Bangkok)<br>ap-bangkok </td>
				 <td >Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td>
		<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Tokyo nodes cover services in North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">Western US (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">Eastern US (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (Virginia nodes cover services in Eastern US)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Virginia nodes cover services in Eastern US)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>Europe (Frankfurt) <br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes cover services Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## How to Select Regions and Availability Zones
When selecting a region and availability zone, you need to consider the following factors:
- The limits on where cloud disks can be mounted. A cloud disk can only be mounted to a CVM in the same availability zone.
- The region of the CVM on which the cloud disk will be used, your location, and the location of your users. We recommend that you choose the region closest to your users when purchasing the Tencent Cloud services to minimize access latency and improve access speed.
- The relationship between the CVM on which the cloud disk will be used and other Tencent Cloud services. We recommend that, when you select other Tencent Cloud products, you try to locate them all in the same region and availability zone to allow them to communicate with each other through the private network, reducing access latency and increasing access speeds.
- Business high availability and disaster recovery considerations. Even if you have just one VPC, we still recommend that you deploy your businesses in different availability zones to prevent a single point of failure and enable cross-AZ disaster recovery.
- There may be higher network latency among different availability zones. We recommend that you assess your business requirements and find the optimal balance between high availability and low latency.

## Relevant Operations
Actions such as the use and viewing of cloud disks are availability zone and region-specific. To easily migrate data and services to other regions or construct a cross-region disaster recovery system, you can copy snapshots to other regions. For more information, see [Cross-region Snapshot Replicating](https://intl.cloud.tencent.com/document/product/362/31623).
