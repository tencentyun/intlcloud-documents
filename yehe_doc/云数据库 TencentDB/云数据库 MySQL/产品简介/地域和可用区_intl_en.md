TencentDB data centers are hosted in multiple locations worldwide. These locations are known as regions. Each region contains multiple availability zones (AZs).
Each region is an independent geographic area containing multiple isolated AZs. Separate AZs in the same region are connected via low-latency private networks. Tencent Cloud provides you with the ability to distribute Tencent Cloud resources across different locations. We recommend placing resources in different AZs to eliminate single points of failure which may lead to service unavailability.

Region name and AZ name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:
- A region name is composed of **region + city**. The `region` indicates the geographic area that the data center covers, while the `city` represents the city in or near which the data center is located.
- AZ names utilizes the format of **city + number**.


## Region
Tencent Cloud regions are completely isolated. This guarantees the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Private Network Communication:
- Tencent Cloud resources in different AZs within the same region can communicate with each other over private network. They can also be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- Tencent Cloud products in different regions **cannot communicate with each other over the private network by default**.
 - By default, CVM instances cannot communicate with each other over the private network across regions or access TencentDB or Cloud Memcached across regions.
 - When a CVM instance is bound to a CLB instance, only the instances in the same region can be selected.
- Tencent Cloud resources in different regions can be accessed over the Internet through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224). Tencent Cloud services in VPCs can communicate with each other over Tencent Cloud high-speed network via [peering connections](https://console.cloud.tencent.com/vpc/conn), which is more stable and faster than public Internet.
- [CLB](https://intl.cloud.tencent.com/document/product/214) does not support cross-region traffic forwarding.

The above notes regarding private network communication only applies to resources under the same account. Resources under different accounts are completely isolated.


## Availability Zone
Availability zones (AZs) refer to Tencent Cloud's physical data centers that are in the same region. Each AZ is independently powered and have its own network resources. They are designed to ensure that failures within one AZ can be isolated from other zones, thereby ensuring service availability and business stability, excepting the occurrences of large-scale disasters or major power failures. Users can protect their applications from being affected by failures that occur in a single location by selecting instances in independent AZs.
When launching an instance, you can select any AZ in the specified region. For high reliability, you can adopt a cross-AZ deployment solution to ensure that the service remains available when an instance in a single location fails. Examples of such solutions include [CLB](https://intl.cloud.tencent.com/document/product/214) and [EIP](https://intl.cloud.tencent.com/document/product/213/5733).

## List of Regions and AZs
Regions and AZs:

### China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
	</tr>
	<tr>
		<td rowspan="4">South China (Guangzhou) <br> ap-guangzhou</td>
		<td>Guangzhou Zone 1 (sold out)<br> ap-guangzhou-1</td>
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
			<td>Beijing Zone 4 <br>ap-beijing-4</td>
	</tr>
		<tr>
			<td>Beijing Zone 5 <br>ap-beijing-5</td>
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

### Other Countries/Regions
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>Availability Zone</th>
		</tr>
		<tr>
			<td>Southeast Asia (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-1</td>
		</tr>
				<tr>
		  	<td >Southeast Asia (Bangkok)<br>ap-bangkok </td>
				 <td >Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td>
		       <tr>
			<td  rowspan="2">South Asia (Mumbai) <br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Mumbai nodes cover services in South Asia) <br>ap-mumbai-2</td>
		</tr>		
		<tr>
			<td >Northeast Asia (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >Northeast Asia (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-1</td>
		</tr>
				<tr>
			<td rowspan="2">US West (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in US West) <br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Silicon Valley nodes cover services in US West) <br>na-siliconvalley-2</td>
		</tr>
				<tr>
			<td rowspan="2">US East (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (Virginia nodes cover services in US East)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Virginia nodes cover services in US East) <br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Toronto nodes cover services in North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td>Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes cover services in Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>


## Selecting Regions and AZs
When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.
