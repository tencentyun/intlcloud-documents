## Regions
A region is the physical geographic location of the data center. Different regions of Tencent Cloud are completely isolated, ensuring maximum stability and fault tolerance between different regions. To reduce access latency and increase the download speed, we recommend that you select the region that is closest to your clients.
Regions have the following characteristics:
- Networks between different regions are completely isolated. Cloud products in different regions **cannot communicate through the private network by default**.
- Cloud products in different regions can access the Internet by using the [public network service](https://intl.cloud.tencent.com/document/product/213/5224). Cloud products in a VPC instance can also use Tencent Cloud’s [peering connection](https://intl.cloud.tencent.com/document/product/553) feature to communicate with each other through Tencent Cloud’s high-speed network to establish a connection that is faster and more stable than Internet access.
-[Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214?from_cn_redirect=1) currently supports intra-region traffic forwarding by default. If the feature of [binding cross-region CLBs](https://intl.cloud.tencent.com/document/product/214/12014) is enabled, the cross-region binding of CLBs and CVMs is supported.

**Notes on the Shenzhen/Shanghai Finance Zone:**
This is a compliance zone tailored to the regulatory requirements of the finance industry, which features high-level security and isolation. Currently, services include CVM, CBS, finance databases, Redis storage, and facial recognition are available. Verified clients in the finance industry can apply to use this zone by submitting tickets. 

## Availability Zones
Availability zones refer to Tencent Cloud’s physical data centers that are in the same region and have independent power and network resources. They are designed to ensure that failures within one availability zone can be isolated (except in the case of large-scale disasters or major power failures) without affecting other zones to ensure users' business stability. By starting an instance in an independent availability zone, users can protect their applications from being affected by failures that occur in a single location.
Availability zones have the following characteristics:
- For cloud products under the same Tencent Cloud account, products in the same region but different availability zones and in the same [VPC](https://intl.cloud.tencent.com/document/product/215) instance can communicate with each other through the private network, and the [private network service](https://intl.cloud.tencent.com/document/product/213/5225) can be used for direct access.
- Resources in the same region but different availability zones and under different Tencent Cloud accounts are completely isolated in the private network.

## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
	</tr>
	<tr>
		<td rowspan="4">South China (Guangzhou)<br>ap-guangzhou</td>
		<td>Guangzhou Zone 1 (sold out)<br>ap-guangzhou-1</td>
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
		<td rowspan="3">South China (Shenzhen Finance)<br>ap-shenzhen-fsi</td>
		<td>Shenzhen Finance Zone 1<span style="background-color: rgb(249, 249, 249);"> (for financial institutions and companies only; to activate it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket to apply</a>)<br>ap-shenzhen-fsi-1</span></td>
	</tr>
	<tr>
		<td>Shenzhen Finance Zone 2<span style="background-color: rgb(249, 249, 249);"> (for financial institutions and companies only; to activate it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket to apply</a>)<br>ap-shenzhen-fsi-2</span></td>
	</tr>
	<tr>
		<td>Shenzhen Finance Zone 3 <span style="background-color: rgb(249, 249, 249);"> (for financial institutions and companies only; to activate it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket to apply</a>)<br>ap-shenzhen-fsi-3</span></td>
	</tr>
	<tr>
		<td rowspan="4">East China (Shanghai) <br>ap-shanghai</td>
		<td>Shanghai Zone 1<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>Shanghai Zone 2<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Shanghai Zone 4 <br>ap-shanghai-4</td>
	</tr>
	<tr>
			<td rowspan="3">East China (Shanghai Finance)<br>ap-shanghai-fsi</td>
			<td>Shanghai Finance Zone 1 (for financial institutions and companies only; to activate it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket to apply</a>)<br>ap-shanghai-fsi-1</td>
	</tr>
	<tr>
			<td>Shanghai Finance Zone 2 (for financial institutions and companies only; to activate it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket to apply</a>)<br>ap-shanghai-fsi-2</td>
	</tr>
	<tr>
			<td>Shanghai Finance Zone 3 (for financial institutions and companies only; to activate it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket to apply</a>)<br>ap-shanghai-fsi-3</td>
	</tr>
	<tr>
		<td rowspan="2">North China (Nanjing)<br>ap-nanjing</td>
		<td>Nanjing Zone 1<br>ap-nanjing-1</td>
	</tr>
	<tr>
		<td>Nanjing Zone 2<br>ap-nanjing-2</td>
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
			<td>Beijing Zone 4 <br>ap-beijing-4</td>
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
			<td rowspan="2">Hong Kong (China), Macao (China), and Taiwan (China) (Hong Kong, China) <br>ap-hongkong</td>
			<td>Hong Kong Zone 1 (nodes in the Hong Kong, China region cover Hong Kong (China), Macao (China), and Taiwan (China)) <br>ap-hongkong-1</td>
</tr>
<tr>
			<td>Hong Kong Zone 2 (nodes in the Hong Kong, China region cover Hong Kong (China), Macao (China), and Taiwan (China)) <br>ap-hongkong-2</td>
</tr>
</tbody>
</table>	

## Other Countries and Regions
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>Availability Zone</th>
		</tr>
<tr>
			<td>Southeast Asia Pacific (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (nodes in the Singapore region cover Southeast Asia)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td >Northeast Asia Pacific (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (nodes in the Seoul region cover Northeast Asia)<br>ap-seoul-1</td>
		</tr>
			<tr>
			<td >Northeast Asia Pacific (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (nodes in the Tokyo region cover Northeast Asia)<br>ap-tokyo-1</td>
		</tr>
		  <tr>
			<td  rowspan="2">South Pacific Asia (Mumbai) <br>ap-mumbai</td>
			<td>Mumbai Zone 1 (nodes in the Mumbai region cover Southeast Asia)<br>ap-mumbai-1</td>
		</tr>
		 <tr>
			<td>Mumbai Zone 2 (nodes in the Mumbai region cover South Asia Pacific) <br>ap-mumbai-2</td>
		   </tr>
		<tr>
		  	<td >Southeast Asia Pacific (Bangkok)<br>ap-bangkok </td>
				 <td>Bangkok Zone 1 (nodes in the Bangkok region cover Southeast Asia)<br>ap-bangkok-1</td>
		<tr>   
			<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (nodes in the Toronto region cover North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">Western US (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (nodes in the Silicon Valley region cover Western US)<br>na-siliconvalley-1</td>
		</tr>
          <tr>
			<td>Silicon Valley Zone 2 (nodes in the Silicon Valley region cover Western US)<br>na-siliconvalley-2</td>
		   </tr>
		<tr>
		<tr>
			<td rowspan="2">East US (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (nodes in the Virginia region cover Eastern US)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (nodes in the Virginia region cover East US) <br>na-ashburn-2</td>
		</tr>
			<tr>
			<td>Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (nodes in the Frankfurt region cover Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (nodes in the Moscow region cover Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## How to Select Regions and Availability Zones
When selecting a region and availability zone, you need to consider the following factors:
- The limits on where cloud disks can be mounted. A cloud disk can only be mounted to a CVM in the same availability zone.
- The geographic location of the CVM where you need to use the cloud disk, your location, and the locations of your target users. We recommend that, when purchasing cloud services, you select the geographic location that is closest to your clients in order to reduce access latency and increase the access speed.
- The relationship between the CVM where you need to use the cloud disk and other cloud products. We recommend that you select cloud products in the same region and availability zone so that each product can communicate with others through the private network, reducing access latency and increasing the access speed.
- Business high availability and disaster recovery considerations. In scenarios where only one VPC instance is available, we recommend that you at least deploy businesses in different availability zones to ensure fault isolation through cross-availability-zone disaster recovery.
- Communication between different availability zones can suffer from higher latency. This needs to be evaluated in conjunction with your actual business requirements to find the balance between high availability and low latency.

## Related Actions
Actions such as the use and viewing of cloud disks are zone- and region-specific. To easily migrate data and services to other regions or to build a cross-region disaster recovery system, you can copy snapshots to other regions. For more information, see [Cross-Region Snapshot Replication](https://intl.cloud.tencent.com/document/product/362/31623).
