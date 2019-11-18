TencentDB has many managed data centers that are distributed in multiple locations around the world. The location of these nodes are called regions. Each region is made up of multiple availability zones.
Each region is an independent geographical region composed of multiple mutually isolated availability zones (AZs). Independent from each other, AZs in the same region are connected together through low-latency private network linkage. Tencent Cloud allows you to distribute Tencent Cloud resources across different locations. You are recommended to place resources in different AZs when designing your system, so as to eliminate single points of failure which may lead to service unavailability.

Region name and AZ name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:
- A region name is composed of **coverage + city**. The first part indicates the region that a data center can cover, while the second part represents the city in or near which the data center is located.
- An AZ name comes in the format of **city + number**.


## Region
Tencent Cloud services are completely isolated in different regions in order to guarantee the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud services, you are recommended to select the region closest to your end users so as to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Notes on communication between Tencent Cloud products over the private network:
- Even in different AZs, Tencent Cloud resources in the same region can be interconnected over the private network and directly accessed through [private IP][2].
- Tencent Cloud products in different regions **cannot communicate with each other over the private network by default**.
 - By default, CVM instances cannot communicate with each other over the private network across regions or access TencentDB or Cloud Memcached across regions.
 - When a CVM instance is bound to CLB, only the instances in the same region can be selected.
- Tencent Cloud resources in different regions can be accessed over the internet through [public IPs][3]. Tencent Cloud services in VPCs support communication over the high-speed network of Tencent Cloud through [peering connections][4], which is more stable and faster than internet access.
- [CLB][5] does not support cross-region traffic forwarding.

The interconnection over the private network above refers to the interconnection of resources under the same account, while the resources under different accounts are completely isolated.


## AZ
AZs refer to Tencent Cloud's physical IDCs in a region with independent power supply and network resources. They are designed to ensure that failures within an AZ can be isolated (except for major natural disasters or power failures) without spreading to and affecting other AZs, so as to ensure business stability and continuity. By starting an instance in an independent AZ, you can protect your applications from being affected by the failures occurring in one single location.
When launching an instance, you can select any AZ in the specified region. To design your application system with high reliability (i.e., services are still available even if an instance fails), you can adopt a cross-AZ deployment solution (such as [CLB][7] and [EIP][8]) where an instance in another AZ can be used to respond to requests in place of the failing one.

## List of Regions and AZs
Regions and AZs:

### China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>AZ</th>
	</tr>
	<tr>
		<td rowspan="4">South China (Guangzhou) <br> ap-guangzhou</td>
		<td>Guangzhou Zone 1 (sold-out)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Guangzhou Zone 2 <br>ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 3 <br>ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 4 <br>ap-guangzhou-4</td>
	</tr>
	<tr>
		<td rowspan="2">South China (Shenzhen Finance) <br>ap-shenzhen-fsi</td>
		<td>Shenzhen Finance Zone 1 <span style="background-color: rgb(249, 249, 249);">(only financial institutions and enterprises can apply for activation by <a href="https://console.cloud.tencent.com/workorder/category">submitting a ticket</a>)<br>ap-shenzhen-fsi-1</span></td>
	</tr>
	<tr>
		<td>Shenzhen Finance Zone 2 <span style="background-color: rgb(249, 249, 249);">(only financial institutions and enterprises can apply for activation by submitting a ticket)<br>ap-shenzhen-fsi-2</span></td>
	</tr>
	<tr>
		<td rowspan="4">East China (Shanghai) <br>ap-shanghai</td>
		<td>Shanghai Zone 1 <br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>Shanghai Zone 2 <br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3 <br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Shanghai Zone 4 <br>ap-shanghai-4</td>
	</tr>
	<tr>
			<td rowspan="3">East China (Shanghai Finance) <br>ap-shanghai-fsi</td>
			<td>Shanghai Finance Zone 1 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shanghai-fsi-1</td>
	</tr>
	<tr>
			<td>Shanghai Finance Zone 2 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shanghai-fsi-2</td>
	</tr>
	<tr>
			<td>Shanghai Finance Zone 3 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shanghai-fsi-3</td>
	</tr>
	<tr>
			<td rowspan="5">North China (Beijing) <br>ap-beijing</td>
			<td>Beijing Zone 1 <br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>Beijing Zone 2 <br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>Beijing Zone 3 <br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>Beijing Zone 4 <br>ap-beijing-4</td>
	</tr>
		<tr>
			<td>Beijing Zone 5 <br>ap-beijing-5</td>
	</tr>
		<tr>
			<td >North China (Beijing Finance) <br>ap-beijing-fsi</td>
			<td>Beijing Finance Zone 1 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-beijing-fsi-1</td>
	</tr>   
	<tr>
		<td rowspan="2">Southwest China (Chengdu) <br>ap-chengdu</td>
		<td>Chengdu Zone 1 <br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>Chengdu Zone 2 <br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >Southwest China (Chongqing) <br>ap-chongqing</td>
			<td>Chongqing Zone 1 <br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">Hong Kong, Macao, and Taiwan (Hong Kong, China) <br>ap-hongkong</td>
			<td>Hong Kong Zone 1 (Nodes in Hong Kong can be used to provide services to users in Hong Kong, Macao, and Taiwan) <br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Hong Kong Zone 2 (Nodes in Hong Kong can be used to provide services to users in Hong Kong, Macao, and Taiwan) <br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>
### Other Countries and Regions
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>AZ</th>
		</tr>
		<tr>
			<td>Southeast Asia Pacific (Singapore) <br>ap-singapore</td>
			<td>Singapore Zone 1 (Nodes in Singapore can be used to provide services to users in Southeast Asia Pacific) <br>ap-singapore-1</td>
		</tr>
				<tr>
		  	<td >Southeast Asia Pacific (Bangkok) <br>ap-bangkok </td>
				 <td >Bangkok Zone 1 (Nodes in Bangkok can be used to provide services to users in Southeast Asia Pacific) <br>ap-bangkok-1</td>
		       <tr>
			<td  rowspan="2">South Pacific Asia (Mumbai) <br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Nodes in Mumbai can be used to provide services to users in South Pacific Asia) <br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Nodes in Mumbai can be used to provide services to users in South Pacific Asia) <br>ap-mumbai-2</td>
		</tr>		
		<tr>
			<td >Northeast Asia Pacific (Seoul) <br>ap-seoul</td>
			<td>Seoul Zone 1 (Nodes in Seoul can be used to provide services to users in Northeast Asia Pacific) <br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >Northeast Asia Pacific (Tokyo) <br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Nodes in Tokyo can be used to provide services to users in Northeast Asia Pacific) <br>ap-tokyo-1</td>
		</tr>
				<tr>
			<td rowspan="2">West US (Silicon Valley) <br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Nodes in Silicon Valley can be used to provide services to users in West US) <br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Nodes in Silicon Valley can be used to provide services to users in West US) <br>na-siliconvalley-2</td>
		</tr>
				<tr>
			<td rowspan="2">East US (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (Nodes in Virginia can be used to provide services to users in East US) <br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Nodes in Virginia can be used to provide services to users in East US) <br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>North America (Toronto) <br>na-toronto</td>
			<td>Toronto Zone 1 (Nodes in Toronto can be used to provide services to users in North America) <br>na-toronto-1</td>
		</tr>
		<tr>
			<td>Europe (Frankfurt) <br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Nodes in Frankfurt can be used to provide services to users in Europe) <br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow) <br>eu-moscow</td>
		<td>Moscow Zone 1 (Nodes in Moscow can be used to provide services to users in Europe) <br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>


## How to Select Region and AZ
When purchasing Tencent Cloud services, you are recommended to select the region closest to your end users so as to minimize access latency and improve download speed.


[1]:	https://intl.cloud.tencent.com/doc/product/213/4943
[2]:	https://intl.cloud.tencent.com/doc/product/213/5225
[3]:	https://intl.cloud.tencent.com/doc/product/213/5224
[4]:	https://intl.cloud.tencent.com/doc/product/215/5000
[5]:	https://intl.cloud.tencent.com/doc/product/214
[7]:	https://intl.cloud.tencent.com/doc/product/214
[8]:	https://intl.cloud.tencent.com/doc/product/213/5733
