A region is the physical location of an IDC. Availability zone (AZ) refers to the physical IDC of Tencent Cloud in the same region with independent power supplies and network resources. For more information, see [CVM - Regions and AZs](https://intl.cloud.tencent.com/document/product/213/6091).

## Supported Regions

### China
<table>
<thead>
<tr>
<th colspan="2">Region</th>
<th>Value</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="2">South China</td>
<td>Guangzhou</td>
<td>ap-guangzhou</td>
</tr>
<tr>
<td>Shenzhen</td>
<td>ap-shenzhen</td>
</tr>
<tr>
<td rowspan="3">East China</td>
<td>Shanghai</td>
<td>ap-shanghai</td>
</tr>
<tr>
<td>Nanjing</td>
<td>ap-nanjing</td>
</tr>
<tr>
<td>Hangzhou</td>
<td>ap-hangzhou</td>
</tr>
<tr>
<td rowspan="2">North China</td>
<td>Beijing</td>
<td>ap-beijing</td>
</tr>
<tr>
<td>Tianjin</td>
<td>ap-tianjin</td>
</tr>
<tr>
<td>Central China</td>
<td>Changshan</td>
<td>changsha</td>
</tr>
<tr>
<td rowspan="2">Southwest China</td>
<td>Chengdu</td>
<td>ap-chengdu</td>
</tr>
<tr>
<td>Chongqing</td>
<td>ap-chongqing</td>
</tr>
<tr>
<td rowspan="2">Hong Kong/Macao/Taiwan (China)</td>
<td>Taipei (China)</td>
<td>ap-taipei</td>
</tr>
<tr>
<td>Hong Kong (China)</td>
<td>ap-hongkong</td>
</tr>
</tbody></table>


### Other countries and regions	
<table>
<thead>
<tr>
<th colspan="2">Region</th>
<th>Value</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="3">Southeast Asia Pacific</td>
<td>Singapore</td>
<td>ap-singapore</td>
</tr>
<tr>
<td>Bangkok</td>
<td>ap-bangkok</td>
</tr>
<tr>
<td>Jakarta</td>
<td>ap-jakarta</td>
</tr>
<tr>
<td>South Asia Pacific</td>
<td>Mumbai</td>
<td>ap-mumbai</td>
</tr>
<tr>
<td rowspan="2">Northeast Asia Pacific</td>
<td>Seoul</td>
<td>ap-seoul</td>
</tr>
<tr>
<td>Tokyo</td>
<td>ap-tokyo</td>
</tr>
<tr>
<td>Western US</td>
<td>Silicon Valley</td>
<td>na-siliconvalley</td>
</tr>
<tr>
<td>Eastern US</td>
<td>Virginia</td>
<td>na-ashburn</td>
</tr>
<tr>
<td>North America</td>
<td>Toronto</td>
<td>na-toronto</td>
</tr>
<tr>
<td>South America</td>
<td>São Paulo</td>
<td>sa-saopaulo</td>
</tr>
<tr>
<td rowspan="2">Europe</td>
<td>Frankfurt</td>
<td>eu-frankfurt</td>
</tr>
<tr>
<td>Moscow</td>
<td>eu-moscow</td>
</tr>

</tbody></table>

## Region and AZ Selection

When selecting a region and AZ, take the following into consideration:

- The geographic locations of CKafka instances, your business, and your target users:
We recommend you choose the region closest to your end users when purchasing CKafka instances to minimize access latency and improve access speed.
- Relationship between CKafka and other Tencent Cloud services:
When you select other Tencent Cloud services, we recommend you try to locate them all in the same region and AZ to allow them to communicate with each other through the private network, reducing access latency and increasing access speed.
- High availability and disaster recovery.
Even if you have just one VPC, we still recommend you deploy your businesses in different AZs to prevent a single point of failure and enable cross-AZ disaster recovery.
- There may be network latency among different AZs. We recommend you assess your business requirements and find the optimal balance between high availability and low latency.
- If you need access to CKafka instances in other countries or regions, we recommend you select an instance in those other countries or regions. If you use a CKafka instance in [China](#MainlandChina) to access [servers in other countries and regions](#InternationalArea), you may encounter a high higher network latency.

## Resource Availability

The following table describes which CKafka resources are global, which are regional, and which are specific to AZs.

<table>
	<tr><th>Resource</th><th>Resource ID Format<br><Resource Abbreviation>-8-Digit String of Numbers and Letters</th><th>Type</th><th>Description</th></tr>
	<tbody>
	<tr>
	  <td>User Account</td>
	  <td>No limit</td>
	  <td>Globally unique</td>
	  <td>Users can use the same account to access Tencent Cloud resources from around the world.</td>
	</tr>
	<tr>
	<td>CKafka instance</td>
	  <td>ckafka-xxxxxxxx</td>
	  <td>Instances are specific to an AZ.</td>
	  <td>A CKafka instance created in an AZ is not available to other AZs.</td>
	</tr>
</table>

## Related Operations
### Migrating instance to another AZ
CKafka supports instance migration across AZs in the same region. If you need this, <a  href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for assistance.
