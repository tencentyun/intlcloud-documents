TencentDB data centers are hosted in multiple locations world wide. These locations are known as regions. Each region contains multiple availability zones (AZs).
Each region is an independent geographic area containing multiple isolated AZs. Separate AZs in the same region are connected via low-latency private networks. Tencent Cloud provides you with the ability to distribute Tencent Cloud resources across different locations. We recommend placing resources in different AZs to eliminate single points of failure which may lead to service unavailability.

Region name and AZ name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:
- A region name is composed of **region + city**. The `region` indicates the geographic area that the data center covers, while the `city` represents the city in or near which the data center is located.
- An AZ name is in the format of **city + number**.


## Regions
Tencent Cloud regions are completely isolated. This guarantees the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Private Network Communication:
- Tencent Cloud resources within the same region (under the same account in the same VPC) can communicate with each other over a private network. They can be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- The networks of different regions are fully isolated. Tencent Cloud services in different regions cannot communicate over a private network by default.
- Tencent Cloud services in different regions can communicate with each other by accessing the Internet through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224). Tencent Cloud services in different VPCs can communicate with each other through [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003), which is faster and more stable.
- [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214) does not support cross-region traffic forwarding.


## Availability Zones
Availability zones (AZs) refer to Tencent Cloud IDCs with independent power supply and network in a region. They are designed to ensure that failures within one AZ can be isolated from other AZs, thereby ensuring service availability and business stability, excepting the occurrences of large-scale disasters or major power failures. Users can protect their applications from being affected by a single point of failure by deploying instances in independent AZs.
When launching an instance, you can select any AZ in the specified region. For high reliability, you can adopt a cross-AZ deployment solution to ensure that the service remains available when an instance in a single location fails. Examples of such solutions include [CLB](https://intl.cloud.tencent.com/document/product/214) and [EIP](https://intl.cloud.tencent.com/document/product/213/5733).

## List of Regions and AZs
Region and Availability Zones:
>?Currently, public network access is supported in the following regions:
>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Seoul, Tokyo, Silicon Valley, and Frankfurt.  

### China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>AZ</th>
	</tr>
	<tr>
		<td rowspan="5">South China (Guangzhou)<br>ap-guangzhou</td>
		<td>Guangzhou Zone 1 (sold out)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Guangzhou Zone 2<br> ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 3<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 4<br>ap-guangzhou-4</td>
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
			<td rowspan="2">East China (Nanjing)<br>ap-nanjing</td>
		<td>Nanjing Zone 1<br>ap-nanjing-1</td>
	</tr>
	<tr>
		<td>Nanjing Zone 2<br>ap-nanjing-2</td>
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
			<td>Southwest China (Chongqing)<br>ap-chongqing</td>
			<td>Chongqing Zone 1<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">Hong Kong, Macao and Taiwan, China (Hong Kong)<br>ap-hongkong</td>
			<td>Hong Kong Zone 1 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Hong Kong Zone 2 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>

### Other countries/regions
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>AZ</th>
		</tr>
		<tr>
			<td>Southeast Asia (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-1</td>
		</tr>
		<tr>
				<td>Singapore Zone 2 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-2</td>
	</tr>
				<tr>
		  	<td>Southeast Asia (Bangkok)<br>ap-bangkok </td>
				 <td>Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td>
		       <tr>
			<td  rowspan="2">South Asia (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes can cover services in South Asia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Mumbai nodes can cover services in South Asia) <br>ap-mumbai-2</td>
		</tr>		
		<tr>
			<td rowspan="2">Northeast Asia (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul nodes can cover services in Northeast Asia)<br>ap-seoul-1</td>
		</tr>
		<tr>
				<td>Seoul Zone 2 (Seoul nodes can cover services in Northeast Asia)<br>ap-seoul-2</td>
	</tr>
		<tr>
			<td>Northeast Asia (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Tokyo nodes can cover services in Northeast Asia)<br>ap-tokyo-1</td>
		</tr>
				<tr>
			<td rowspan="2">Western US (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in Western US) <br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Silicon Valley nodes cover services in Western US) <br>na-siliconvalley-2</td>
		</tr>
				<tr>
			<td rowspan="2">Eastern US (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (Virginia nodes can cover services in Eastern US)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Virginia nodes can cover services in Eastern US)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Tokyo nodes can cover services in North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td>Europe (Frankfurt) <br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes can cover services in Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td>Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes can cover services in Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>


## Selecting Regions and AZs
When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.
