
TencentDB for Redis is available in various regions in and outside Mainland China. It can be deployed wherever CVM can be deployed.

## Network Descriptions
- Tencent Cloud services in the same region can communicate with one another over private networks.
- A CVM instance in a VPC can communicate with a TencentDB for Redis instance on a basic network in a different availability zone in the same region only after a subnet is configured and a VPC IP is assigned.
- Tencent Cloud services in different regions cannot communicate with one another over the private network. They can communicate over a VPC only after a peering connection is configured.
 > It is recommended to select the same region for the TencentDB for Redis instance as the CVM instance so as to reduce access latency.

## Regions and AZs
**Mainland China**

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
		<td rowspan="5">East China (Shanghai) <br>ap-shanghai</td>
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
		<td>Shanghai Zone 5 <br>ap-shanghai-5</td>
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
</tbody>
</table>	


**Outside Mainland China**

<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>AZ</th>
		</tr>
		<tr>
			<td rowspan="2">Southeast Asia (Hong Kong, China) <br>ap-hongkong</td>
			<td>Hong Kong Zone 1 (Nodes in Hong Kong, China can be used to provide services to users in Southeast Asia) <br>ap-hongkong-1</td>
		</tr>
<tr>
			<td>Hong Kong Zone 2 (Nodes in Hong Kong, China can be used to provide services to users in Southeast Asia) <br>ap-hongkong-2</td>
		   </tr>
		<tr>
			<td>Southeast Asia (Singapore) <br>ap-singapore</td>
			<td>Singapore Zone 1 (Nodes in Singapore can be used to provide services to users in Southeast Asia) <br>ap-singapore-1</td>
		</tr>
		<tr>
			<td >Asia Pacific (Seoul) <br>ap-seoul</td>
			<td>Seoul Zone 1 (Nodes in Seoul can be used to provide services to users in Northeast Asia) <br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >Asia Pacific (Tokyo) <br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Nodes in Tokyo can be used to provide services to users in Northeast Asia) <br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td >Asia Pacific (Mumbai) <br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Nodes in Mumbai can be used to provide services to users in South Pacific Asia) <br>ap-mumbai-1</td>
		</tr>
		<tr>
		  	<td >Asia Pacific (Bangkok) <br>ap-bangkok </td>
				 <td >Bangkok Zone 1 (Nodes in Bangkok can be used to provide services to users in Southeast Asia Pacific) <br>ap-bangkok-1</td>
		<tr>
			<td>North America (Toronto) <br>na-toronto</td>
			<td>Toronto Zone 1 (Nodes in Toronto can be used to provide services to users in North America) <br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">West US (Silicon Valley) <br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Nodes in Silicon Valley can be used to provide services to users in West US) <br>na-siliconvalley-1</td>
		</tr>
			<tr>
			<td>Silicon Valley Zone 2 (Nodes in Silicon Valley can be used to provide services to users in West US) <br>na-siliconvalley-2</td>
	</tr> 
		<tr>
		<tr>
			<td>East US (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (Nodes in Virginia can be used to provide services to users in East US) <br>na-ashburn-1</td>
		</tr>
			<td>Europe (Frankfurt) <br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Nodes in Frankfurt can be used to provide services to users in Europe) <br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow) <br>eu-moscow</td>
		<td>Moscow Zone 1 (Nodes in Moscow can be used to provide services to users in Europe) <br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>
