## Regions

### Overview

A region is the physical location of an IDC. Tencent Cloud regions are completely isolated. This guarantees the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud products, you are advised to select the region closest to your end users to minimize access latency and improve download speed.

You can view the following table or use the [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) API to view the complete list of regions.

### Related features

- The networks of different regions are fully isolated from each other, and Tencent Cloud products in different regions **cannot communicate with each other over the private network by default**.
- Tencent Cloud resources in different regions can be accessed over the Internet through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224). Tencent Cloud products in VPCs can communicate with each other over Tencent Cloud high-speed network via [Peering connections](https://intl.cloud.tencent.com/document/product/553), which is more stable and faster than public Internet.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) enables intra-region traffic forwarding (default setting) and supports the binding of CVMs in the same region. If the [CLB Instance Cross-Region Binding](https://intl.cloud.tencent.com/document/product/214/12014) feature is enabled, cross-region binding of load balancers and CVMs is supported.

## Availability Zone

### Overview

Availability zones (AZs) refer to Tencent Cloud's physical IDCs that are in the same region. Each AZ is independently powered and have its own network resources. They are designed to ensure that failures within 1 AZ can be isolated from other zones, thereby ensuring service availability and business stability, excepting the occurrences of large-scale disasters or major power failures. Users can protect their applications from being affected by failures that occur in a single location by selecting instances in independent AZs.
You can view the following table or use the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API to view the complete list of AZs.

### Related features

Tencent Cloud products in the same VPC are interconnected through a private network, meaning they can communicate using [private IPs](https://intl.cloud.tencent.com/document/product/213/5225), even if they are in different AZs within the same region.
> Private network interconnection refers to the interconnection of resources under the same account. Resources under different accounts are completely isolated on the private network.
>

<span id="MainlandChina"></span>
## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>AZ</th>
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
			<td rowspan="2">East China (Nanjing)<br>ap-nanjing</td>
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
	<tr>
			<td rowspan="2">Hong Kong/Macao/Taiwan (Hong Kong, China) <br>ap-hongkong</td>
			<td>Hong Kong Zone 1 (Hong Kong nodes cover services in Hong Kong/Macao/Taiwan) <br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Hong Kong Zone 2 (Hong Kong nodes cover services in Hong Kong/Macao/Taiwan) <br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>
## Other Countries and Regions	
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
			<td>Northeast Asia (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Northeast Asia (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">South Asia (Mumbai) <br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Mumbai nodes cover services in South Asia) <br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td>Southeast Asia (Bangkok)<br>ap-bangkok </td>
				 <td>Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td>
		<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Toronto nodes cover services in North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">US West (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in US West)<br>na-siliconvalley-1</td>
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
			<td>Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td>Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes cover services in Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## Selecting Regions and AZs

When selecting the region and AZ, consider the following factors:
- The region where the CVM is located, your location, and the location of your users.
When purchasing CVMs, you are advised to select the region closest to your end users to minimize access latency and improve download speed.
- The relationship between CVMs and other Tencent Cloud products.
When selecting other Tencent Cloud products, you are advised to put them all in the same region and AZ, so they can communicate with each other through the private network to minimize access latency and improve download speed.
- High availability and disaster recovery.
Even where there is only 1 VPC, we still recommend you deploying businesses in different availability zones (AZs) to ensure fault isolation between AZs and implement cross-AZ disaster recovery.
- Different AZs may have network communication delay, which needs to be assessed based on your actual business needs to find the optimal balance between high availability and low delay.
- If you need to access hosts in other countries or regions, we recommend you selecting and access CVMs in other countries or regions. If you create CVMs in [China](#MainlandChina) and access [hosts in other countries and regions](#InternationalArea), there will be high access delay. We do not recommend this.

## Resource Availability
The following table specifies which Tencent Cloud resources are global, which resources are regional but not specific to any AZs, and which resources are based on AZs.

<table>
	<tr><th>Resource</th><th>Resource ID Format<br><Resource Abbreviation>-8 Digits and Letters</th><th>Type</th><th>Description</th></tr>
	<tbody>
	<tr>
	  <td>User account</td>
	  <td>No limit</td>
	  <td>Globally unique</td>
	  <td>Users can use the same account to access Tencent Cloud resources from around the world.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH key</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>Globally available</td>
	  <td>Users can use the SSH key to bind a CVM in any regions under the account.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM instance</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>Available in only 1 AZ of a single region</td>
	  <td>Users can only create CVM instances in a specific AZ.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941">Custom image</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>Available in multiple AZs of a single region</td>
	  <td>Users can create a custom image for an instance, which can be used in different AZs of the same region. To use it in other regions, copy the custom image to other regions using the **Copy Image** feature.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>Available in multiple AZs of a single region</td>
	  <td>An EIP is created under a certain region, and can only be associated with instances in the same region.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security group</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>Available in multiple AZs of a single region</td>
	  <td>A security group is created under a certain region, and can only be associated with instances in the same region. Tencent Cloud automatically creates 3 default security groups for users.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">Cloud disk</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>Available in only 1 AZ of a single region</td>
	  <td>Users can only create a cloud disk in a specific AZ, and mount it on instances in the same AZ.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">Snapshot</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>Available in multiple AZs of a single region</td>
	  <td>After creating a snapshot for a specific cloud disk, users can use this snapshot for other operations (such as creating a cloud disk) in the same region.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>Available in multiple AZs of a single region</td>
	  <td>Cloud Load Balancer can be bound with CVMs in different AZs of a single region to implement traffic forwarding.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>Available in multiple AZs of a single region</td>
	  <td>A VPC is created under a certain region. Resources belonging to the same VPC can be created under different AZs.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">Subnet</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>Available in only 1 AZ of a single region</td>
	  <td>Users cannot create subnets across AZs.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/31810">Route table</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>Available in multiple AZs of a single region</td>
	  <td>When creating a route table, users need to specify a VPC, and therefore, the route table follows the region attribute of the VPC.</td>
	</tr>
	</tbody>
</table>


## Related Operations

### Migrating an instance to another AZ

Once launched, an instance cannot be migrated. However, you can create a custom image of your CVM instance and use the image to launch or update an instance in a different AZ.
1. Create a custom image for the current instance. For more information, see [Create Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
2. If the instance is on a [VPC](https://intl.cloud.tencent.com/document/product/213/5227) and you want to retain its current private IP address after the migration, first delete the subnet in the current AZ and then create a subnet in the new AZ with the same IP address range. Note that a subnet can be deleted only when it contains no available instances. Therefore, all the instances in the current subnet should be migrated to the new subnet.
3. Create a new instance in the new AZ by using the custom image you have just created. You can choose the same type and configuration as the original instance, or choose new settings. For more information, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).
4. If an EIP is associated with the original instance, dissociate it from the old instance and associate it with the new instance. For more information, see [EIP](https://intl.cloud.tencent.com/document/product/213/5733).
5. (Optional) If the original CVM instance is [pay-as-you-go](https://intl.cloud.tencent.com/document/product/213/2180), you can choose to terminate it. For more information, see [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).

### Copying images to other regions

Operations such as starting and viewing instances are region-specific. If the image you need to start an instance does not exist in the region, the image needs to be copied to the current region. For more information, see [Copy Images](https://intl.cloud.tencent.com/document/product/213/4943).
