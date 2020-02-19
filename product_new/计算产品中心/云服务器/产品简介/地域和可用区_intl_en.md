## Region

### Overview

A region is the physical location of the IDC. In Tencent Cloud, different regions are fully isolated, ensuring the maximal stability and fault tolerance among those regions. To reduce access latency and increase download speeds, we recommend you select the region nearest to your customers.

You can view the following table or use the [DescribeRegions](http://intl.cloud.tencent.com/document/product/213/9456) API to view the complete list of regions.

### Related Features

- The networks of different regions are fully isolated from each other, and Tencent Cloud products of different regions **cannot communicate via private network by default**.
- Tencent Cloud products of different regions can access the Internet through [Public IP](http://intl.cloud.tencent.com/document/product/213/5224). Tencent Cloud products in VPCs can also communicate with each other by using [Peering Connection](http://intl.cloud.tencent.com/document/product/215/5000) provided by Tencent Cloud through Tencent Cloud’s high-speed connected network, to implement connectivity that is more stable and faster than Internet access.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) currently supports intra-region traffic forwarding, and binding of CVMs in the same region. If the [cross-region binding](http://intl.cloud.tencent.com/document/product/214/12014) function is enabled, then binding CVMs to the Cloud Load Balancer across regions is supported.

## Availability Zone

### Overview

Availability zones refer to Tencent Cloud physical IDCs in the same region with independent power and network resources. They are designed to ensure that the failures within an availability zone can be isolated (except for large-scale disaster or major power failure) without spreading to and affecting other zones, so as to ensure users' business stability. By starting an instance in an independent availability zone, users can protect their applications from being affected by failures that occur in a single location.
You can view the following table or use the [DescribeZones](http://intl.cloud.tencent.com/document/product/213/9455) API to view the complete list of availability zones.

### Related Features

Tencent Cloud products that are in the same region and different availability zones, but in the same VPC, are interconnected through private network. they can be accessed directly through the [private IP](http://intl.cloud.tencent.com/document/product/213/5225).
>Private network interconnection refers to the interconnection of resources under the same account. Private networks for resources under different accounts are completely isolated.

<span id="MainlandChina"></span>
## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
	</tr>
	<tr>
		<td rowspan="4">South China (Guangzhou) <br>ap-guangzhou</td>
		<td>Guangzhou Zone 1 (sold out)<br> ap-guangzhou-1</td>
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
    	<td rowspan="2">East China (Nanjing) <br>ap-nanjing</td>
    	<td>Nanjing Zone 1 <br>ap-nanjing-1</td>
    </tr>
    <tr>
    	<td>Nanjing Zone 2 <br>ap-nanjing-2</td>
    </tr>
    <tr>
    		<td rowspan="4">North China (Beijing) <br>ap-beijing</td>
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
    		<td rowspan="2">Hong Kong/Macao/Taiwan (Hong Kong, China) <br>ap-hongkong</td>
    		<td>Hong Kong Zone 1 (Nodes in Hong Kong, China can cover Hong Kong/Macao/Taiwan) <br>ap-hongkong-1</td>
    </tr>
    <tr>
    		<td>Hong Kong Zone 2 (Nodes in Hong Kong, China can cover Hong Kong/Macao/Taiwan) <br>ap-hongkong-2</td>
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
			<td>Southeast Asia Pacific (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Nodes in Singapore can cover Southeast Asia Pacific)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Northeast Asia Pacific (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Nodes in Seoul can cover Northeast Asia Pacific)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Northeast Asia Pacific (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Nodes in Tokyo can cover Northeast Asia Pacific)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">South Asia Pacific (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Nodes in Mumbai can cover South Asia Pacific) <br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Nodes in Mumbai can cover South Asia Pacific) <br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td>Southeast Asia Pacific (Bangkok)<br>ap-bangkok </td>
				 <td >Bangkok Zone 1 (Nodes in Bangkok cover Southeast Asia Pacific) <br>ap-bangkok-1</td>
		<tr>
			<td>North America (Toronto) <br>na-toronto</td>
			<td>Toronto Zone 1 (Nodes in Toronto can cover North America) <br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">West US (Silicon Valley) <br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Nodes in Silicon Valley can cover West US) <br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Nodes in Silicon Valley can cover West US) <br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">East US (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (Nodes in Virginia can cover East US) <br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Nodes in Virginia can cover East US) <br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>Europe (Frankfurt) <br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Nodes in Frankfurt can cover Europe) <br>eu-frankfurt-1</td>
		</tr>
		<td>Europe (Moscow) <br>eu-moscow</td>
		<td>Moscow Zone 1 (Nodes in Moscow can cover Europe) <br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## How to Select the Region and Availability Zone

When selecting the region and availability zone, you must take the following factors into consideration:
- The region where the CVM is located, your location, and the location of your users.
We recommend that when you purchase CVMs, you choose the region that is closest to your users to minimize the access latency and improve access speed.
- The relationship between CVMs and other Tencent Cloud products.
We recommend that when you select other Tencent Cloud products, you try to make them all in the same region and availability zone to allow them communicate with each other through the private network, reducing access latency and increasing access speeds.
- Considerations for high reliability and disaster recovery of businesses.
Even in a scenario where there is only one VPC, we still recommend that you deploy businesses in different availability zones to guarantee failure isolation between availability zones and to implement cross-AZ disaster recovery.
- There may be a network communication delay between different availability zones, so you need to make an assessment based on the actual requirements of the businesses to find the optimal balance point between high availability and low delay.
- If you need to access CVMs in other countries or regions, we recommend you select a CVM in other countries or regions for access. If you create a CVM in [Mainland China](#MainlandChina) and access [servers in other countries and regions](#InternationalArea) there will be relatively high access delay. We do not recommend you do this.

## Resource Location Description
The following table specifies which resources of Tencent Cloud are global, which resources are regional and not specific to any availability zone and which resources are based on availability zones.

<table>
	<tr><th>Resource</th><th>Resource ID format<br><Resource abbreviation>-8 digit numeric and alphabetic characters</th><th>Type</th><th>Description</th></tr>
	<tbody>
	<tr>
	  <td>User Account</td>
	  <td>No limit</td>
	  <td>Globally unique</td>
	  <td>Users can use the same account to access Tencent Cloud resources from around the world.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH Key</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>Globally available</td>
	  <td>Users can use the SSH key to bind a CVM in any region under the account.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM Instance</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>This can only be used under one availability zone in one region.</td>
	  <td>Users can only create CVM instances in a specific availability zones.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941#custom-images">Custom Images</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>Available in a single region and multiple availability zones</td>
	  <td>Users can create a custom image for instances, which can be used in different availability zones of the same region. Copy the custom image to other regions using the **Copy Image** feature to use it in those regions.</td>
	</tr>
	<tr>
	<td> <a href="http://intl.cloud.tencent.com/document/product/213/5733">Elastic IP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>Available in a single region and multiple availability zones</td>
	  <td>Elastic IP address is created under a certain region, and can only be associated with instances in the same region.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>Available in a single region and multiple availability zones</td>
	  <td>Security Group is created under a certain region, and can only be associated with instances in the same region. Tencent Cloud automatically creates three default security groups for users.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>This can only be used under one availability zone in one region.</td>
	  <td>Users can only create a Cloud Block Storage in a specific availability zone, and can mount it on instances in the same availability zone.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/2345">Snapshots</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>Available in a single region and multiple availability zones</td>
	  <td>After creating snapshot for a specific cloud disk, users can use this snapshot in this region for other operations (such as creating cloud disk).</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>Available in a single region and multiple availability zones</td>
	  <td>Cloud Load Balancer can be bound with CVMs in different availability zones in a single region for traffic forwarding.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>Available in a single region and multiple availability zones</td>
	  <td>A VPC is created under a certain region. You can create resources in different AZs but in the same VPC.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">Subnet</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>This can only be used under one availability zone in one region.</td>
	  <td>Users cannot create subnets across availability zones.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/4954">Route Table</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>Available in a single region and multiple availability zones</td>
	  <td>When creating a route table, users need to specify a specific VPC. Thus, the location attribute of the VPC should be followed.</td>
	</tr>
	</tbody>
</table>


## Related Operations

### Migrating an Instance to Another Availability Zone

For a launched instance, its availability zone cannot be changed. But you can migrate it to another availability zone through other means. The migration process involves creating a custom image using the original instance, using the custom image to launch an instance in a new availability zone and updating the configuration of the new instance.
1. Create a custom image for the current instance. For more information, see [Creating a Custom Image](http://intl.cloud.tencent.com/document/product/213/4942).
2. If the network environment of the current instance is [VPC](http://intl.cloud.tencent.com/document/product/213/5227) and the private IP address needs to be retained after the migration, you can first delete the subnet in the current availability zone and then create a subnet in the new availability zone with the same IP address range as that of the original subnet. Please note that a subnet can be deleted only when it contains no available instances. Thus, all the instances in the current subnet should be migrated to the new subnet.
3. Create a new instance in the new availability zone by using the custom image you have just created. You can choose the same type and configuration as those of the original instance, or choose new ones. For more information, see [Purchasing and Launching Instances](http://intl.cloud.tencent.com/document/product/213/4855).
4. If an Elastic IP is associated with the original instance, dissociate it from the old instance and associate it with the new instance. For more information, see [Elastic IP](http://intl.cloud.tencent.com/document/product/213/5733).
5. (Optional) If the original instance is billed on a [Pay-as-you-go](http://intl.cloud.tencent.com/document/product/213/2180) basis, then you can choose to terminate the original instance. For more information, see [Terminating Instances](http://intl.cloud.tencent.com/document/product/213/4930).

### Copying Images to Other Regions

Actions such as launching and viewing instances have region attributes. If the image of the instance that you need to launch does not exist in the region, the image needs to be copied to the current region. For more information, see [Copying Images](http://intl.cloud.tencent.com/document/product/213/4943).
