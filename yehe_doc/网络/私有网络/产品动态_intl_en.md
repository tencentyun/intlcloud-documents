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
<td>Increases quotas</td>
<td>The quotas of the following resources are increased:<ul><li>The number of VPC instances per region for each account is adjusted to 20</li><li>The number of subnets per VPC is adjusted to 100</li><li>The number of secondary ENI per VPC is adjusted to 1,000</li></ul>
</td>
<td>2020-11</td>
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
<td>Supports display the last modification time of security group rules</td>
<td>Each security group rule shows the “Last Modification Time” field, which will record the last time of creation or modification and facilitate troubleshooting.</td>
<td>2019-12</td>
<td>—</td>
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
<td>Launches HAVIP to all users</td>
<td>A high availability virtual IP (HAVIP) is a floating private IP address that supports binding to a server through ARP announcement and updates IP to mac mappings. In a high availability deployment scenario (such as Keepalived), HAVIP can be switched from a primary server to secondary server for disaster recovery of the service.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31817" target="_blank">Overview</a></td>
</tr>
<tr>
<td>Security groups supports adding IPv6 rules</td>
<td>This allows you to enable or disable public or private network access of IPv6 CVM instances in a security group.</td>
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
<td>VPC supports tags</td>
<td>This allows you to add resource-level tags to VPCs, subnets, and route tables, which provides better permission controls of sub-users and collaborators.</td>
<td>2019-07</td>
<td>—</td>
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
<td>Activates instance port verification tool</td>
<td>The instance port verification feature can help you check the accessibility of security group ports of CVM instances and quickly locate faults, improving user experience.</td>
<td>2018-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31875" target="_blank">Instance Port Verification</a></td>
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
<td>Supports opening all ports in a security group</td>
<td>Opening all ports is ideal if you do not need custom ICMP rules and all traffic goes through ports 20, 21, 22, 80, 443, and 3389 and the ICMP protocol.</td>
<td>2018-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35513" target="_blank">Adding a Security Group Rule</a></td>
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
<td>Supports DHCP option set</td>
<td>The Dynamic Host Configuration Protocol (DHCP) is a standard LAN network protocol that specifies how to deliver configurations to TCP/IP network servers. The CVMs in Tencent Cloud VPCs support DHCP, which can be configured on the VPC details page. These configurations will take effect for all CVMs in that VPC.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31808" target="_blank">Modifying DNS Addresses and Domain Names</a></td>
</tr>
<tr>
<td>Adds network probe feature</td>
<td>The Tencent Cloud network probe service is used to monitor the quality of VPC network connections, including latency, packet loss rate, and other key metrics. You can use network probe to set alerts and multi-dimensional monitoring to facilitate your troubleshooting. To monitor the network quality of connections in real time, you can create a network probe in the subnet to improve your service stability.</td>
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
<td>Supports binding a VPC-based TencentDB to a security group</td>
<td>Security groups can be bound with TencentDB and other relevant products. A security group is a virtual firewall that features stateful data packet filtering. It can be used to configure the network access control of instances such as CVMs and ENIs, and also TencentDB instances in VPCs. Therefore, a security group can effectively enhance the security of TencentDB.</td>
<td>2018-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/34832" target="_blank">Associating CVM Instances with Security Groups</a></td>
</tr>
<tr>
<td>VPCs and security groups supports operation audit</td>
<td>VPCs and security groups now support CloudAudit, which will retrieve the historical records of API calls under your Tencent Cloud account, including API calling via the Tencent Cloud console, Tencent Cloud SDK, command line tool, and other Tencent Cloud services. This means that any deployment behavior on Tencent Cloud is monitored, and you can find out the source IP address and time when a sub-user or collaborator calls an Tencent Cloud API.</td>
<td>2018-02</td>
<td>—</td>
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
<td>Security groups supports access control</td>
<td>The security group now provides the permission control feature to make your service more secure.</td>
<td>2017-06</td>
<td>Access Control Overview</td>
</tr>
<tr>
<td>Security groups supports the parameter template configuration</td>
<td>A parameter template is a set of parameters. You can save IP addresses and protocol ports as a template that you can use to add security group rules. This improves your efficiency in using security groups.</td>
<td>2017-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31867" target="_blank">Parameter Template Management</a></td>
</tr>
<tr>
<td>Upgrades monitoring feature</td>
<td>The system visualizes the alarms and monitoring data of multiple key metrics. The monitoring data is available via an API to ensure steady and smooth operation of your services.</td>
<td>2017-06</td>
<td>—</td>
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
<td>Security groups supports access control</td>
<td>The security group now provides the permission control feature to make your service more secure.</td>
<td>2017-05</td>
<td>Access Control Overview</td>
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
<td>Supports broadcast and multicast</td>
<td>Broadcast and multicast are one-to-many communications, which can help enterprises save network bandwidth and reduce network load through efficient point-to-multipoint data transmission.<li>Broadcast: Tencent Cloud supports subnet broadcast.</li><li>Multicast: Tencent Cloud supports VPC multicast.</li></td>
<td>2017-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31809" target="_blank">Enabling or Disabling the Broadcasting and Multicasting</a></td>
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
<td>Supports ENIs</td>
<td>The multi-ENI hot swapping service for CVMs helps you achieve isolation among private network, public network and management network, and deployment of high-availability services.</td>
<td>2016-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35502" target="_blank">Managing ENIs</a></td>
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
<td>Supports network topology</td>
<td>A network topology can clearly display your network architecture to help you easily tackle problems in network management.</td>
<td>2015-12</td>
<td>—</td>
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
<td>Launches VPC</td>
<td>A Virtual Private Cloud (VPC) is an independent isolated network space that supports software-defined networks. You can connect a VPC to your IDC via VPN connection or Direct Connect, flexibly creating a hybrid cloud.</td>
<td>2015-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215" target="_blank">VPC</a></td>
</tr>
</tbody></table>
