## Region

### Overview

A region is the physical location of an IDC. In Tencent Cloud, regions are fully isolated from each other, ensuring cross-region stability and fault tolerance. We recommend that you choose the region closest to your end users to minimize access latency and improve access speed.

The following table describes the regions, availability zones, and resource types that are currently supported by TKE Serverless Cluster.

### Characteristics

- The networks of different regions are fully isolated. Tencent Cloud services in different regions **cannot communicate via a private network by default**.
- Tencent Cloud services across regions can communicate with each other through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224) over the Internet, while those in different VPCs can communicate with each other through [CCN](https://intl.cloud.tencent.com/document/product/1003), which is faster and more stable.
- [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214) currently supports intra-region traffic forwarding by default. If you enable the [cross-region binding](https://intl.cloud.tencent.com/document/product/214/38441) feature, cross-region binding of CLB and CVM instances is supported.

## Availability Zone

### Overview

An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network in the same region. Business stability can be ensured because failures (except for major disasters or power failures) in one AZ do not affect other AZs in the same region. By starting an instance in an independent availability zone, users can protect their applications from a single point of failure.
You can view the following table or use the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API to get a complete AZ list.

### Characteristics

Tencent Cloud services in the same VPC are interconnected via the private network, which means they can communicate using [private IPs](https://intl.cloud.tencent.com/document/product/213/5225), even if they are in different AZs in the same region.
>? Private network interconnection refers to the interconnection of resources under the same account. Resources under different accounts are completely isolated on the private network.
>


## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
	</tr>
	<tr>
		<td rowspan="3">South China (Guangzhou)<br>ap-guangzhou</td>
		<td>Guangzhou Zone 3<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 4</br>ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 6<br>ap-guangzhou-6</td>
	</tr>
	<tr>
		<td rowspan="4">East China (Shanghai)<br>ap-shanghai</td>
		<td>Shanghai Zone 2</br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3</br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Shanghai Zone 4</br>ap-shanghai-4</td>
	</tr>
 <tr>
		<td>Shanghai Zone 5<br>ap-shanghai-5</td>
	</tr>
	<tr>
		<tr>
			<td rowspan="2">East China (Nanjing)<br>ap-nanjing</td>
			<td>Nanjing Zone 1<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>Nanjing Zone 2<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="5">North China (Beijing)<br>ap-beijing</td>
			<td>Beijing Zone 3</br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>Beijing Zone 4</br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>Beijing Zone 5<br>ap-beijing-5</td>
	</tr>
	<tr>
			<td>Beijing Zone 6<br>ap-beijing-6</td>
	</tr>
	<tr>
			<td>Beijing Zone 7</br>ap-beijing-7</td>
	</tr>
	<tr>
	<tr>
		<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
		<td>Chengdu Zone 1<br>ap-chengdu-1</td>
	</tr>
	<tr>
		<td>Chengdu Zone 2</br>ap-chengdu-2</td>
	</tr>    
	<tr>
		<td rowspan="1">Hong Kong, Macao and Taiwan, China (Hong Kong)<br>ap-hongkong</td>
		<td>Hong Kong Zone 2 (Nodes in Hong Kong, China can cover services in Hong Kong/Macao/Taiwan regions)<br>ap-hongkong-2</td>
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
			<td>Singapore Zone 1 (Singapore nodes can cover services in Southeast Asia)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Singapore Zone 2 (Singapore nodes can cover services in Southeast Asia)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>Southeast Asia (Jakarta)<br>ap-jakarta</td>
			<td>Jakarta Zone 1 (Jakarta nodes can cover services in Southeast Asia)<br>ap-jakarta-1</td>
		</tr>
		<tr>
			<td  rowspan="2">Northeast Asia (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul nodes can cover services in Northeast Asia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Seoul Zone 2 (Seoul nodes can cover services in Northeast Asia)<br>ap-seoul-2</td>
		</tr>
		<tr>
			<td rowspan="1">Northeast Asia (Tokyo)<br>ap-tokyo</td>
        	<td>Tokyo Zone 2 (Tokyo nodes can cover services in Northeast Asia)<br>ap-tokyo-2</td>
		</tr>
       <tr>
			<td  rowspan="2">South Asia (Mumbai) <br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes can cover services in South Asia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Mumbai nodes can cover services in South Asia) <br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td rowspan="1">Southeast Asia (Bangkok)<br>ap-bangkok </td>
			<td>Bangkok Zone 1 (Bangkok nodes can cover services in Southeast Asia)<br>ap-bangkok-1</td>
        </tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Toronto nodes can cover services in North America)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">Eastern US (Virginia) <br>na-ashburn</td>
			<td>Virginia Zone 1 (Virginia nodes can cover services in Eastern US)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Virginia nodes can cover services in Eastern US)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td rowspan="1">Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes can cover services in Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes can cover services in Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>
