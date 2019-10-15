## Region
A region is the physical geographic location of the data center. Different regions of Tencent Cloud are completely isolated, ensuring maximum stability and fault tolerance between different regions. In order to reduce access latency and increase download speed, we recommend you select the region that is closest to your clients.
Regions have the following characteristics:
- Network between different regions is completely isolated. Cloud products in different regions **cannot communicate through private network by default**.
- Cloud products in different regions can access the Internet through [Public IP](https://intl.cloud.tencent.com/document/product/213/5224). Cloud products in a VPC can also use Tencent Cloud’s [Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000) to communicate with each other by using Tencent Cloud’s high-speed network to implement a connection that is faster and more stable than Internet access.
-[Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) currently supports intra-region traffic forwarding by default. If the [Cross-region binding](https://intl.cloud.tencent.com/document/product/214/12014) function is enabled, it supports cross-region binding of load balancer and CVM.


## Availability Zone
Availability zones refer to Tencent Cloud’s physical data centers that are in the same region and have independent power and network resources. They are designed to ensure that failures within one availability zone can be isolated (except for large-scale disasters or major power failures) without affecting other zones, ensuring users' business stability. By starting an instance in an independent availability zone, users can protect their applications from being affected by failures that occur in a single location.
Availability zones have the following characteristics:
- For cloud products under the same Tencent Cloud account, if in the same region but different availability zones and under the same [VPC](https://cloud.tencent.com/document/product/215), they can communicate with each other through the private network, and [Private IP](https://intl.cloud.tencent.com/document/product/213/5225) can be used for direct access.
- Resources in the same region but different availability zones and under different Tencent Cloud accounts are completely isolated in the private network.

## Mainland China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
	</tr>
	<tr>
		<td rowspan="4">South China (Guangzhou)<br>ap-guangzhou</td>
		<td>Guangzhou Zone 1 (Sold out)<br>ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Guangzhou Zone 2<br>ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 3<br>ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 4<br>ap-guangzhou-4</td>
	</tr>   
	<tr>
			<td>South China (Guangzhou Open)<br>ap-guangzhou-open</td>
			<td>Open Zone<br>ap-guangzhou-open-1</td>
	</tr>
	<tr>
		
	</tr>
	<tr>
		<td rowspan="4">East China (Shanghai)<br>ap-shanghai</td>
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
			<td>East China (Jinan EC)<br>ap-jinan</td>
			<td>Jinan EC Zone 1<br>ap-jinan-1</td>
	</tr>
	<tr>
			<td rowspan="4">North China (Beijing)<br>ap-beijing</td>
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
		<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
		<td>Chengdu Zone 1<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>Chengdu Zone 2<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td>Southwest China (Chongqing)<br>ap-chongqing</td>
			<td>Chongqing Zone 1<br>ap-chongqing-1</td>
	</tr>
</tbody>
</table>	

## Overseas Regions	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>Availability Zone</th>
		</tr>
		<tr>
			<td rowspan="2">Southeast Asia (Hong Kong, China)<br>ap-hongkong</td>
			<td> Hong Kong Zone 1 (Hong Kong, China node can be used to cover Southeast Asia)<br>ap-hongkong-1</td>
		</tr>
<tr>
			<td> Hong Kong Zone 2 (Hong Kong, China node can be used to cover Southeast Asia)<br>ap-hongkong-2</td>
		   </tr>
		<tr>
			<td>Southeast Asia (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Singapore node can be used to cover Southeast Asia)<br>ap-singapore-1</td>
		</tr>
		<tr>
		  	<td>Asia Pacific (Bangkok)<br>ap-bangkok</td>
				 <td>Bangkok Zone 1 (Bangkok node can be used to cover Southeast Asia)<br>ap-bangkok-1</td>
		<tr>
       <tr>
			<td  rowspan="2">Asia Pacific (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai node can be used to cover Southeast Asia)<br>ap-mumbai-1</td>
		</tr>
<tr>
			<td>Mumbai Zone 2 (Mumbai node can be used to cover Southeast Asia)<br>ap-mumbai-2</td>
		   </tr>
		<tr>
			<td>Asia Pacific (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul node can be used to cover Northeast Asia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td> Asia Pacific (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Tokyo node can be used to cover Northeast Asia)<br>ap-tokyo-1</td>
		</tr>
		<tr>
			<td rowspan="2">Western USA (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley node can be used to cover the Western USA)<br>na-siliconvalley-1</td>
		</tr>
          <tr>
			<td>Silicon Valley Zone 2 (Silicon Valley node can be used to cover the Western USA)<br>na-siliconvalley-2</td>
		   </tr>
		<tr>
		<tr>
			<td>Eastern USA (Virginia)<br>na-ashburn</td>
			<td>Virginia Zone 1 (Virginia node can be used to cover Eastern USA)<br>na-ashburn-1</td>
		</tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Toronto node can be used to cover North America)<br>na-toronto-1</td>
		</tr>
			<td>Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt node can be used to cover Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td>Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow node can be used to cover Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## How to select region and availability zone
When selecting a region and availability zone, you need to consider the following factors:
- The limits on where the cloud disk can be mounted. A cloud disk can only be mounted to a CVM in the same availability zone.
- The geographic location of the CVM where you need to use the cloud disk, your location, and that of your target users. We recommend that when purchasing cloud services, you select the geographic location closest to your clients in order to reduce access latency and increase access speed.
- The relationship between the CVM where you need to use the cloud disk and other cloud products. We recommend that you select cloud products in the same region and availability zone, so that each product can communicate through the private network, reducing access latency and increasing access speed.
- Business high availability and disaster recovery considerations. In scenarios where there is only one VPC, we recommend that you at least deploy businesses in different availability zones to ensure fault isolation, implementing cross-availability zone disaster recovery.
- Different availability zones can have network communication latency, which needs to be evaluated in conjunction with your actual business requirements to find the balance between high availability and low latency.

## Related Actions
Your actions such as the use and viewing of cloud disks are zone and region-specific. To easily migrate data and services to other regions or to construct a cross-region disaster recovery system, you can copy snapshots to other regions. For more information, see [Cross-region snapshot replication](https://intl.cloud.tencent.com/document/product/362/31623).

