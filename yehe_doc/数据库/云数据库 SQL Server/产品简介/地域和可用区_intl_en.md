## Region
### Overview
A region is the physical location of an IDC. In Tencent Cloud, regions are fully isolated from each other, ensuring cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.

### Characteristics
- The networks of different regions are fully isolated from each other, and Tencent Cloud services in different regions **cannot communicate using private networks by default**.
- Tencent Cloud services in different VPCs can communicate with each other over [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) which is fast and stable.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) currently supports intra-region traffic forwarding by default. If [cross-region binding](https://intl.cloud.tencent.com/document/product/214/38441) is enabled, cross-region binding of CLB and TencentDB instances is supported.

## AZ
### Overview
An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network in the same region. It can ensure business stability, as failures (except for major disasters or power failures) in one AZ are isolated without affecting other AZs in the same region. By starting an instance in an independent AZ, users can protect their applications from being affected by a single point of failure.

### Characteristics
Tencent Cloud services in the same VPC are interconnected over the private network, which means they can communicate using [private IPs](https://intl.cloud.tencent.com/document/product/213/5225), even if they are in different AZs of the same region.
>?Private network interconnection refers to the interconnection of resources under the same account. Resources under different accounts are completely isolated on the private network.

## China[](id:MainlandChina1)
<table class="table-striped">
<tbody><tr><th>Region</th><th>AZ</th></tr> 
<tr>
<td rowspan="6">South China (Guangzhou)<br>ap-guangzhou</td>
<td>Guangzhou Zone 1 (sold out)<br> ap-guangzhou-1</td></tr>	
<tr>
<td>Guangzhou Zone 2 (sold out)<br> ap-guangzhou-2</td></tr>
<tr>
<td>Guangzhou Zone 3<br> ap-guangzhou-3</td></tr>
<tr>
<td>Guangzhou Zone 4 (sold out)<br> ap-guangzhou-4</td></tr>
<tr>
<td>Guangzhou Zone 6<br> ap-guangzhou-6</td></tr>
<tr>
<td>Guangzhou Zone 7<br> ap-guangzhou-7</td></tr>
<tr>
<td rowspan="5">East China (Shanghai)<br>ap-shanghai</td>
<td>Shanghai Zone 1 (sold out)<br>ap-shanghai-1</td></tr>
<tr>
<td>Shanghai Zone 2<br>ap-shanghai-2</td></tr>
<tr>
<td>Shanghai Zone 3<br>ap-shanghai-3</td></tr>
<tr>
<td>Shanghai Zone 4<br>ap-shanghai-4</td></tr>
<tr>
<td>Shanghai Zone 5<br>ap-shanghai-5</td></tr>
<tr>
<td rowspan="2">East China (Nanjing)<br>ap-nanjing</td>
<td>Nanjing Zone 1<br>ap-nanjing-1</td></tr>
<tr>
<td>Nanjing Zone 2<br>ap-nanjing-2</td></tr>
<tr>
<td rowspan="7">North China (Beijing)<br>ap-beijing</td>
<td>Beijing Zone 1<br>ap-beijing-1</td></tr>
<tr>
<td>Beijing Zone 2<br>ap-beijing-2</td></tr>
<tr>
<td>Beijing Zone 3<br>ap-beijing-3</td></tr>
<tr>
<td>Beijing Zone 4<br>ap-beijing-4</td></tr>
<tr>
<td>Beijing Zone 5<br>ap-beijing-5</td></tr>
<tr>
<td>Beijing Zone 6<br>ap-beijing-6</td></tr>
<tr>
<td>Beijing Zone 7<br>ap-beijing-7</td></tr>
<tr>
<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
<td>Chengdu Zone 1<br>ap-chengdu-1</td></tr>
<tr>
<td>Chengdu Zone 2<br>ap-chengdu-2</td></tr>    
<tr>
<td >Southwest China (Chongqing)<br>ap-chongqing</td>
<td>Chongqing Zone 1<br>ap-chongqing-1</td></tr>
<tr>
<td rowspan="3">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
<td>Hong Kong Zone 1 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-1</td></tr>
<tr>
<td>Hong Kong Zone 2 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-2</td></tr></tr>
<tr>
<td>Hong Kong Zone 3 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-3</td></tr></tr>
</tbody></table>


## Other Countries and Regions[](id:InternationalArea1)
<table class="table-striped">
<tbody><tr><th>Region</th><th>AZ</th></tr>
<tr>
<td rowspan="2">Southeast Asia (Singapore)<br>ap-singapore</td>
<td>Singapore Zone 1 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-1</td></tr>
<tr>
<td>Singapore Zone 2 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-2</td></tr>
</tr>
<td>Southeast Asia (Jakarta)<br>ap-jakarta</td>
<td>Jakarta Zone 1 (Jakarta nodes cover services in Southeast Asia)<br>ap-jakarta-1</td></tr>
<tr>
<td rowspan="2">Southeast Asia (Bangkok)<br>ap-bangkok</td>
<td >Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td>
<tr>
<td >Bangkok Zone 2 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-2</td>
<tr>
<td>Northeast Asia (Seoul)<br>ap-seoul</td>
<td>Seoul Zone 1 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-1</td></tr>
<tr>
<td rowspan="2">Northeast Asia (Tokyo)<br>ap-tokyo</td>
<td>Tokyo Zone 1 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-1</td></tr>
<tr>
<td>Tokyo Zone 2 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-2</td></tr>
<tr>
<td rowspan="2">Western US (Silicon Valley)<br>na-siliconvalley</td>
<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-1</td></tr>
<tr>
<td>Silicon Valley Zone 2 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-2</td></tr>
<tr>
<td>Europe (Moscow)<br>eu-moscow</td>
<td>Moscow Zone 1 (Moscow nodes cover services in Europe)<br>eu-moscow-1</td></tr>
</tbody></table>
## Selection of Regions and AZs
- The geographic locations of TencentDB instances, your business, and your target users:
We recommend you choose the region closest to your end users when purchasing TencentDB instances to minimize access latency and improve access speed.
- Other Tencent Cloud services you use.
When you select other Tencent Cloud services, we recommend you try to locate them all in the same region and AZ to allow them to communicate with each other through the private network, reducing access latency and increasing access speed.
- High availability and disaster recovery.
Even if you have just one VPC, we still recommend you deploy your businesses in different AZs to prevent a single point of failure and enable cross-AZ disaster recovery.
- There may be network latency among different AZs. We recommend you assess your business requirements and find the optimal balance between high availability and low latency.
- If you need access to servers in other countries or regions, we recommend you select an instance in those other countries or regions. If you use a TencentDB instance in [China](#MainlandChina1) to access [servers in other countries and regions](#InternationalArea1), you may encounter a higher network latency.

## Resource Availability
The following table describes which resources are global, which are regional, and which are specific to AZs.

<table>
<tr><th width="14%">Resource</th><th>Resource ID Format<br><Resource Abbreviation>-8-Digit String of Numbers and Letters</th><th>Type</th><th>Description</th></tr>
<tbody>
<tr>
<td>User account</td>
<td>No limit</td>
<td>Globally unique</td>
<td>You can use the same account to access Tencent Cloud resources from around the world.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH key</a> </td>
<td>skey-xxxxxxxx</td>
<td>Global</td>
<td>You can use an SSH key to bind a CVM instance in any region under the account.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM instance</a> </td>
<td>ins-xxxxxxxx</td>
<td>AZ-specific</td>
<td>A CVM instance created in an AZ is not available in other AZs.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941">Custom image</a> </td>
<td>img-xxxxxxxx</td>
<td>Regional</td>
<td>Custom images created for the instance are available in all AZs in the same region. Use the image replication feature to copy a custom image if you need to use it in other regions.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
<td>eip-xxxxxxxx</td>
<td>Regional</td>
<td>EIPs are created in a region and can only be associated with instances in the same region.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security group</a> </td>
<td>sg-xxxxxxxx</td>
<td>Regional</td>
<td>A security group can only be associated with instances in the same region. Tencent Cloud automatically creates three default security groups for you.</td></tr>
<tr>
<td> <a href="https://cloud.tencent.com/document/product/362">Cloud disk</a> </td>
<td>disk-xxxxxxxx</td>
<td>AZ-specific</td>
<td>You can only create a CBS cloud disk in a specific AZ and mount it to instances in the same AZ.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">Snapshot</a> </td>
<td>snap-xxxxxxxx</td>
<td>Regional</td>
<td>A snapshot created from a cloud disk can be used for other purposes (such as creating cloud disks) in the same region.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">CLB instance</a> </td>
<td>clb-xxxxxxxx</td>
<td>Regional</td>
<td>CLB instances can be bound to CVM instances in different AZs in the same region for traffic forwarding.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
<td>vpc-xxxxxxxx</td>
<td>Regional</td>
<td>A VPC in one region can have resources created in different AZs in the region.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">Subnet</a> </td>
<td>subnet-xxxxxxxx</td>
<td>AZ-specific</td>
<td>You cannot create subnets across AZs.</td></tr>
<tr>
<td> <a href="https://intl.cloud.tencent.com/document/product/215/31810">Route table</a> </td>
<td>rtb-xxxxxxxx</td>
<td>Regional</td>
<td>When creating a route table, you need to specify a VPC. Therefore, route tables are regional as well.</td></tr>
</tbody></table>

## Related Operations
TencentDB for SQL Server supports cross-AZ instance migration. For more information, see [Migrating Across AZs](https://intl.cloud.tencent.com/document/product/238/42695).
