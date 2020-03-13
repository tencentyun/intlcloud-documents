Data centers hosted by Tencent Cloud are distributed at multiple locations around the globe. The locations of these nodes are referred to as regions, and each region comprises multiple availability zones.
When creating a VPC, you need to select a region. When creating a subnet, you need to select an availability zone, and subnets must be in the region where the VPC resides. Understanding basic information regarding regions and availability zones helps you better deploy resources in the cloud.

## Regions
Tencent Cloud regions are named after the rule of **coverage range + city where the data center is located**, for example, South China (Guangzhou), East China (Shanghai), and Asia Pacific (Seoul). The coverage range indicates the coverage of the data center. The city indicates the city where the data center is located or the closest city. For the list of regions, see the [List of Tencent Cloud regions and availability zones] (#liebiao).
**Region features:**
- A VPC has the region attribute, and each VPC belongs to only one region.
- Whether in the same region or different regions, different VPC instances are isolated from each other and cannot directly communicate through the private network. If communication between VPC instances is needed, you can use [CCN](https://intl.cloud.tencent.com/document/product/1003) or [peering connections](https://intl.cloud.tencent.com/document/product/553).

## Availability Zones
Availability zones refer to Tencent Cloud’s physical data centers with power facilities and networks that are independent of each other within the same region. Each region has at least one availability zone. In the following example, four availability zones exist in the Guangzhou region.
Establishing multiple availability zones in one region is a way to implement failure isolation between availability zones (with the exception of large-scale disasters or large-scale power outages) so that failures do not spread and users’ businesses are not interrupted.
![](https://main.qcloudimg.com/raw/d08b5c6929deea1470b5fddd217d880f.png)
**Availability zone features:**
- A subnet of a VPC is associated with an availability zone, and one VPC can concurrently host subnets in different availability zones (for example, the VPC in the Guangzhou region can host subnets in Zone 1, Zone 2, Zone 3, and Zone 4 of the Guangzhou region.)
- Cloud products in the same region and same VPC can interconnect with each other even if they are in different availability zones. For example, subnets in different availability zones of the VPC in the Guangzhou region can directly interconnect with each other through the private network via private IP addresses.
- Resources of different accounts are completely isolated from each other on private networks. You must establish cross-account peering connections to achieve the interconnection of these resources.

## Choosing Regions and Availability Zones
When choosing regions and availability zones, you must take the following into consideration:
- The region of the CVM and the geographical locations of you and your target users: we recommend that you select the region closest to your end users to reduce access latency and increase the access speed.
- Relationships between the CVM and other cloud products: we recommend that the selected cloud products reside in the same availability zone of the same region to facilitate interconnection through private networks and to reduce access latency and increase the access speed.
- High availability of services and disaster recovery concerns: even in scenarios with a single VPC, we recommend that you deploy services in different availability zones to guarantee failure isolation between availability zones and to achieve cross-zone disaster recovery.
- Network communication delay may occur between availability zones, and therefore it is necessary to make an assessment based on the actual requirements of services to figure out the optimal balance point between high availability and low latency.

## Migrating an Instance to Another Availability Zone
You cannot change the availability zone of an instance that has been launched, but can migrate the instance to another availability zone and keep the current private IP address. The detailed process is as follows:
- Create a custom image from the original instance.
- Use the custom image to launch an instance in the target availability zone.
- Update the configuration of the new instance.

For more detailed steps, see [Migrating an Instance to Another Availability Zone](https://intl.cloud.tencent.com/document/product/213/6091).

<span id='liebiao'></span>
## List of Tencent Cloud Regions and Availability Zones
### China
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
		<td rowspan="2">South China (Shenzhen Finance)<br>ap-shenzhen-fsi</td>
		<td>Shenzhen Finance Zone 1<span style="background-color: rgb(249, 249, 249);">(only for financial institutions and enterprises, and you must submit <a href="https://console.cloud.tencent.com/workorder/category">a ticket to apply for</a> activation)<br>ap-shenzhen-fsi-1</span></td>
	</tr>
	<tr>
		<td>Shenzhen Finance Zone 2<span style="background-color: rgb(249, 249, 249);">(only for financial institutions and enterprises, and you must submit <a href="https://console.cloud.tencent.com/workorder/category">a ticket to apply for</a> activation)<br>ap-shenzhen-fsi-2</span></td>
	</tr>
<tr>
		<td>Shenzhen Finance Zone 3<span style="background-color: rgb(249, 249, 249);">(only for financial institutions and enterprises, and you must submit <a href="https://console.cloud.tencent.com/workorder/category">a ticket to apply for</a> activation)<br>ap-shenzhen-fsi-2</span></td>
	</tr>
	<tr>
		<td rowspan=“4”>East China (Shanghai)<br>ap-shanghai</td>
		<td>Shanghai Zone 1<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>Shanghai Zone 2<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3<br>ap-shanghai-4</td>
	</tr>
	<tr>
			<td rowspan=“3”>East China (Shanghai Finance)<br>ap-shanghai-fsi</td>
		<td>Shanghai Finance Zone 1 (only for financial institutions and enterprises, and you must submit <a href="https://console.cloud.tencent.com/workorder/category">a ticket to apply for</a> activation)<br>ap-shanghai-fsi-1</td>
	</tr>
	<tr>
			<td>Shanghai Finance Zone 2 (only for financial institutions and enterprises, and you must submit <a href="https://console.cloud.tencent.com/workorder/category">a ticket to apply for</a> activation)<br>ap-shanghai-fsi-2</td>
	</tr>
<tr>
			<td>Shanghai Finance Zone 3 (only for financial institutions and enterprises, and you must submit <a href="https://console.cloud.tencent.com/workorder/category">a ticket to apply for</a> activation)<br>ap-shanghai-fsi-2</td>
	</tr>
<tr>
			<td rowspan="2">East China (Nanjing)<br>ap-nanjing</td>
			<td>Nanjing Zone 1<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>Nanjing Zone 2<br>ap-nanjing-2</td>
	</tr>
	<tr>
	<tr>
			<td rowspan="3">North China (Beijing)<br>ap-beijing</td>
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
			<td >Southwest China (Chongqing)<br>ap-chongqing</td>
			<td>Chongqing Zone 1<br>ap-chongqing-1</td>
	</tr>
			<tr>
			<td rowspan="2">Hong Kong (China), Macao (China), and Taiwan (China) (Hong Kong, China) <br>ap-hongkong</td>
			<td>Hong Kong (China) Zone 1 (nodes in the Hong Kong (China) region can be used to cover Hong Kong (China), Macao (China), and Taiwan (China))<br>ap-hongkong-1</td>
		</tr>
	<tr>
			<td>Hong Kong (China) Zone 2 (nodes in the Hong Kong (China) region can be used to cover Hong Kong (China), Macao (China), and Taiwan (China))<br>ap-hongkong-2</td>
		   </tr>
</tbody>
</table>	

### Other Regions	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>Availability Zone</th>
		</tr>
		<tr>
			<td>Southeast Asia Pacific (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Singapore nodes can be used to cover Southeast Asia Pacific)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td >Northeast Asia Pacific (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul nodes can be used to cover Northeast Asia Pacific)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >Northeast Asia Pacific (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Tokyo nodes can be used to cover Northeast Asia Pacific)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td >Southern Asia Pacific (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes can be used to cover Southern Asia Pacific)<br>ap-mumbai-1</td>
		</tr>
		<tr>
		  	<td >Southeast Asia Pacific (Bangkok)<br>ap-bangkok </td>
				 <td >Bangkok Zone 1 (Bangkok nodes can be used to cover Southeast Asia Pacific)<br>ap-bangkok-1</td>
		<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Toronto nodes can be used to cover North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">Western US (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley nodes can be used to cover Western US)<br>na-siliconvalley-1</td>
		</tr>
          <tr>
			<td>Silicon Valley Zone 2 (Silicon Valley nodes can be used to cover Western US)<br>na-siliconvalley-2</td>
		   </tr>
		<tr>
		<tr>
			<td>Eastern US (Virginia)<br>na-ashburn</td>
			<td>Virginia Zone 1 (Virginia nodes can be used to cover Eastern US)<br>na-ashburn-1</td>
		</tr>
			<td>Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes can be used to cover Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes can be used to cover Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>
