## February 2022
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Added support for creating IP ranges with a minimum mask of "/12" bits for VPCs</td> 
<td>The minimum mask of the VPC IP ranges beginning with 10 and 172 is changed from "/16" to "/12" bits to support the creation of a larger range of CIDR blocks to meet network requirements such as scaling.</td> 
<td>2022-02</td> 
<td>
<a href="https://intl.cloud.tencent.com/document/product/215/535">Overview</a>
</td> 
</tbody>
</table>



## December 2021
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Launched snapshot backup and rollback features for security groups</td> 
<td>Snapshot policies can be configured for a security group to back up its inbound and outbound rules, and rule comparison, preview, and quick rollback are supported.</td> 
<td>2021-12</td> 
<td>
<ul><li><a href="https://intl.cloud.tencent.com/document/product/215/46787">Snapshot Policy</a></li><li><a href="https://intl.cloud.tencent.com/document/product/215/47910">Snapshot Rollback</a></li><ul>
</td> 
</tbody>
</table>


## August 2021
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Opened the secondary CIDR block feature to all users</td> 
<td>The secondary CIDR block feature is opened to all users. You can directly edit secondary CIDR blocks in the VPC console with no need to apply for additional permissions.</td> 
<td>2021-08</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/215/40070">Editing IPv4 CIDR Blocks</a></td> 
</tbody>
</table>



## November 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Increased the quotas</td>
<td>Quotas of the following resource items are increased:<ul><li>The number of VPCs per account per region is adjusted to 20.</li><li>The number of subnets per VPC is adjusted to 100.</li><li>The number of secondary ENIs per VPC is adjusted to 1,000.</li></ul>
</td>
<td>November 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/38959">Quota Limit</a></td>
</tr>
</tbody></table>

## December 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for displaying the last modified time of security group rules</td>
<td>The `Last Modified Time` attribute is added for each security group rule, which records the creation time or last modified time for easier troubleshooting.</td>
<td>2019-12</td>
<td>-</td>
</tr>
</tbody></table>

## November 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Opened HAVIP to all users</td>
<td>A high-availability virtual IP (HAVIP) is a floating private IP address that supports binding to a server by using ARP announcement to update the mapping between the IP address and MAC address. In a high-availability deployment use case (such as keepalived), this IP address can be switched from the primary server to the secondary server for business disaster recovery.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31817" target="_blank">Use cases</a></td>
</tr>
<tr>
<td>Added support for adding IPv6 rules to security groups</td>
<td>By adding IPv6 rules to a security group, you can allow or reject traffic to and from public or private networks for IPv6 CVM instances in a security group.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35513" target="_blank">Adding a Security Group Rule</a></td>
</tr>
</tbody></table>

## July 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for tags for VPCs</td>
<td>VPCs, subnets, and route tables support resource-level tags, which can help you better manage resource permissions for sub-users and collaborators.</td>
<td>2019-07</td>
<td>-</td>
</tr>
</tbody></table>

## December 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Launched the instance port verification feature</td>
<td>The instance port verification feature can help you check the accessibility of security group ports of CVM instances and quickly locate faults, improving user experience.</td>
<td>2018-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31875" target="_blank">Instance Port Verification </a></td>
</tr>
</tbody></table>

## October 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for quickly opening common ports in a security group</td>
<td>This operation is applicable to scenarios in which ICMP protocol rules do not need to be set and operations can be completed through ports 22, 3389, ICMP, 80, 443, 20, and 21.</td>
<td>2018-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35513" target="_blank">Adding a Security Group Rule </a></td>
</tr>
</tbody></table>

## June 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for the DHCP option set</td>
<td>The Dynamic Host Configuration Protocol (DHCP) is a LAN network protocol that provides the standard for delivering configuration information to TCP/IP network servers. The CVM instances in Tencent Cloud VPCs support DHCP. You can configure the two parameters on the VPC details page. These settings will take effect for all CVM instances under that VPC.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31808" target="_blank">Modifying VPC DNS</a></td>
</tr>
<tr>
<td>Launched the network probe feature</td>
<td>The Tencent Cloud network probe service is used to monitor the quality of VPC connections, including latency, packet loss rate, and other key metrics. You can quickly locate problems by setting alarms and multidimensional monitoring via the network probe. You can also create a network probe object in a subnet to monitor the connection quality in real time, so as to improve the business stability.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35522" target="_blank">Network Probe</a></td>
</tr>
</tbody></table>

## February 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for binding a VPC-based TencentDB to a security group</td>
<td>Security groups can be bound to TencentDB instances. A security group is a stateful virtual firewall that provides data packet filtering. It can be used to set network access control for CVM instances, ENIs, and TencentDB instances in VPCs, thereby effectively enhancing the security of TencentDB.</td>
<td>2018-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/34832" target="_blank">Associating CVM Instances with Security Groups</a></td>
</tr>
<tr>
<td>Added support for operation audit for VPCs and security groups</td>
<td>CloudAudit is supported for VPCs and security groups to get the history of API calls under your Tencent Cloud account, including those made through the Tencent Cloud console, Tencent Cloud SDKs, command line tools, and other Tencent Cloud services, to monitor any deployment behaviors in Tencent Cloud. You can find out the sub-users and collaborators who use Tencent Cloud APIs, the source IP addresses from which the APIs are called, and when they are called.</td>
<td>2018-02</td>
<td>-</td>
</tr>
</tbody></table>

## June 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for access control for security groups</td>
<td>You can manage the user permissions in a security group, which makes your services more secure.</td>
<td>2017-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35498" target="_blank">Cloud Access Management Overview</a></td>
</tr>
<tr>
<td>Added support for parameter templates for security groups</td>
<td>A parameter template is a set of parameters. You can save IP addresses and protocol ports as a template that can be directly imported when security group rules are added. Parameter templates, if properly used, can enhance your efficiency in using security groups.</td>
<td>2017-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31867" target="_blank">Parameter Template Management</a></td>
</tr>
<tr>
<td>Upgraded the monitoring feature</td>
<td>The visualized alarming and monitoring data of multiple key metrics and acquisition of monitoring data through APIs are supported to ensure the steady and smooth operation of your services.</td>
<td>2017-06</td>
<td>-</td>
</tr>
</tbody></table>

## May 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for access control for security groups</td>
<td>You can manage the user permissions in a security group, which makes your services more secure.</td>
<td>2017-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35498" target="_blank">Cloud Access Management Overview</a></td>
</tr>
</tbody></table>

## January 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for broadcast and multicast</td>
<td>Broadcast and multicast are one-to-many communication, which can help you save network bandwidth and reduce network load through efficient point-to-multipoint data transfer.<li>Broadcast: Tencent Cloud supports broadcast in the subnet dimension.</li><li>Multicast: Tencent Cloud supports multicast in the VPC dimension.</li></td>
<td>2017-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31809" target="_blank">Enabling or Disabling Broadcast</a></td>
</tr>
</tbody></table>

## October 2016
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for ENIs</td>
<td>The multi-ENI hot swapping service for CVM instances helps you achieve isolation among three networks and deployment of high-availability services.</td>
<td>2016-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35502" target="_blank">ENIs</a></td>
</tr>
</tbody></table>

## December 2015
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for network topology diagrams</td>
<td>A network topology diagram can clearly display your network architecture to help you easily tackle problems with network management.</td>
<td>2015-12</td>
<td>-</td>
</tr>
</tbody></table>

## May 2015
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="50%">Description</th>
<th width="5%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Launched VPC</td>
<td>A VPC is an independent isolated network space that supports software-defined networks, connection with your IDCs through VPN Connections or Direct Connect, and flexible deployment of hybrid cloud.</td>
<td>2015-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215" target="_blank">Virtual Private Cloud</a></td>
</tr>
</tbody></table>
